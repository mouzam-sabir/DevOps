#  Basic Git Commands 
---
# Setup
- Tell Username to git (One-time)
```bash 
git config --global user.name "name"
```
- Tell email to git (One-time)
```bash 
git config --global user.email "email"
```
- Enable Colorful Output (Not compulsory)
```bash 
git config --global color.ui auto
```
---
# Make a Repository
- Create a Folder and make a GIT repository of the folder
```bash
git init
```
- Clone a Exisiting GitHub repo
```bash
git clone "https://github.com/username/repo.git"
```
---
# Basic Stage and Commit
- Add a file
```bash
 echo  "LEARNING DEVOPS" > filename.md
```
- Move file to the staging phase i-e For moving from local repository to remote repository
```bash
git add filename
```
- All files staging using one command
```bash 
git add .
```
- Check Status (Changes, File tracking)
```bash 
git status
```
- Unstage a file
```bash 
git reset filename
```
- View Unstage Changes 
```bash 
git diff
```
- What Exactly Added (To Differentiate the changes)
```bash 
git diff --staged
```
- Add a comment on the changes
```bash
 git commit -m "I HAVE MADE THIS CHANGES"
```
- Check details of Commit
```bash 
git log
```
---
# Branching
- Branches List and to check current branch
```bash 
git branch
```
- Make a new branch
```bash 
git branch newbranch
```
- Switch to another branch
```bash 
git checkout newbranch
```
- Make a new branch and switch to it
```bash 
git checkout -b newbranch
```
- Branch rename (First move to that specific branch)
```bash 
git branch -M main
```
- Delete a Branch
```bash 
git branch -d branchtodel
```
- Delete a Branch from remote repo
```bash 
git push origin --delete branchtodel
```
---
# Merge, Rebase, Squash, Cherrypick (Mainly for Commits)
- Connect branches (Old commit history rehti hai, or ek new banti hai)
```bash
git merge branch
```
- Connect branches (Old Commit history replaced with the new one)
```bash
 git rebase branch
```
- Connect branches (Commits history edit/reorder)
```bash 
git rebase -i HEAD~n
```
- Pick specific commit from another branch
```bash 
git cherry -pich SHA
```
---
# Remote GitHub Connection
- Connecting a local repo with remote repo
```bash 
git remote add origin "url"
```
- Checking and Verifying connected repo Url
```bash 
git remote -v
```
- Changing remote repo Url
```bash 
git remote set-url origin "url"
```
- Push local commits to remote repo
```bash 
git push origin branchname
```
- Fetching Remote repo and merging with local repo 
```bash 
git pull
```
- Merging specific branch
```bash 
git pull origin branchname
```
- Download Remote Repo into local system
```bash 
git fetch origin "url"
```
- Merging remote repo with local
```bash 
git merge origin/branchname
```
---

# IMPORTANT

- -u (LINK THE BRANCH WITH THE URL)
- -b (MAKE A NEW BRANCH)
- -m (MESSAGE)
- -M (FORCE BRANCH RENAME)
- checkout (SWITCH THE BRANCH)
- ">" (Overwrite)
- ">>" (Append)
