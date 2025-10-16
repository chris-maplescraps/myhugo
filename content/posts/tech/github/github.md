+++
title = 'Github'
date = 2025-10-14T19:43:39+08:00
draft = false
slug = "81f9b3e"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Github

## Github 安装
> Github 是基于云的代码托管平台，它使用 Git 进行版本控制，帮助开发者存储、管理和共享代码
> - 下载 + 安装 [点击此链接](https://git-scm.com/downloads)

> [!NOTE]+ **Github 流程** :
>
>> **工作区 (Working Directory)**
>> - 位置： 就是你打开的那个 **项目文件夹**。你看到的所有文件，包括代码、图片、配置文件等等，都属于工作区
>> - 状态： 当你在文件中进行修改时，这些修改都处于“未追踪”或“已修改”状态
> 
>> **暂存区 (Staging Area / Index)**
>> - 位置： 在项目根目录下的 **隐藏文件夹 .git/** 中的一个 **名为 index 的文件**
>> - 功能： 它充当工作区和储存区之间的“缓冲站”。你使用 *git add* 命令将工作区中你想要的修改精准地加入暂存区。只有被加入到暂存区的修改，才会包含在你的下一个 commit 中
>
>> **储存区 (Local Repository / Git Directory)**
>> - 位置： 也是在项目 **根目录下的隐藏文件夹 .git/** 中，主要内容 **存储在 .git/objects** 文件夹里
>> - 功能： 这是 Git 的核心数据库。当你执行 *git commit* 时，暂存区中的快照会被永久地记录为历史版本，并存储在储存区中

## *工作区 ( Working Directory ) 常用命令*

> - git clone `< http.git > own_directory`
> - git clone `-`b `< branch > < repo_url >`
> - git clone `-`b develope --single-branch <你的仓库URL>
> - git add `< files >` 将文件保存到暂存区
> - git log `--`stat 显示提交后的信息
> - git log `-`p `-`2 显示最新两个log信息
> - git log `-`2 显示最新两个log信息
> - git log `--`graph `--`oneline 以图线和一行显示
> - git tag v1.0.0 创建标签
> - git commit `-`m 将暂存区文件提交到储存区
> - git checkout `< branch >` 如果本地没有该分支，会自动创建并跟踪对应的远程分支
> - git restore `< files >` 撤销已经追踪/提交过，但是在工作区的文件
> - git stash 需要保存修改但不想提交时
> - git stash save "Solving login page issue" 添加一个描述，方便以后查找
> - git stash list 查看储存多个列表
> - git stash pop 恢复最近一次的储藏，并从列表中移除它
> - git stash apply stash@{1} 恢复指定的储藏，但保留它在列表中以备后用
> - git stash drop stash@{0} 使用索引是你出指定的记录
> - git stash clear 一次性删除所有的git stash记录
> - git config --global --add safe.directory 拷贝到其他设备，需要在新设备添加此配置
> - git clean `< file_name >` `-`f 可以删除新创建但不曾提交过的文件
> - git clean `-`n `--`dry-run 模拟删除不曾提交/追踪过的文件
> - git clean `< folder_name >` `-`nd 模拟删除不曾提交/追踪过的文件夹
> - git clean `< folder_name >` `-`fd 确认删除文件夹

## *暂存区 ( Staging Area ) 常用命令*

> - git add `-`p 显示确认窗口
> - git diff `--`staged 显示暂存区最后一次状态
> - git diff 比较工作文件 和 暂存区文件的差异
> - git diff `<commit1>` `<commit2>` 比较2个提交的差异
> - git diff `--`cached 查看已经 git add 但未提交的更改
> - git diff `<commit>` HEAD 查看指定提交和当前分支最新提交的差异
> - git diff `<commit>` 显示该提交与当前工作区的差异
> - git reset  HEAD `< changed_file >` 从暂存区移除，也会丢失硬盘上的文件
> - git restore `--`staged `< changed_file >` 只从暂存区移除

## *储存区 ( Local Repository ) 常用命令*

> - git rm 删除在储存区的文件
> - git mv 重命名在储存区的文件
> - git commit `-`a `-`m 将文件提交到储存区，跳过暂存区
> - git commit `--`amend 修改提交后的错误信息，或者遗漏添加文件（会替换原本的 commit，然后重新创建生成SHA）不建议在多人协作的共享分支上使用
> - git revert HEAD 不删除提交，而是生成一个“相反”的提交，
把更改抵消掉，然后再执行git push origin将这个撤销再次提交到远程仓库
> - git revert `< commit ID >`
> - git reset `--`soft HEAD~1 删除最后一次提交但保留修改
> - git reset `--`hard HEAD~1 撤销最后一次的提交后，删除工作和暂存区后期的修改
使用 git push `--`force-with-lease origin `<sub-branch>`
>> Parameters :
>> - `--`soft	只移动 HEAD 指针，更改保留在暂存区
>> - `--`mixed	移动 HEAD 指针，撤销 commit，也会撤销暂存区的文件。这是 git reset 的默认选项
>> - `--`hard	移动 HEAD 指针，清空暂存区和工作区。所有更改都被丢弃。这是最危险的选项
>> 

## *分支 ( Branch ) 常用命令*

> - git branch 显示分支列表
> - git branch  `< new-branch >` 创建新分支
> - git branch `-`d `< current-branch >` 删除某个分支，包括master/main分支？
> - git branch `-`D `< current-branch >` 强制删除某个分支
> - git checkout `-`b `< new-branch >` 创建新分支，然后指针到新分支
> - git checkout `< other-branch >` 指针到存在的分支，也自动对应到远程分支
> > - git merge `--`abort 用于merge conflict，取消合并
>> 使用 git branch `-`vv 可以看到以下讯息：指针的分支，是否和远程仓库分支一样 
>> 
>> 		test   5ab7ba3 [origin/test] Create a new file for result record purpose
>
>> - git merge 将主分支 <---- 其他分支进行文件合并
>> 
>>  	`git chekout main/master`
>>  
>> 		`git merge [ sub-branches ]`

## *远程仓库 ( Remote Repository ) 常用命令*

> - git clone 克隆github远程储存库某个项目到本地
> - git pull 从远程储存库更新 ( git fetch )+ 合并 ( git merge )到本地目录
> - git push origin main从本地的快照上传文件到远程储存库 ( 新分支在执行推送到远程仓库，会自动创建 )
> - git remote `-`v 
> - git remote show origin 显示当前连接的远程仓库
> - git remote add origin `< git@github.com:you/project.git >` 添加远程仓库 （ 属于自己的远程仓库 ）
> - git remote add upstream `< http://github.com/[git-username] >` 添加上游 （ fork别人的github仓库 ）
> - git remote set-url origin `< git@github.com:you/project.git >` 修改远程地址
> - git remote remove origin 删除远程仓库连接
> - git branch `-`a 显示本地 和 远程分支
> - git branch `-`r  只显示远程分支
> - git branch `-`M main 将当前分支的名称强制重命名为 main ( 用于远程空仓库，第一次在本地提交到远程仓库， 因为在本地git init 默认是master )
> 
> - git fetch 将远程仓库别人更新的提交，复制到本地远程分支，就可以看到别人提交什么，但不会合并
          * git log origin/main 查看main分支最新的状态
          * git log origin/main --online --graph 以树状显示分支状态
> - git fetch origin optimize:optimize 本地没有该远程分支，可以直接把它 origin/optimize 拉到本地 optimize 并切换过去
git remote update 获取远程分支所有的内容，但不会自动合并到本地分支

> - git push `-`u origin < 分支名 > 将本地< 分支名 >分支推送代码到origin 远程仓库, -u 默认为当前的远程仓库
> - git push `--`set-upstream origin 等于 git push -u origin < branch >
> - git push `--`delete origin < 远程仓库分支 >  删除远程分支
> - git pull `--`rebase origin main 将其他同事推送更新，同步到本地，然后将自己的新推送放在最后
> - git rebase `--`continue 
> - git merge origin/master
> - git log origin/master
> git rebase `--`continue 
> 
>> - git rebase < target-branch > 把我在其他分支提交，重新放在 main/master 后面继续排队走
>>
>> ```markdown
>> [ 真实环境例子 ]
>> main:          A --- B --- C --- F
>>                             \
>> feature:                     D  --- E <--- 我拉的分支
>>
>>```
>>```markdown
>> [ 使用 git rebase ]
>> main:          A --- B --- C --- F
>>                                   \
>> feature:                           D  --- E <--- 将我分支所有提交排在main最后继续开发
>> ```

> [!NOTE] 其他：
>> Pull request =  
> 
>> Code review :  
>> 	`git commit -a --amend`  
>> 	`git push -f`  
>
>> Issue tracker = 
