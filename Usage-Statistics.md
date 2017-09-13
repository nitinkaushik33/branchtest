In an attempt to ~~grossly violate people's privacy~~ get a sense of how people are using Processing, we keep a tally of what Libraries, Modes, Tools, and Examples that are installed when the PDE checks for updates for those items. (This can, of course, be turned off in Preferences, or by simply never using the Contribution Manager.) This is really helpful information for us to help understand the community, and to help us prioritize where we should put our very limited resources and time toward helping folks out.

Those stats are now available so that other developers can see what's being used via a simple set of endpoints. You could call it a REST API in the Cloud, which might be correct, but overdoing it. 

Use this URL to get the number of unique users who have opened the Contribution Manager in the last 30 days:
```
http://download.processing.org/stats/manager
```
As an inclusive community, we don't make a value judgement on who is unique and who is boring. 'Unique' in this context means that we're not counting the same person twice in one month. 

Note that this is different from the number of actual Processing users during that period: a rough estimate is that only a tenth of the users will open the Contribution Manager and be counted this way. (We may add more stats for other user numbers in the future.)

These next four links each provide a list of contributions (Library, Mode, Tool, or Examples) ranked by most-used, including the number of users for that type, and a URL to the item itself. 
```
http://download.processing.org/stats/libraries
http://download.processing.org/stats/modes
http://download.processing.org/stats/tools
http://download.processing.org/stats/examples
```
So for instance, visiting [http://download.processing.org/stats/libraries](http://download.processing.org/stats/libraries) will provide a list of Libraries (up to 100), ranked in order of how often they've been used in the past month, along with the number of users for each. Divide this number by the 'users' link above to get the percentage of the Processing community that's using your contribution. 

These are all in TSV format (tab separated values) for you numberly-minded folks to visualize to your hearts' content. The stats will be updated every 24 hours, and again, are relevant for the last 30 days (not calendar month). 

Enjoy!


## Example

The simplest is to grab a URL via `loadStrings()` or `loadTable()`. Here's a 15-minute sketch you can use as a starting point for something more interesting:

```processing
Table stats;
int visibleRows = 25;

int chartTop, chartBottom;
int chartLeft, chartRight;
int currentRow;


void setup() {
  size(600, 600);
  pixelDensity(displayDensity());
  
  // Do not call loadTable() from draw(). You'll be re-loading 
  // the table 60 times every *second*, and making our server slow.
  stats = loadTable("http://download.processing.org/stats/libraries", "tsv");
  textFont(createFont("Helvetica", 14));
  
  // add some margin
  chartTop = 20;
  chartBottom = height-chartTop;
  chartLeft = 20;
  chartRight = width - 80;
}


void draw() {
  background(255);
  cursor(HAND);
  
  // get the highest number from the first line, second column
  int highest = stats.getInt(0, 1);
  
  textAlign(LEFT, CENTER);
  strokeCap(SQUARE);
  strokeWeight(10);
  stroke(192);
  
  currentRow = -1;
  for (int row = 0; row < visibleRows; row++) {
    String title = stats.getString(row, 0);
    int count = stats.getInt(row, 1);
    //String url = stats.getString(row, 2);
    
    float x = map(count, 0, highest, chartLeft, chartRight);
    float y = map(row, 0, visibleRows-1, chartTop, chartBottom);
    line(chartLeft, y, x, y);
    
    fill(96);
    // if the mouse is nearby, select this row
    if (abs(y - mouseY) < 8) {
      currentRow = row;
      fill(0);
    }
    text(title, x + 8, y);
  }
}


void mousePressed() {
  if (currentRow != -1) {
    // open the url in a browser
    link(stats.getString(currentRow, 2));
  }
}
```