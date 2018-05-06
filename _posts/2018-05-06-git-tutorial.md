---
layout:     post
title:      "Git的基础使用"
subtitle:   ""
date:       2018-05-06 12:00:00
author:     "Popo"
header-img: "img/bg/bg_xingkong5.jpg"
tags:
    - 工作
---


### 默认信息设置
```
git config --global user.name 用户名
git config --global user.email 邮件
```

### 指令
##### git init [指定的目录名称]
初始化本地仓库
初始化当前目录为git本地仓库：`git init`
初始化指定目录为git本地仓库：`git init config`

##### git status [-s]
查看改动信息

##### git diff
详细查看当前的改动信息
尚未缓存的改动:`git diff`
查看已缓存的改动:`git diff --cached`
查看已缓存的与未缓存的所有改动:`git diff HEAD`
显示改动的位置:`git diff --stat`

##### git add <文件夹|文件筛选格式>
缓存改动到版本控制
把当前目录下所有改动加到缓存：`git add .`
把指定格式文件改动加到缓存：`git add *.c`
把指定文件的改动加到缓存：`git add README`

##### git rm
简单删除文件：`git rm 文件名称`
删除已经添加到缓存的文件：`git rm -f 文件名称`
只想删除文件的改动的缓存信息：`git rm --cached 文件名称`

##### git mv [旧的的文件名|旧的目录名] [新的文件名|新的目录名]
移动和重命名一个文件、目录

##### git commit -m <日志>
提交改动缓存到本地仓库:`git commit -m "测试git"`

##### git clone <仓库路径> [指定的路径]
从git仓库中拷贝项目到当前目录：`git clone https://github.com/linchunbogit/testgit.git`
从git仓库中拷贝项目到指定目录：`git clone https://github.com/linchunbogit/testgit.git testDir`

##### git reset
清除当前改动的缓存：`git reset HEAD`
切换到前一个版本：`git reset --hard HEAD^`
切换到前100个版本：`git reset --hard HEAD~100`
切换到指定的版本：`git reset --hard 版本号`

##### git branch
列出所有分支：`git branch`
创建分支：`git branch 分支名`
删除分支：`git branch -d 分支名`

##### git checkout
分支切换
切换到指定分支：`git branch 已经存在的分支名称`
创建切切换到分支：`git branch -b 不存在的分支名`

##### git merge
分支合并
把指定分支合并到当前分支上：`git merge 分支名称`

##### git log
查看提交日志：`git log`
查看前几个日志：`git log -数量`
简洁的方式查看日志：`git log --oneline`
拓扑图形式查看日志：`git log --graph`
查看指定用户的提交日志：`git log --author=用户名`
查看指定日期的提交日志：`git log --oneline --before={3.weeks.ago} --after={2010-04-18}`
查看日志的标签：`git log --decorate`

##### git tag
查看说有的标签：`git tag`
给版本上标签：`git tag -a v1.0`
给老版本追加标签：`git tag -a v1.2 版本号`
给标签加信息：`git tag -a 标签名称 -m 信息`

### 冲突处理
把有冲突的文件的中所有 <<<<<<<HEAD 和 >>>>>>> ????的内容处理就好，然后把这个区间符删除就可以了








