This tutorial will show you how to successfully contribute a bug-fix to Processing using GitHub's Pull Request workflow.

You'll be typing git commands in the Terminal. Mac and Linux users may have git pre-installed. You can download git from [here](http://git-scm.com/downloads). Windows users must use the included git bash application. (seriously, don't use command prompt).

The tutorial assumes you have some basic understanding of git concepts - repositories, branches, commits, etc. Explaining it all from scratch is beyond the scope of this tutorial. Some good links to learn git basics are: [Link 1](http://git-scm.com/book/en/Getting-Started-Git-Basics), [Link 2](https://www.atlassian.com/git/tutorial/git-basics)

Keep in mind that Processing has multiple repositories that deal with various parts of the Processing project. There are separate repos for documentation, android, video-library, etc. You can know more about them in the [Repositories](https://github.com/processing/processing/wiki/Repositories) page. You need to work with the repo to which you want to submit a bug fix.

Before starting, ensure that the bug has been reported in the **Issues** tab of the repo. Sometimes you may come across a bug which might not have been reported yet. **Open an issue for it, and then proceed with the bug fix.**

## Step 1: Setup your Processing Fork

* You'll make your changes in your own copy of the processing repo. Go to the processing GitHub repo and press the **Fork** button. Your fork should be ready in a few minutes. You need to download a copy of your fork to your local machine (aka cloning your repo). In the terminal, type:

````
git clone <your-repo's-git-url>
````

This will clone your repo into the current folder. The main processing repo is about a 1.5 GB download, so it may take some time.

You can find your repo's git url on the repo page. The url looks like this: `https://github.com/<your-username>/<repo-name>.git`

***

**Optional:** If you're using git 1.9 or above, you can optionally shallow clone repos using the `--depth` option. The download size is then greatly reduced. (~50 MB instead of the full 1.5 GB for the main repo). See [this link](http://stackoverflow.com/questions/6941889/is-git-clone-depth-1-shallow-clone-more-useful-than-it-makes-out) for more.

````
git clone <your-repo's-git-url> --depth 1
````
The above command will fetch the history of just the latest commit instead of all the commits. A shallow clone is helpful if you're planning to submit a quick patch. Git 1.9 is relatively new, so you'll probably need to update your git installation before using this option.

***

### Syncing your Fork

* Use the following command to add **upstream** (original project repo) as a remote repo so that you can fetch the latest processing commits into your branch and keep your forked copy in sync.

````
git remote add upstream https://github.com/processing/processing.git
````

This will add the original processing repo as a remote repo named **upstream**. (Remote repositories are versions of your project that are hosted on the Internet or network somewhere.) If you've cloned processing-docs, use its url as the upstream url.

* To sync your fork to the latest commit in the processing repo, type:

````
git fetch upstream
````
(fetches the latest commits from the processing repo)

````
git merge upstream/master
````
(merges the master branch of the processing repo with your current branch)

* Now your local copy of your fork has been synced. But the fork's copy is not updated on GitHub's servers yet. To do that, use:

````
git push origin master
````

(pushes the changes to your fork's online copy.)

Phew, that was a lot. Don't worry, the setup is just a one time gig.

## Step 2: Hacking Processing

So your fork is now setup and you're ready to hack Processing and squash that bug.

Now here's the part people usually don't figure out until it's too late - Do not commit any changes to your fork's master branch! The master branch of your fork is always kept in sync with processing's master branch (from remote). 

It's a good practice to make changes in your fork in a separate branch. You can submit only ONE pull request per branch. So create a new branch for the bug-fix/feature-enhancement that you'd like to work on.

* Before creating a new branch, it's best to sync your fork and then create a new branch from the latest master branch. If you're not on the master branch, switch to it using:

````
git checkout master
````

* To create a new branch, use: 

````
git branch bugfix-frameRate
````
(where `bugfix-frameRate` is the name of the branch in your fork)


**Side note:** We recommend naming branches using the following convention:

1. Branches that fix bugs are named bugfix-{description}, e.g. `bugfix-frameRate`

2. Branches that add features are named feature-{description}, e.g. `feature-frenchTranslation`

* Switch to the branch using: 

````
git checkout bugfix-frameRate
````

***

**Protip:** Create and checkout a branch in one line using:

````
git checkout -b bugfix-frameRate
````

***

* Now comes the part where you step up. Make those awesome fixes till you feel the bug's been taken care of (meaningful commit messages appreciated).

* Remember to push your changes in your branch to GitHub using: 

````
git push origin bugfix-frameRate
````

### Some things to keep in mind for a PR

* Try to make the minimum required changes to fix the issue. If you've added any debugging code, etc remember to remove or comment them.
* The PR should deal with one issue at a time only, unless two issue are so interlinked they must be fixed together.
* Avoid unnecessary formatting or whitespace changes in other parts of the code. Be wary of auto-format options in your code editor which can cause wide scale formatting changes.
* Adhere to Processing [Code Style](https://github.com/processing/processing/wiki/Style-Guidelines).
* Make sure Processing's ant build doesn't fail because of any changes you introduce.
* Add code comments whenever you feel that the meaning or function of your code is not obvious.

## Step 3: Submitting a Pull Request

* Ensure you've pushed the changes in your branch to GitHub. Go to your GitHub repo page and switch to `bugfix-frameRate` branch.

* You need to submit a PR from the `bugfix-frameRate` branch to processing's `master` branch. 

* Click on the **Pull Request** button.

* Describe your PR thoroughly. Then press **Send Pull Request**. 

The project maintainers have other commitments as well, so they may not always be able to checkout your PR quickly. Please be patient and give them some time to go through it.

Once they take a look at your PR, they may sometimes suggest additional changes. So you'll need to make those changes in your branch, and push those changes to your repo. Your PR will always include the latest changes in your branch on GitHub, so you don't need to resubmit the PR.

Once your changes have been accepted, a project maintainer will merge your pull request.

Congratulations, you just successfully contributed your first patch!

We are grateful to the users for their time and effort in contributing fixes. But please understand that project maintainers may sometimes choose to not accept your PR. This may happen due to technical or organizational reasons. The project heads have the final say in this regard. (It is also a good idea to discuss the bug in its issues page before working on a fix).

Happy Hacking!

--
This tutorial was adapted from [this excellent guide](https://gun.io/blog/how-to-github-fork-branch-and-pull-request/).