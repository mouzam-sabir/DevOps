#  Basic Commands to make and connect a  Git repository (Locally to Remote)
---
- Create a Folder
- To make a GIT repository of the folder
```bash
git init
```
---
- Add a file with the name README.md
```bash
 echo  "LEARNING DEVOPS" > README.md
```
---
- Move file to the staging phase i-e For moving from local repostory to remote repository
```bash
git add README.md
```
---
- Add a comment on the changes
```bash
 git commit -m"I HAVE MADE THIS CHANGES"
```
---
- Connect the local repository with remote repostory
```bash
git remote add origin "https://github.com/username/repositoryname.git"
```
---
- New branch banao
```bash
 git branch -m main
```
---
- Changes push karo
```bash 
git push -u origin main
```
---
- To check the current branch
```bash 
git branch
```
---
- To add a new branch
```bash 
git checkout -b newbranchname
```
---

# IMPORTANT

- -u (LINK THE BRANCH WITH THE URL)
- -b (MAKE A NEW BRANCH)
- -m (MESSAGE)
- -M (FORCE BRANCH RENAME)
- checkout (SWITCH THE BRANCH)
