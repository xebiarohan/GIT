# GIT

Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.


If you are working in any software project then there are good chances that you already heard of GIT before. In this article we will deep dive into some uncommon git 
commands which can make out life easier.


## Stashing in GIT

It is used to store all the local changes (staged and unstaged changes) for future use and reverts them from your working copy. It takes you back to the working
directory HEAD commit (last commit).

#### Stashing all modified files

For commiting all modified files

```js
git stash   
```
or

```js
git stash push
```
It stores all the changes in a queue and these changes will be present in your local repository, not in remote repository.

### Fetching last stashed files

```js
git stash apply
```
or

```js
git stash pop
```
These commands will bring back all the last stashed changes to the current working directory. The difference between apply and pop is that in case of pop, it will bring back the changes but will not remove it from the stash queue, you have to manually remove it from queue using <b>'git stash drop'</b>, in case of apply it will 
bring back last changes and removes it from the stash queue.

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


## Resetting branch

git reset - It resets the current branch HEAD to a specfic state, it has 3 different form --hard, --soft and --mixed

### Hard resetting
It is the most widely used option, it is used when we are 100% sure to go to a particular commit and want to discard all the changes done after than incuding the 
staged, unstaged changes and all the commit done after that commit.

```js
git reset --hard {commit-id}
```

If you just want to remove all the staged changes and move back to the HEAD of the branch (most recently committed code) then

```js
git reset --hard HEAD
```

If you want to remove all the commits happen on any particular branch

```js
git reset --hard HEAD^
```


### Soft resetting 
Resets the pointer to the commit with the given commit id and add all the files of all commits following the given commit in the staged changes.
It is used in the scenarios like we did some mistage in the last commit or added some extra files. So we can reset the files and bring back them in staged state and
update the desired files or remove few files from commit using 'git reset {name of the file}' and can commit again.

```js
git reset --soft {commit-id}
```

Then we can unstaged the file which we want to update using 'git reset {name of the file}', update it and can push it again.

### Mixed resetting
It is the default resetting policy, it is similar to --soft resetting the only difference is that it takes all the files to unstaged state.It is used in the scenarios
like when we want to commit 1 or 2 files and by mistake we added all the files in the commit. So we can reset all the files in unstaged state and can select our desired files which we want to commit again.

```js
git reset --mixed {commit-id}
```
or

```
git reset {commit-id}
```

## Reverting commit

Reverts all the changes done in the given commit-id and add a new commit to maintain the history of deleting the commit.
This command requires your working tree to be clean (no modifications from the HEAD commit).

```js
git revert {commit-id}
```

Reverting undoes a commit by creating a new commit, where as git reset does alter the existing commit history. For this reason, git revert should be used to undo changes on a public branch, and git reset should be reserved for undoing changes on a private branch.

## Fetching remote branches

It is used to fetch all the remote branches which may be created by other developers working on the same repository.

```js
git fetch --all
```

It will fetch all remote branches.

## Removing unwanted files
Used to remove untracked, ignored files from the repository. Sometimes IDE creates some files in our local project repository, or my mistake we adds some files.
So to remove all these files we can use these commands.

### Removing untracked files
To interactively delete untracked files

```js
git clean -d -i 
```

The best thing about this command is it will ask you before deleting all the files, you can delete all files togather, can select files to delete by pattern like (\*.js) or can select by sequence number etc.

The -d option tells git to remove untracked directories too. If you don’t want to delete empty untracked directories, omit -d option.

-i is for interactive.

-n is used to do a dry-run, it will show all the files that will be deleted.


### Removing untracked files from a directory

If you want to limit the clean operation to given directories, pass the paths to the directories to be checked for untracked files as arguments to the command. For example, to check for files under the src directory, you would run:

```js
git clean -d -n {src}
```

### Removing ignored files
If you want to remove only the ignored files and directories, use the -X option:

```js
git clean -d -n -X
```
