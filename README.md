# GIT

Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.


If you are working in any software project then there are good chances that you already heard of GIT before. In this article we will deep dive into some uncommon git 
commands which can make out life easier.


## Stashing in GIT

It is used to store all the local changes (staged and unstaged changes) for future use and reverts them from your working copy. It takes you back to the working
directory HEAD commit (last commit).

### Commiting all modified files

For commiting all modified files

```js
git stash   
```
or

```js
git stash push
```
It stores all the changes in a queue and these changes will be present in your local repository, not in remote repository.

### Fetching back files from last commit.

```js
git stash apply
```
or

```js
git stash pop
```
These commands will bring back all the last stashed changes to the current working directory.

### checking all last stashed files.

```js
git stash show
```
Shows all the file which got saved in queue in the last stash.

### Checking all stashes 

```js
git stash list
```

Shows all the stashes present in the queue, It contains information like stash id (like stash@{0}, stash@{1}), branch name from where they got stashed and
last commit description.
example
```js
stash@{0}: WIP on feature/TE-4312: 61307eaca last commit message on feature/TE-4312 branch
stash@{1}: WIP on feature/TE-4513: bba77bd0a last commit message on feature/TE-4513 branch
stash@{2}: WIP on feature/TE-1234: dc42acaf1 last commit message on feature/TE-1234 branch
```
stash@{0}, stash@{1}, and stash@{2} are the stash ids.
feature/TE-4312, feature/TE-4513, feature/TE-1234 are the branch names.
61307eaca, bba77bd0a, dc42acaf1 are the commit ids.
and the remaining part are the commit messages.


### Fetching older shash files

We can do multiple stashes and can pull out the changes of older shash

```js
git stash pop {stash-id}
```

we can first check the stash id using 'git stash list' then can use this command to pull desired files changes. Stash id 

### Stashing specific file

```js
git shash push {filepath}
```
It will stash a given file.

### Stashing multiple files

```js
git stash push {filepath1} {filepath2} ... {filepathN}
```

This command is used when we want to stash multiple files but not all the files.

### Clearing stash queue

```js
git stash clear
```
It will remove all the stash items from the queue.
