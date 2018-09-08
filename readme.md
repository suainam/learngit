#### install git
- Linux
    sudo apt-get install git
- windows
    dowload git from 'https://git-scm.com/downloads'
    start menu, 'git' -> 'git bash', if open success, then git installed.
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
#### to last  or new distribute
```bash
git reset --hard HEAD^ #last of last, user 'HEAD^^', many ago, 'HEAD~100' and so on
cat file #see what had happened

git rest --hard 1094a # this is commit id, the new distribute

git reflog # with this you can find you every comd, commit id is also in it
```
#### work place and repostiory
- learngit is my work place
- git add, can add my file, for example, readme.md, to .git/stage[index]
- git commit, can add the files in stage to current branch (eg. master)




