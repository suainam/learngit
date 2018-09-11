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

#### Force Delete feature branch
- before merge to master, delete branch
```bash
git branch -D feature1
```
- "-D" needed

#### 多人协作
+ 查看远程库的信息
```bash
git remote # 简略的信息
git remote -v # 详细的信息
# origin git@github.com:username/learngit.git(fetch)
# origin git@github.com:username/learngit.git(push)
```
+ 推送分支
```bash
git push origin master
git push origin dev # 推送其他分支
# master 是主分支，要时刻与远程同步
# dev 是开发分支，所有的成员都需要在上面工作，要时刻与远程同步
# bug 是用于在本地修复bug，没必要推到远程
# feature是否推到远程，取决于你是否和你的团队成员合作在上面开发
```
+ 抓取分支
```bash
# 多人协作是，大家都会往master和dev分支上推送各自的修改
# 模拟另外一个人克隆和提交
git clone git@github.com:username/learngit.git
git branch 
# master
# 需要在dev分支上面开发，在本地创建dev
git checkout -b dev origin/dev
# vim file and add, commit
# git push origin dev
# at this moment, you modify the file modified by others
# vim file and add, commit, push will be rejected
git pull
# no tracking information, 本地分支和远程分支的链接关系没有创建，使用以下命令进行创建
git branch --set-upstream-to=origin/dev dev
```
+ 多人协作的工作模式
	+ 首先，用 git push origin <branch-name>推送自己的修改
	+ if false，git pull and try merge
	+ if merge false, then fix conflict, and add then commit
	+ push them when conflict is solved

#### Rebase
```bash
+ git rebase
# 只对尚未推送或分享给别人的本地修改执行变基操作清除历史，从不对已推送至别处的提交执行变基操作
```

#### 标签管理
+ 切换到需要打标签的分支上，以master为例
	+ 'git tag <tag name>'，打标签，默认是在HEAD上，也可以根据commit id来打标签
	+ 'git tag' 可以查看所有标签
	+ 'git log --graph --pretty=oneline --abbrev-commit', 可以查看历史提交的图形化界面，然后根据commit id来打标签。'git tag v0.9 f52c633'
	+ 标签默认按照字母排序
	+ 'git tag -a v0.1 -m "version 0.1 release" 1094adb'，可以使用'-a'来指定变签名，'-m'指定说明文字
	+ 'git show <tagname>' eg.'git show v0.9'，可以查看标签信息
+ 操作标签
	+ 推送某个标签到远程，'git push origin v1.0' | 'git push origin --tags'，可以推送1个或一次性推送尚未推送的本地标签
	+ 在本地删除标签，'git tag -d v0.1'。创建的标签都只存储在本地，不会自动推送到远程，因此打错的标签可以再本地安全删除
	+ 删除已推送的远程标签，首先在本地删除，'git tag -d v0.9', 'git push origin :refs/tags/v0.9', 然后可以通过登录github查看是否已经删除

#### github
+ 在github上面，可以fork任意的开源仓库
+ 自己拥有fork后的仓库，有读写的权限
+ 可以推送pull request 给官方的仓库来贡献代码

#### use gitee
+ 'git remote -v'，查看远程库的信息
+ 'git remote rm [origin]',[origin]替换成远程库的名字，来删除关联
+ 'git remote add github git@github.com:suainam/learngit.git', 'git remote add gitee git@gitee.com:suainam/learngit.git', 进行多个远程库的关联
+ 'git push [name] master', 推送master到[name]

#### git config
+ 'git config --global color.ui true', 让命令输出更醒目
+ .gitignore文件，可以帮助我们忽略文件，以免每次add的时候，都会显示Untracked files。Github也有现成的各种配置文件，在线：https://github.com/github/gitignore
	+ 忽略的规则一般是：
		+ 忽略操作系统自动生成的文件，比如windows下面的缩略图等
		+ 忽略编译生成的中间文件、可执行文件。也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如java编译产生的.class文件
		+ 忽略自己的带有敏感信息的配置文件，比如存放口令的配置文件 
	+ 如果想要添加文件到stage，如果是忽略的，需要使用'git add -f filename'
		+ 如果错误忽略了，.gitignore写的有问题，通过'git check-ignore'来检查
+ .gitignore需要放到版本库里，并且可以对ignore进行版本管理

#### 配置别名
```bash
git config --glboal alias.st status
#status as st
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
#global
git config --global alias.unstage 'reset HEAD'
git config --global alias.last 'log -1'

git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```
+ 配置文件
	+ global是对当前用户的，当前用户的配置文件在用户主目录下：.gitconfig
	+ 如果不加global，就是针对当前的仓库的，每个仓库的git配置文件都放在：.git/config 

