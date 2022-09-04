# Git

分布式：

Git是分布式版本控制系统，同一个Git仓库，可以分布到不同的机器上。首先找一台电脑充当服务器的角色，每天24小时开机，其他每个人都从这个“服务器“仓库克隆一份到自己的电脑上，并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交。可以自已搭建这台服务器，也可以使用GitHub网站。

git config --gloabl user.name  'name'

git config -l 

git add file.txt

git status 

git commit -m '注释'

git status 

git diff file.txt  文件是否修改

## 1：版本回退

git log

git log --pretty=online

git reset --hard HEAD^     # HEAD^^..

git reset --hard HEAD~50 

恢复日志： git reflog

git reset --hard 版本号 

## 2：理解工作区与暂存区的区别

工作区：

就是你在电脑上看到的目录，比如目录下git里的文件(.git隐藏目录版本库除外 )或者以后需要再新建的目录文件等等都属于工作区范畴

版本库(Repository)：

工作区有一个隐藏目录.git,这个不属于工作区，这是版本库。其中版本库里面存了很多东西，其中最重要的就是stage(暂存区)，还有Git为我们自动创建了第一个分支master,以及指向master的一个指针HEAD

第一步：是使用 git add 把文件添加进去，实际上就是把文件添加到暂存区。

第二步：使用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支上。

git checkout -- readme.txt  # 丢弃修改文件内容  # 如果放入暂存区，撤销不行

rm  file.txt     #删除文件

git checkout -- file.txt   #恢复删除的文件

## 3：远程仓库

　git ls-remote origin

ssh-keygen -t rsa –C “youremail@example.com”,

在github 创建ssh 

```
git remote add origin https://github.com/m168168/demo_01.git
```

ssh-agent bash

ssh-add id_rsa

git clone [url]

git remote -v

git push [origin] [master]

```
git remote set-url origin https://github.com/username/repository.git
```

## 4:     分支



git branch 

git branch branch_name

git checkout branch_name # 切换分支

git branch -d branch)name # 删除分支

git branch -b branch_name # 建立一个分支，且切换到该分支

分支冲突

## 5： 系统版本号管理

git tag

git tag v1.0.0

git show version 

## 6: 设置别名

git config --global  alias.[name] [command_name]



## 7-Note 搭建

1： 配置系统文件

git config --global user.name "刚在Github上面注册的用户名"

git config --global user.email "刚在Github上面注册的邮箱"

2： 生成秘钥 在users/Mrwang/.ssh 文件夹下

ssh-keygen -t rsa -C "xxxxx@xxxxx.com" 其中-t指定密钥类型，这里设置rsa即可，-c是密钥的注释 这里我为了便于辨识所以使用了邮箱，

3: 在github 上添加公钥

4： 在github 上 Setting/Developer setting / Personal access token/ 

5： 本地创建一个文件夹 note

git init

git add .

git commit -m ' commet'

git branch -M C++ 

 git remote add origin https://github.com/m168168/Note_Alg_C.git

git push -u origin C++

## 8: 贡献其他项目

1： 将要贡献的项目fork 到自己账号下

2： git clone + 地址

3： 在本地对项目进行修改，不再master分支上直接修改，创建dev分支，修改完成后，再将dev分支merge 到master分支

git checkout -b dev

4: 修改完成，切换到master分支，

git checkout master

5: 合并分支

git merge dev

6:  git push 同步到自己github仓库中

git push















