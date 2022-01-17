# git-in-depth

## What is Git?
Git is an Open Source Distributed Version Control System. Now that’s a lot of words to define Git.

## Git Foundation

### 1. Data Storage

### 2. Git Blobs & Trees
Git uses a series of BLOBs and trees to store content of the working directory of a project. Whenever we perform a commit operation, Git internally creates a series of trees and BLOBs, which is the binary representation of the project folder structure at that point in time of commit.

See example:
```
$ git init                   // initialize a repo
$ echo hello>file1.txt        // create a file and enter some content
$ echo hello>file2.txt        // create a file and enter the same content
$ echo hello world>file3.txt  // create a file and enter some content
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
