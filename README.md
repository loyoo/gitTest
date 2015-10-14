# gitTest
本项目用于git相关操作的测试.

常用命令收集:[wiki](https://github.com/loyoo/gitTest/wiki)

##git的主要特点:
* 本地提交
* 轻量级分支
* 高度灵活

## 主要概念
### 仓库 repository
### 用户 user
### 工作区域
* 工作区 working directory
* 缓存区 stage/index
* 本地版本库 commit/HEAD
* 远端库 remote

### 基本简单流程
* 新建repo
  * clone
  * fork
  * init

* 提交commit
  * git status
  * git add -A
  * git commit -m 'info'

### 远端操作
  * git remote -v 查看远端URL
  * git remote add/remove \<URL\> 添加/删除远端的URL
  * git pull = git fetch + git merge 注意是合并到当前分支
  * git fetch 在不确定情况下使用,可以在merge前进行比较
  * git remote add **upstream** \<URL\> 添加远端的主干
  * git fetch upstream 抓取远端主干代码到本地
  * git merge upstream/master 合并主干代码到本地
  * git branch --set-upstream \<branch-name\> origin/\<branch-name\> 建立本地分支和远程分支的关联

* 回滚
  * 在add之前恢复某文件: git checkout -- \<filename\>  注意在commit前可能会有多次add,此命令仅能恢复到最近一次add后的状态
  * 在commit后回滚版本: git reset –hard \<id\>/HEAD^  回滚到某一head/上一个head
  * 撤消某次commit: git revert HEAD 注意是将需要revert的版本的内容再反向修改回去,这是一次新的提交,不影响之前提交内容

## 结合github的项目流程
### 项目初始化
  * 需求
  * mileStone
  * 原型
  * 任务分配,issues
  * fork

### 流程
  1. fork项目
  2. git init,增加.ignore文件
  3. 设置个人的上游URL: git remote add origin \<URL\>
  4. 获取需要开发的远程分支:git fetch origin dev:dev , git checkout dev
  5. 开启新的功能分支f1开发,测试,commit: git checkout -b f1
  3. 设置主干的上游URL: git remote add upstream \<URL\> (loyoo)
  6. 在开发过程中保持与dev主干同步: git pull --rebase upstream dev
  7. 在开发过程中随时推送f1到远端保存: git push origin f1
  8. 功能分支f1开发结束,回到dev: git checkout dev , git merge f1
  8. 如果需要,可删除本地f1分支及远端分支:  git branch -d f1 (删除本地) , git push --delete origin f1 (删除远端f1)
  10. 功能正式结束后,push到服务端:git checkout dev , git push origin dev //在push前同步(后期再说,暂不操作):git fetch upstream dev , git rebase -i upstream/dev (清理dev分支的commits),
  11. 在github页面在dev分支提交pull request到主项目

### 分支
  * git branch 查看分支
  * git checkout \<branch1\> 切换到分支
  * git checkout -b \<branch1\> 新建并切换到**本地**分支, 此命令等同于:git branch \<branch1\> (创建) 加上 git checkout \<branch1\> (切换)
  * git checkout -b \<branch1\> origin/\<branch1\> 将远端的branch1分支抓取并切换过去
  * git branch -d \<branch1\> 删除**本地**分支
  * git push origin \<branch1\> 提交到**远程**分支
  * git pull origin \<branch1\> 拉取到**远程**分支
  * git merge \<branch1\> 合并分支
  * git diff \<source_branch\> \<target_branch\> 比较分支

### dev分支开发
  * 所有的开发先在该功能的dev分支完成
  * 每解决一个问题/完成一个功能 进行一次commit
  * 注意git reset的灵活使用 --hard/--soft/--mixed...,在远端与本地之间处理版本

### 集成与合并
  * 集成测试
  * 合并

## 常用
  * git status 查看状态
  * git reflog/log 获取commit的head id


