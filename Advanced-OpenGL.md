This page covers OpenGL in Processing 3. These advanced OpenGL features in 3.x are significantly different from 2.x. Please note that these methods are not a supported part of the Processing API, but are documented here for advanced users with the caveat that they may break in future releases of Processing.

## Textures

All images in Processing are backed up by OpenGL [textures](http://www.learnopengl.com/#!Getting-started/Textures). By default, Processing uses the highest-quality texture filtering mode: `GL_LINEAR_MIPMAP_LINEAR` for the minification filter with mipmaps, `GL_LINEAR` for the magnification filter, and [anisotropic](https://www.opengl.org/registry/specs/EXT/texture_filter_anisotropic.txt) filtering if supported by the hardware. This combination is denoted as trilinear because of the `LINEAR_MIPMAP_LINEAR` and `GL_LINEAR` options. The mipmap generation can be disabled using `hint(DISABLE_TEXTURE_MIPMAPS)`.

There is no corresponding `PApplet` method to change the filtering options, however the renderer class, `PGraphicsOpenGL`, exposes a function that can be used for that purpose, called `textureSampling(int mode)`, where mode can take the values 2 (nearest), 3 (linear), 4 (bilinear), and 5 (trilinear):

```java
PImage img;
boolean highq = true;

void setup() {
  size(500, 500, P3D);
  img = loadImage("moonwalk.jpg");
}

void draw() {
  translate(0, 0, -100);
  rotateX(QUARTER_PI);
  image(img, 0, 0, width, height);
}

void keyPressed() {
  if (highq) {
    hint(DISABLE_TEXTURE_MIPMAPS);
    ((PGraphicsOpenGL)g).textureSampling(2);
    highq = false;
  } else {    
    hint(ENABLE_TEXTURE_MIPMAPS);
    ((PGraphicsOpenGL)g).textureSampling(5);
    highq = true;
  }
}
```

## Using the low-level OpenGL functions

Generally, this should be only considered a last-ditch way to get at a particular GL-specific feature. It can make your code incompatible with everything else (such as future versions of Processing or other 3D renderers) and will confuse the hell outta people when you post your code to the web. Again, if this works for you great, but if not, we aren't responsible. If you want to write code for Java and JOGL, then find yourself a good Java IDE and get JOGL installed, Processing is probably not the way to do it because that's the kind of confusing mess we're trying to insulate you from.

Due to the changes in the OpenGL renderer from Processing 1.x to 2.x, the way to access the low-level functions is quite different between the two, so examples using 1.x syntax will not work in later releases. 


Vertex coordinates are in Model Space
-------------------------------------

By default, all vertices are sent to the vertex shader already multiplied by the modelview matrix, and the modelview matrix in the vertex shader is set to the identity to avoid applying the transformation twice.

The reason for this seemingly puzzling approach is to optimize performance when drawing multiple shapes: since it is most efficient to minimize the number of buffer copies between CPU and GPU memory, the renderer batches as many shapes together as possible to draw them in a single call. However, if each shape had a different transformation, then it wouldn't be possible to group them because they would have different uniform matrices. You can disable the batching with `hint(DISABLE_OPTIMIZED_STROKE)`. More [here](https://github.com/processing/processing/issues/2904).


Processing 3.x
--------------

In Processing 3 we upgraded to JOGL [2.3.1](http://jogamp.org/wiki/index.php/Release_2.3.1), which introduced some [API changes](http://jogamp.org/deployment/v2.3.1/archive/API-Changes/semver-jogl-2.3.0-2.3.1.txt), but most importantly, we completely removed support for the fixed-function pipeline in 3.0 beta 5. What does this mean? Basically, you won't be able to use any of the old immediate mode GL calls such as glBegin(), glEnd(), and glVertex(), as well as the geometry transformations (glTranslate, glRotate, glScale) and lighting API. In addition to that, you will need to provide your own GLSL shaders implementing the rendering on the GPU. Since this change will surely break any Processing sketch that relies on the immediate mode functions, a brief explanation of the rationale behind it is in order. First of all, the immediate mode [was deprecated from OpenGL back in 2008](https://www.opengl.org/wiki/History_of_OpenGL#Deprecation_Model), but we were able to continue to expose through the [profile mechanism in JOGL](http://jogamp.org/jogl/doc/Overview-OpenGL-Evolution-And-JOGL.html). Over the past years, this gave us a way to support new functionality, like shaders and custom vertex attributes, while preserving to some degree compatibility with older sketches. With the widespread adoption of OpenGL on the Web and mobile through WebGL and OpenGL ES, and both skipping immediate mode and adopting GLSL shaders and the programmable-pipeline from the start, it became anachronistic to keep supporting the fixed-function pipeline, and even an obstacle to simplify graphics programming across multiple devices and platforms.

This section of the wiki is not meant to explain how the programmable-pipeline and GLSL shaders work, as there are many [excellent online resources](http://learnopengl.com/) about this topic, but below you have a Processing sketch for beta 5+ that uses low-level GL calls to render a simple object with GLSL shaders and Vertex Buffer Objects (VBOs). Note that any use of GL functions needs to happen between the beginPGL()/endGL() calls, through the corresponding JOGL interface object exposing the desired profile.

```java
import java.nio.ByteBuffer;
import java.nio.ByteOrder;
import java.nio.FloatBuffer;
import java.nio.IntBuffer;

import com.jogamp.opengl.GL;
import com.jogamp.opengl.GL2ES2;

PShader shader;
float a;

float[] positions;
float[] colors;
int[] indices;

FloatBuffer posBuffer;
FloatBuffer colorBuffer;
IntBuffer indexBuffer;

int posVboId;
int colorVboId;
int indexVboId;

int posLoc; 
int colorLoc;

PJOGL pgl;
GL2ES2 gl;

void setup() {
  size(800, 600, P3D);

  shader = loadShader("frag.glsl", "vert.glsl");  

  positions = new float[32];
  colors = new float[32];
  indices = new int[12];

  posBuffer = allocateDirectFloatBuffer(32);
  colorBuffer = allocateDirectFloatBuffer(32); 
  indexBuffer = allocateDirectIntBuffer(12);

  pgl = (PJOGL) beginPGL();  
  gl = pgl.gl.getGL2ES2();

  // Get GL ids for all the buffers
  IntBuffer intBuffer = IntBuffer.allocate(3);  
  gl.glGenBuffers(3, intBuffer);
  posVboId = intBuffer.get(0);
  colorVboId = intBuffer.get(1);
  indexVboId = intBuffer.get(2);    

  // Get the location of the attribute variables.
  shader.bind();
  posLoc = gl.glGetAttribLocation(shader.glProgram, "position");
  colorLoc = gl.glGetAttribLocation(shader.glProgram, "color");
  shader.unbind();

  endPGL();
}

void draw() {
  background(255);

  // Geometry transformations from Processing are automatically passed to the shader
  // as long as the uniforms in the shader have the right names.
  translate(width/2, height/2);
  rotateX(a);
  rotateY(a*2);  

  updateGeometry();

  pgl = (PJOGL) beginPGL();  
  gl = pgl.gl.getGL2ES2();

  shader.bind();
  gl.glEnableVertexAttribArray(posLoc);
  gl.glEnableVertexAttribArray(colorLoc);  

  // Copy vertex data to VBOs
  gl.glBindBuffer(GL.GL_ARRAY_BUFFER, posVboId);
  gl.glBufferData(GL.GL_ARRAY_BUFFER, Float.BYTES * positions.length, posBuffer, GL.GL_DYNAMIC_DRAW);
  gl.glVertexAttribPointer(posLoc, 4, GL.GL_FLOAT, false, 4 * Float.BYTES, 0);

  gl.glBindBuffer(GL.GL_ARRAY_BUFFER, colorVboId);  
  gl.glBufferData(GL.GL_ARRAY_BUFFER, Float.BYTES * colors.length, colorBuffer, GL.GL_DYNAMIC_DRAW);
  gl.glVertexAttribPointer(colorLoc, 4, GL.GL_FLOAT, false, 4 * Float.BYTES, 0);

  gl.glBindBuffer(GL.GL_ARRAY_BUFFER, 0);

  // Draw the triangle elements
  gl.glBindBuffer(PGL.ELEMENT_ARRAY_BUFFER, indexVboId);
  pgl.bufferData(PGL.ELEMENT_ARRAY_BUFFER, Integer.BYTES * indices.length, indexBuffer, GL.GL_DYNAMIC_DRAW);
  gl.glDrawElements(PGL.TRIANGLES, indices.length, GL.GL_UNSIGNED_INT, 0);
  gl.glBindBuffer(PGL.ELEMENT_ARRAY_BUFFER, 0);    

  gl.glDisableVertexAttribArray(posLoc);
  gl.glDisableVertexAttribArray(colorLoc); 
  shader.unbind();

  endPGL();

  a += 0.01;
}

void updateGeometry() {
  // Vertex 1
  positions[0] = -200;
  positions[1] = -200;
  positions[2] = 0;
  positions[3] = 1;

  colors[0] = 1.0f;
  colors[1] = 0.0f;
  colors[2] = 0.0f;
  colors[3] = 1.0f;

  // Vertex 2
  positions[4] = +200;
  positions[5] = -200;
  positions[6] = 0;
  positions[7] = 1;

  colors[4] = 1.0f;
  colors[5] = 1.0f;
  colors[6] = 0.0f;
  colors[7] = 1.0f;

  // Vertex 3
  positions[8] = -200;
  positions[9] = +200;
  positions[10] = 0;
  positions[11] = 1;    

  colors[8] = 0.0f;
  colors[9] = 1.0f;
  colors[10] = 0.0f;
  colors[11] = 1.0f;

  // Vertex 4
  positions[12] = +200;
  positions[13] = +200;
  positions[14] = 0;
  positions[15] = 1;

  colors[12] = 0.0f;
  colors[13] = 1.0f;
  colors[14] = 1.0f;
  colors[15] = 1.0f; 

  // Vertex 5
  positions[16] = -200;
  positions[17] = -200 * cos(HALF_PI);
  positions[18] = -200 * sin(HALF_PI);
  positions[19] = 1;

  colors[16] = 0.0f;
  colors[17] = 0.0f;
  colors[18] = 1.0f;
  colors[19] = 1.0f;

  // Vertex 6
  positions[20] = +200;
  positions[21] = -200 * cos(HALF_PI);
  positions[22] = -200 * sin(HALF_PI);
  positions[23] = 1;

  colors[20] = 1.0f;
  colors[21] = 0.0f;
  colors[22] = 1.0f;
  colors[23] = 1.0f;

  // Vertex 7
  positions[24] = -200;
  positions[25] = +200 * cos(HALF_PI);
  positions[26] = +200 * sin(HALF_PI);
  positions[27] = 1;    

  colors[24] = 0.0f;
  colors[25] = 0.0f;
  colors[26] = 0.0f;
  colors[27] = 1.0f;

  // Vertex 8
  positions[28] = +200;
  positions[29] = +200 * cos(HALF_PI);
  positions[30] = +200 * sin(HALF_PI);
  positions[31] = 1;

  colors[28] = 1.0f;
  colors[29] = 1.0f;
  colors[30] = 1.1f;
  colors[31] = 1.0f; 

  // Triangle 1
  indices[0] = 0;
  indices[1] = 1;
  indices[2] = 2;

  // Triangle 2
  indices[3] = 2;
  indices[4] = 3;
  indices[5] = 1;

  // Triangle 3
  indices[6] = 4;
  indices[7] = 5;
  indices[8] = 6;

  // Triangle 4
  indices[9] = 6;
  indices[10] = 7;
  indices[11] = 5;  

  posBuffer.rewind();
  posBuffer.put(positions);
  posBuffer.rewind();

  colorBuffer.rewind();
  colorBuffer.put(colors);
  colorBuffer.rewind();

  indexBuffer.rewind();
  indexBuffer.put(indices);
  indexBuffer.rewind();
}  

FloatBuffer allocateDirectFloatBuffer(int n) {
  return ByteBuffer.allocateDirect(n * Float.BYTES).order(ByteOrder.nativeOrder()).asFloatBuffer();
}

IntBuffer allocateDirectIntBuffer(int n) {
  return ByteBuffer.allocateDirect(n * Integer.BYTES).order(ByteOrder.nativeOrder()).asIntBuffer();
}
```

Since now the shaders must to be provided explicitly, below you have the code for the vertex and fragment shaders used in this example:

```glsl
// vert.glsl
#version 150

uniform mat4 transform;

in vec4 position;
in vec4 color;

out vec4 vertColor;

void main() {
  gl_Position = transform * position;
  vertColor = color;
}
```

```glsl
// frag.glsl
#version 150

uniform mat4 transform;

in vec4 vertColor;

out vec4 fragColor;

void main() {
  fragColor = vertColor;
}
```

A few additional notes:

* You must include the #version preprocessor directive as the first line of your GLSL code, indicating what version of the GLSL language you are using. This version must match the OpenGL profile selected by Processing, which by default is [GL2ES2](https://jogamp.org/deployment/v2.2.4/javadoc/jogl/javadoc/javax/media/opengl/GL2ES2.html) -essentially the intersection between the GL2 and GLES2 APIs. If you don't provide the #version directive and the GLSL version in the computer is 1.30 or higher, then Processing assumes that the shader code is 1.10 or 1.20 and it applies a pre-processing step to make sure the code valid for the GLSL compiler.
* You can use the [PShader](https://processing.org/reference/PShader.html) class as a helper to handle the tedious aspects of loading and compiling your GLSL code. The shader needs to be bound/unbound as shown in the example so it does render the geometry as expected. If you don't wan to use PShader, you can simply rely on the low-level GL calls to manually load the shader code and to compile it into the corresponding GL shader objects. JOGL's [utility classes](https://jogamp.org/deployment/jogamp-next/javadoc/jogl/javadoc/com/jogamp/opengl/util/glsl/ShaderCode.html) can be used as well.
* Geometry transformations and lighting configuration defined with Processing calls (i.e: [translate()](https://processing.org/reference/translate_.html), [lights()](https://processing.org/reference/lights_.html)) will be automatically passed over the the GLSL shader when loading it loadShader(), provided that the uniforms inside the shader code follow certain naming conventions, which are detailed in [this tutorial](https://processing.org/tutorials/pshader/). If the shader is initialized manually, you will need to handle all the geometry transformation math yourself.
* Processing by default creates a GL2ES2 profile, but if you need more advanced functionality available in higher profiles -and they are supported by your OpenGL driver- you can explicitly request profiles 3 and 4 by using the [settings()](https://processing.org/reference/settings_.html) function:

```java
void settings() {
  size(400, 400, P3D);
  PJOGL.profile = 4;
}

void setup() {
  // ...
}
```
* When working with profiles 3 and 4, you can subclass the PShader class to implement your own custom geometry and tessellation shaders, to see how to do this take a look at the sample code available in [this repo](https://github.com/codeanticode/pshader-experiments), particularly [SphereSubdivGS](https://github.com/codeanticode/pshader-experiments/blob/master/SphereSubdivGS/GeometryShader.pde), [SphereTess](https://github.com/codeanticode/pshader-experiments/blob/master/SphereTess/TessellationShader.pde), and [TerrainTess](https://github.com/codeanticode/pshader-experiments/blob/master/TerrainTess/GL4Shader.pde).


Processing 2.x
----------------------

We no longer support this version, but in case you are stuck with some OpenGL code in Processing 2.x, maybe [this old section](Advanced-OpenGL-in-Processing-2.x) can be useful.