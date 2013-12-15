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
That is, I wouldn't commit every time I saved my python program because a program with syntax errors probably isn't helpful to keep a record of.
But I would commit if I had written a simple working version of a function that I planned to make more complicated.

Before committing files we first "stage" them.
This staging helps us differentiate changes we want to commit (i.e., record the history of) and those we want to ignore for now.
Staging allows to add/remove files from a commit before confirming the commit and giving the commit a descriptive message.

In git there is a distinction between "tracked" and "untracked" files.
Tracked files have been staged and then committed.
They are associated with the repository and will be copied if the repository is "cloned".
Untracked files are files that are not associated with the repository since they have never been committed or removed from the repository.
Both tracked and untracked files can exist in the same directory as the repository. Only tracked files are a part of the repository.

### Collaborating with git
<!--- This section should also have a diagram --->

Git is a "Distributed Version Control System".
This means that everyone has their own repository with its own files and commits.
The repository you have is called the "local" repository. External repositories are called "remote" repositories.
Collaboration is done by "push"ing and "pull"ing code to and from remote repositories.

Let's say your friend has a repository for a cool space invaders game and you'd like to make some improvements to it.
The first thing we would do is create our own local version of the repository by "cloning" it.

The next step is making our changes to the game, sound effects and James Curran UFOs.
Ideally committing each of these changes separately.
Then we "push" the changes we made to our friend.

Our friend then makes some changes of his own which include some better colours and graphics.
We can get these changes from her remote repository by telling git to "pull" them.
A git "pull" essentially "fetches" the changes from the remote location and "merges" them with our changes.

## A Walkthrough
All of these concepts can be quite tricky to understand.
Especially if you've never used a version control system before.
Perhaps the best way to learn version control is by using it in a real world setting.

The following section walks through how a group of programmers might use version control.
You don't need to understand it all at once and you certainly don't need to remember it all.
Use each section as a reference for how to perform certain tasks with version control.

There will be screenshots of Github for Windows and command line samples.
Feel free to use whichever you are most comfortable with.

### The scenario
Dom, Smerity, Kenni and Georgina are creating a social network site with python!
For the sake of brevity let's call this team "Group 0".
All of them have Github for Windows installed already.
All of them will be adding changes to the project at some stage.

### Getting set up
The first thing Group 0 need to do is create a new repository.

<!---
I don't know if we want to use Github or Bitbucket as opposed to a vanilla git repo
I'm inclined to avoid Github and Bitbucket to avoid having to create/manage accounts for those services.
  - Kenni
--->

Kenni creates a repository called ncssbook.

<!--- Screenshot of GfW repo creation --->
![Information is eneter about the repository and then the create button is clicked](images/create-gw.png "Creating a repository")
![The repository is created and is shown in the list](images/created-gw.png "The repository has been created")

```bash
git init ncssbook
```

This repository won't be worked on directly by any of Group 0.
Instead this repository is like a remote backup that will be updated with the latest version of the code as the group member "push" it out.

<!--- Diagram of the relationship between the repos --->


Now everyone has to "clone" a copy of ncssbook for themselves.
To be able to do this they have to be able to access the repository over the internet.
Luckily Kenni has put the repo on the NCSS servers.

To clone the repository Dom simply drags a link to the repository onto Github for Windows.

<!--- Screenshot of GfW repo cloning --->
![Drag any url (must start with the protocol e.g. `http`) onto the window](images/clone-gw.png "Clone the repository")
![The repository is cloned and opened](images/cloned-gw.png "The repository is cloned")

```bash
git clone http://ncss.edu.au/2014/group0/ncssbook.git
```


### Adding new files
The first thing Group 0 are going to do with this new repository is create an index page for their social network.
To do this Georgina simply creates a file called `index.html` using her favourite text editor (vimacs).

<!--- Screenshot of folder --->
![There is now an index.html file in the ncssbook folder](images/newfile-ex.png "index.html file is created")

Once the file exists it can be added to the repository using Github for Windows.
We can see on thee right hand side of the window the list of new files.
For the moment this is just `index.html`.
The checkbox next to its name indicates Georgina wants it to be part of the repository.

<!--- Screenshot of new files in GfW --->
![The index.html file is listed as 'NEW' in Github for Windows](images/newfile-gw.png "index.html is list as a new file")

```bash
# Show the files that are new
git status

# Add the index page to the commit
git add index.html
```
Now it's time for Georgina to commit the changes to her repository.
To do this she adds a message to the text field and then clicks 'commit to master'.

<!--- Screenshot of committing in GfW --->
![The commit message is entered into the text field and then the 'commit to master' button gets clicked](images/commit-gw.png "A helpful commit message is written")

```bash
git commit -m "The new home page for NCSSBook"
```

![The commit has been added and we now have a record of our changes](images/committed-gw.png "The commit has been added")

```bash
git log
```


### Sharing the changes
At the moment Georgina is the only person who has the NCSSBook homepage.
So the next step for Georgina is to push the commit containing `index.html` to the remote repository Kenni created.

<!--- Screenshot of pushing commits in GfW --->
![The commit gets pushed to the remote server when the 'publish' button is clicked](images/push-gw.png "The commit is pushed to the remote server")
![The commit moves from 'unsynced commits' to 'history'](images/pushed-gw.png "The commit is now synced")

```bash
git push
```

Now everyone else in Group 0 can pull the changes stored on the remote repository.
For example Smerity clicks on the 'sync' button to pull the commit.

<!--- Screenshot of pullng commits in GfW --->
![The changes pushed from the remote repository have been pulled to a different local repository](images/pull-gw.png "The commit is now synced")

```bash
git pull
```

### Fixing mistakes

<!---
Unstaging files
  git reset HEAD

Untracking files
  git rm --cached <file>
Completely remove file
  git rm <file>

Undo the last commit 
  git reset --soft HEAD^

Fixing the previous commit
  git add <file> 
  git commit --amend

Why it's a bad idea to try and change the remote repo's history
--->


### Merging other people's work

<!---
Situations where we can't push due to changes to the remote repo
  git push

Merge conflict
  git pull
Make changes to fix conflict
  git merge
--->


### Avoiding conflicts

<!---
Why branches?

Create a new branch
  git branch <branch>

Changing branch
  git checkout <branch> 

Merging branches
  git checkout <branch-to-merge-into>
  git merge <branch-to-merge>
---> 


### Going back in time

<!---
Viewing old commits
  git log

Labelling commits
  git tag

Stashing changes temporarily
  git stash
Quick changes
  git pop

Viewing old files
  git diff <commit-a> <commit-b>

Revert to previous commit
  git reset --hard

Revert to old commit
  git revert <commit>
--->

## Workflow
<!--- A digram explaining the stage/commit/pull/push workflow --->
