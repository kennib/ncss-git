# Version Control
## What exactly is version control?
Version control is simply a way to track your files as they change. 

At its core it's really not that complicated at all.
You may have even created a very simple version of it yourself.
Something like this:

  * ~Essay FINAL really final this time.doc
  * Essay.doc
  * Essay (final draft).doc
  * Essay FINAL.doc
  * Essay FINAL1.doc
  * Essay FINAL countdown.doc
  * Essay (first draft).doc
  * Essay (first draft) 1.doc

## Why use a version control tool?
There are many problems that will appear with a solution like the above one.
What is the file we're currently working on?
How do we find that sentence about the effect of the plutocracy on bourgeois society? Was it in "Essay FINAL.doc" or "Essay.doc"?
What if we just want to change back to the version of the essay we had at the start of the day? What if we've already saved over that version?
What if we need to collaborate with someone on our essay? Do we have to manual go through and find all the changes we both made and merge them together?

We could of course come up with increasingly more consistent and complicated schemes for naming and storing our files.
At some point though we should probably ask ourselves if someone has already made a tool for helping us do this.
The answer is of course yes! There are many different version control systems available.
At NCSS we will be using git <http://git-scm.com/>


# Git
## What is git?
### The components of git
<!--- It would be helpful to have a diagram that summarises this section --->

In the most basic sense git is made up of collections of files called "repositories".
Each repository is a directory that contains the files for a particular project, for example a small social network site.

A repository also contains the history of these files as they've changed.
These changes are known as "commits".

Each commit can have multiple files associated with it and has associated with it a message that describes the commit's contents.
Commits are manually created and can be considered a discrete set of work done.
That is, I wouldn't commit every time I saved my python program because a program with synatx errors probably isn't helpful to keep a record of.
But I would commit if I had written a simple working version of a function that I planned to make more complicated.

Before commiting files we first "stage" them.
This staging helps us differentiate changes we want to commit (i.e., record the history of) and those we want to ignore for now.
Staging allows to add/remove files from a commit before confirming the commit and giving the commit a descriptive message.

In git there is a distinction between "tracked" and "untracked" files.
Tracked files have been staged and then commited.
They are associated with the repository and will be copied if the repository is "cloned".
Untracked files are files that are not associated with the repository since they have never been committed or removed from the repository.
Both tracked and untracked files can exist in the same directory as the repository. Only tracked files are a part of the repository.

