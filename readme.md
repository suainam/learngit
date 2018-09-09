#### install git
- Linux
    sudo apt-get install git
- windows
      - dowload git from 'https://git-scm.com/downloads'
      - start menu, 'git' -> 'git bash', if open success, then git installed.
#### git config
```bash
git config --global user.name 'Your Name'
git config --global user.email 'email@example.com'
# global, you can also 
```
#### create repository
```bash
mkdir file  | cd file # your current file is also ok
git init # inint this file to be your repository, a file named '.git' will be created
```
#### writting your file in your files
#### add and commit
```bash 
git add file
git commit -m "wrot a readme file and so on"
# you can add many file, and commit them to your repository in one time
```
#### git status
```bash
git status # the status of repository
git diff file # list the difference between new file and old file
```
#### git log
```bash
# git add and git commit will store every changes, and git log will store the changes' infomation
git log --pretty=online # will show log in line 
```
#### rollbach to last  or new distribute
```bash
# ^ in cmd will be "\", should use "^^" or "~1" to replace
git reset --hard HEAD^^ 
#last of last, user 'HEAD^^', many ago, 'HEAD~100' and so on
cat file 
#see what had happened

git rest --hard 1094a 
# this is commit id, the new distribute

git reflog 
# with this you can find you every comd, commit id is also in it
```
#### work place and repostiory
- learngit is my work place
- git add, can add my file, for example, readme.md, to .git/stage[index]
- git commit, can add the files in stage to current branch (eg. master)
- **git will only commit the files in stage, if you modify you file after git add, you use commit will only commit the last distribute, not the newest modify**
- **git manage the changes, not the files**

#### how to discard the changes
1. before in stage, use "git checkout -- filename" to discard the changes in work place
2. in stage, use " git reset HEAD filename" to unstage the file, and use step 1 
3. if you had commit the changes to your computer repostiory, you need use " git reset --hard HEAD~1" to rollback

#### remove the files
1. "git add file", in workplace, you "rm test.txt", and git will know it, you nedd "git rm test.txt", and "git commit -m "remove file"
2. after you remove the file, you regret to do it. you need "git checkout -- file" to replace the file in workplace(evenif it's empty)

#### github
- create sshkey
    - in user profiles, find ".ssh" and "id_rsa id_ras.pub" in it, if not exists:
    	- ssh-keygen -t rsa -C "youremail@gmail.com"
		- just press enter is ok
	- "id_rsa.pub" is public
    - login github, "account setting", "ssh keys", "add ssh key", copy the content of "id_rsa.pub"
and paste it here
    
#### remote origin
```bash
# create your repository on github, eg. learngit
git remote add orgin git@github.com:yourusername/learngit.git
git push  -u origin master
# when you first push, "-u" will bulid a realtionships between master on your desktop and origin, it need'tafter 
git clone git@github.com:yourusername/learngit.git
#clone from origin. git@github.com is git://, use ssh, https:// is also useful, but maybe slowly.
```

#### branch
```bash
git checkout -b dev 
# create dev branch and checkout
# git branch dev, git checkout dev
git branch 
# *dev, master

# vim a new file, and add it to stage, then commit it. 
git checkout master
git merge dev
# switched to branch master, and merge dev

git branch -d dev
# after merged, delete dev
```
#### resolve conflict
- if modify the same file, add, commit and then merge will be false
- modify it before merge

#### --no-ff
- default, Fast forward will effect, and the branch info will be lost
```bash
git checkout -b dev
# vim license.txt, add, commit
git checkout master
git merge --no-ff -m "merge with no-ff" dev
# with new commit, "-m" is needed
git log --graph --pretty=oneline --abbrev-commit
```

#### bug branch
- git stash can store the status of your current workplace
- which branch's bug, and create new branch form it
```bash
git status 
# current work needs to be stored
git stash
# stored
git status 
# it's clear
git checkout master
git checkout -b issue-01
# eg. The bug is in master's
# fix the bug, then add and commit it
git checkout master
git merge --no-f -m "merge bug fix 01" issue-01
# bug fixed, have to do the job

git checkout test
git status
# it's clear
git stash list
# it's here
git stash apply @{}
git stash drop @{}
or
git stash pop
# this will apply and drop
# git stash list will be empty
```

