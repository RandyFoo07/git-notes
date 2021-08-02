# Notes on Git

_omit `[]`, include `""` when using this sheet, [file1] -> "test.txt"_  
_use [imperative mood](#https://en.wikipedia.org/wiki/Imperative_mood) for commit messages_

# Table of Contents

**[First Time Setup](#First-Time-Setup)**  
**[Cloning/Initializing a Repository](#Cloning--Initializing-a-Repository)**  
**[Commonly Used Commands](#Commonly-Used-Commands)**  
**[Commonly Used Commands for Fixing Mistakes](#Commonly-Used-Commands-for-Fixing-Mistakes)**  
**[Common Workflow with Branches](#Common-Workflow-with-Branches)**  
**[Restoring Deleted Commits](#Restoring-Deleted-Commits)**  
**[Contributing to Open Source Projects on GitHub](#Contributing-to-Open-Source-Projects)**  
**[Creating a Private Forked Repository](#Creating-a-Private-Forked-Repository)**  
**[Accessing Manual Page for Commands](#Manual-Page)**  
**[The .gitignore File](#gitignore)**

<br>
<br>

## First Time Setup

1. `$ git config --global user.name "name"`  
   Set username so that it appears in git log commits
2. `$ git config --global user.email "email address"`  
   Set email so that it appears in git log commits
3. `$ git config --global color.ui auto`  
   Enable auto command line coloring
4. `ssh-keygen -C [email]`  
   Creates a SSH Key as an identifier for the machine in use
5. `cat ~/.ssh/id_rsa.pub`  
   Copy output of command above (starting from `ssh-rsa`)
6. Github -> Settings -> SSH and GPG keys -> New SSH Key  
   Paste copied output into key field -> Add SSH key
7. `$ ssh -T git@github.com`  
   Verify SSH key with Github (if prompted, type `yes`)

- `$ git config --list`  
  To check current configuration
- `ls ~/.ssh/id_rsa.pub`  
  To check if any SSH key is installed

<br>
<br>

## Cloning / Initializing a Repository

#### Initializing

1. `$ git init`  
   Turn current directory into a Git repository
2. `$ git add .`  
   Add current directory (and all its subdirectories) to staging area
3. `$ git commit -m "Initial commit"`  
   Commit files in staging area with included message
4. Create a repository (on Github)
5. `$ git remote add origin [url copied from Github]`  
   Create a new remote named origin located at url (Origin can be replaced with any name)
   _Push/Pull commands can be used with origin now instead of typing out the url_
6. `$ git push -u origin master`  
   Push changes to remote repository

#### Cloning

1. Create a repository (on Github)
2. `$ git clone [url copied from Github]`  
   Copy remote repository to local machine as a folder

<br>
<br>

## Commonly Used Commands

- `$ git add .` / `$ git add [file1] [file2]`  
  Add current directory (and all its subdirectories) or file(s) to staging area.  
  _Types of add [here](#Git-add-Types)_
- `$ git commit` / `$ git commit -m "message"`  
  Commit files in staging area with message  
  If `-m` is ommited, will be brought to [default git editor (nano/vim)](#Using-git-editornanovim-when-committing-without--m) to enter multi-line commmit message, a format of `$ git commit -m "Head message" -m "Description"` can also be used instead
- `$ git commit -am "message"`  
  Add and commit all modified files with message in one command  
  _Does not add any untracked files_
- `$ git pull` / `$ git pull origin master`  
  Pull changes from current working branch or master branch of remote 'origin'  
  _`$ git pull -u origin master` may be required for pulling for the first time to associate local branch with remote branch_
- `$ git push` / `$ git push origin master`  
  Push staged files to current working branch or master branch of remote 'origin'  
  _`$ git push -u origin master` may be required for pushing for the first time to associate local branch with remote branch_
- `$ git status`  
  Show status of files in local repository
- `$ git diff`  
  Show changes made to local repository
- `$ git log` / `$ git log --stat`  
  Show all commits or commits with detailed changes made in current branch
- `$ git remote -v`  
  List information on remote repository
- `$ git remote rename [name1] [name2]`  
  Rename remotes named 'name1' to 'name2'
- `$ git remote set-url origin [url] / $ git remote set-url upstream [url]`  
  Replace existing remote repository to new remote repository
- `$ git branch` / `$ git branch -a`  
  List all branches on local repository or local and remote repositories
- `$ git branch [name]`  
  Create a branch
- `$ git checkout [branchname]`  
  Switch to the named branch
- `$ git stash save "message"`  
  Save and stash all changes since last commit in current branch  
  _Useful for transferring changes (still in working directory) from one branch to another_
- `$ git stash list`  
  Show list of stashes
- `$ git stash apply [stashid]`  
  Applying changes from stated stash, not removing it from the list
- `$ git stash pop`  
  Apply the first stash from the stash list and remove it from the list
- `$ git stash drop [stashid]`  
  Delete changes from stated stash and remove it from the list
- `$ git stash clear`  
  Remove and clear all changes from all stashes

#### Git add Types

- `$ git add -A` / `$ git add --all` - **Default**  
  Add entire working tree (all directories including parent and sub directories) to staging area  
  If a directory is added as a argument, `$ git add -A dir/`, only adds files in directory stated and its sub directories  
  _`$ git add -A dir/` is the same as `$ git add dir/`_
- `$ git add -u` / `$ git add --update`  
  Add modified and deleted files but not untracked files (for entire working tree)  
  If a directory is added as a argument, `$ git add -u dir/`, only adds files in directory stated and its sub directories

#### Git reset Types

- `$ git reset [hash of commit to reset to]` - **Default**  
  Reset to a commit, but keep changes in the working directory
- `$ git reset --soft [hash of commit to reset to]`  
  Reset to a commit, but keep changes in the staging area
- `$ git reset --hard [hash of commit to reset to]`  
  Reset to a commit, and remove all changes made before except untracked files

#### Using git editor(nano/vim) when committing without -m

##### Nano

1. `Ctrl + X` (to prompt exit after entering commit message)
2. `Y` (to save changes)
3. `Enter` (to exit)

##### Vim

1. `1` (to enter commit message)
2. `esc` (to prompt exit)
3. `:wq`
4. `Enter` (to exit)

<br>
<br>

## Commonly Used Commands for Fixing Mistakes

- `$ git checkout` / `$ git checkout [file1] [file2]`  
  Remove any changes to all files or file(s) not in staging area, back to as it is from last commit
- `$ git reset` / `$ git reset [file1] [file2]`  
  Unstage all files or file(s) selected in the working directory
- `$ git commit --amend -m "Correct message"`  
  Replace the last commit (only commits that has not been pushed), including a corrected message if necessary  
  _If a file is added after a commit, using the above command will add the file along with the corrected commit message to replace the last commit. This is used if a file intended for a commit was not added_
- `$ git cherry-pick [hash of commit to copy]`  
  Copy a commit to the current branch  
  _Able to copy commits from other branches (hash of commit can be shown in `$ git log`)_
- `$ git reset [hash of commit to reset to]`  
  Reset to a commit, deleting any commits that comes after it.  
  _Types of resets [here](#Git-reset-Types)_
- `$ git clean -df`  
  Remove any untracked directories and files
- `$ git reflog`  
  Shows all commits in the order of last being referenced
- `$ git revert [hash of commit]`  
  Add a new commit resetting the commit with the hash entered  
  _This is only intended if the commit that needs resetting has already been pushed to the remote repository_

<br>
<br>

## Common Workflow with Branches

1. `$ git branch [featureName]`  
   Create branch intended for a new feature/thing
2. `$ git checkout [featureName]`  
   Switch to newly created branch
3. `$ git add -A`  
   Add modified files to staging area
4. `$ git commit -m "Do something"`  
   Commit files in staging area
5. `$ git push -u origin [featureName]`  
   Push branch containing committed files to remote repository
6. `$ git checkout master`  
   Switch to master branch
7. `$ git pull origin master`  
   Pull any changes from remote repository to make sure master branch of local repository is up to date
8. `$ git merge [featureName]`  
   Merge branch into master branch
9. `$ git push origin master`  
   Push changes (merged branch) to master branch of remote repository
10. `$ git branch -d [featureName]`  
    Delete branch in local repository
11. `$ git push origin --delete [featureName]`  
    Delete branch in remote repository

- `$ git branch --merged`  
  List all the branches merged

<br>
<br>

## Restoring Deleted Commits

1. `$ git reflog`  
   Shows all commits in the order of last being referenced
2. `$ git checkout [hash of commit before reset(from reflog)]`  
   Go to the commit before deleting last commit
3. `$ git branch backup`  
   Create a backup branch containing deleted commit
4. `$ git checkout master`  
   Go to the master branch or any branch intended for the commit to be copied to
5. `$ git cherry-pick [commit hash]`  
   Copy the deleted commit to current branch
6. Delete backup branch  
   _Follow steps 10 & 11 from [Common Workflow with Branches](#Common-Workflow-with-Branches))_

<br>
<br>

## Contributing to Open Source Projects

1. Fork the Project repository (from GitHub)
2. `$ git clone [forkedRepository]`  
   Clone the forked version of the project repository
3. `$ git remote add upstream [urlOfOriginalRepository]`  
   Add the original repository as an additional remote alongside the forked repository
4. `Add` and `Commit` changes to the cloned repository
5. `$ git pull upstream master`  
   Pull changes from the original repsository to the local cloned repository
6. `$ git push origin master`  
   Push changes to the master branch of the forked repository
7. Click **Pull Request** button in the forked repository to request changes to be pulled into the original repository

<br>
<br>

## Creating a Private Forked Repository

1. `$ git clone --bare [urlOfOrignalRepository]`  
   Create a temporary clone of the repository
2. Create a private repository (on Github)
3. `cd [directoryOfClonedRepository]`  
   Change directory to previously cloned directory
4. `$ git push --mirror [urlOfPrivateRepository]`  
   Push to newly created private respository using its url
5. `cd ..` `rm -rf [clonedRepository]`  
   Remove the temporary clone
6. `$ git clone [urlOfPrivateRepository]`
   Clone the private repository
7. `$ git remote add upstream [urlOfOriginalRepository]`  
   Set the original repository as a upstream remote to pull any future changes to the private repository  
   _To pull in future changes, use the command `$ git pull upstream [branch]`_
8. `$ git remote set-url --push upstream DISABLE`  
   Disable pushing to the original repository  
   _Instead, push to the private repository which has the remote name of "origin" by default by using `$ git push origin [branch]`_

<br>
<br>

## Manual Page

- `$ git help [command]`
- `$ git [command] --help`

<br>
<br>

## .gitignore

For excluding files from Version Control

1. Create a file named `.gitignore` in current directory
2. Enter the name of any files to be excluded from tracking in `.gitignore`

- `*.html` will ignore all files with html extension
