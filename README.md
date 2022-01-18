# git-in-depth

## What is Git?
Git is an Open Source Distributed Version Control System. Now that’s a lot of words to define Git.

## Git Foundation

### 1. Data Storage
At its core, git is like a key value store, the value = data & the key = hash of the data

### 2. Git Blobs & Trees
Git uses a series of BLOBs and trees to store content of the working directory of a project. Whenever we perform a commit operation, Git internally creates a series of trees and BLOBs, which is the binary representation of the project folder structure at that point in time of commit.

See example:
```
$ git init                   // initialize a repo
$ echo Hallo>hallo.txt        // create a file and enter some content
```

A tree is like a directory. Each commit in Git points to a tree object, which in turn references the BLOBs. A tree can recursively reference other tree objects or subtrees. Thus, a tree builds a complete hierarchy of files and subdirectories. Just like BLOBs, trees can be viewed under the “.git/objects” folder.

### 3. Git Commits
Git commit is a command line when you add some some changes in your local repo and want to push then first your have to run below command

```
% git cat-file -t 980a0
blob
% git cat-file -p 980a0
Hello World!
```

## Git Areas & Stashing
There are three core areas to git. These are the Working Tree, the Staging Area (also known as Index), and the Local Repository.

**Working Area:**
This file in local area or only in your device (untracked file), in there u can modify your content

**Stagging Area:**
This area used for thats file are going to be part of the next commit. this area know change between current commit and next commit

**Repository:**
This area contains all commits and contains all files you have committed in git

We use git stash to store our changes when they are not ready to be committed and we need to change to a different branch.
```
git stash save
# or
git stash
# or with a message
git stash save "this is a message to display on the list"
```

Apply stash to keep working on it:
```
git stash apply
# or apply a specific one from out stack
git stash apply stash@{3}
```
Every time we save a stash it gets stacked so by using list we can see all our stashes.
```
git stash list
# or for more information (log methods)
git stash list --stat
```
To clean our stack we need to manually remove them:
```
# drop top stash
git stash drop
# or
git stash drop <name>
# to clear all history we can use
git stash clear
```
Apply and drop on one command:
```
git stash pop
```

## References, Commits, Branches
There are 3 types of git references

**Tags & annotated tags**
are just a simple pointer to a commit. When you create a tag with no arguments, it captures the value in HEAD

**What is a branch?** 
So a branch, it's just a pointer to a particular commit. The pointer to the current branch is going to change.

**HEAD** 
is how git knows what branch you’re currently on, and what the next parent will be.
```
$ git checkout master
```
```
$ cat .git/HEAD
ref: refs/heads/master
```
```
$ git checkout feature
Switched to branch 'feature'
```
```
$ cat .git/HEAD
ref: refs/heads/feature
```

## Merging and Rebasing
Merge commits are just commit, but they happen to be commits that have more than one parent. It maintains all the same commits that you had created on a future branch.

### Merge Conflicts
Attempt to merge, but files have diverged
Git stops until the conflicts are resolved
```
$ git merge feature
CONFLICT (add/add): Merge conflict in feature
```
### Git Rerere
Once you set rerere.enabled, it's the act of merging itself that both creates the conflicts and (because it automatically runs git rerere with no arguments) records them and then tries to re-use any existing recorded resolutions. It's the act of committing itself that records the final resolutions (because Git automatically runs git rerere again for you). So it is all automatic—you just need to make sure, by running your own git diff commands, that your previous re-used resolutions are correct. If not, just fix them files, add, and commit as usual, and Git will replace the recorded resolutions with the new ones.

Note that you must still git add and git commit! You should always inspect the merge results (and/or run tests)—though you should do this always, regardless of your rerere.enabled setting.




