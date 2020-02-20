

# git 团队开发流程规范

## 分支命名规则

1. 主分支：master
2. 开发分支：developer
3. 功能分支：feature - 分支名称
4. 分支发布：release - 版本号
5. bug 分支修复：bugfix - 版本号

## 操作步骤

管理员「项目负责人」创建 git 仓库，建立 developer 分支

```
git branch develop 
git push -u origin develop
```

项目成员「开发者」clone 项目，在本地建立自己功能分支

```
git clone 项目 git 地址 
git checkout -b develop origin/develop

创建本地功能分支
git checkout -b feature-[name-desc] develop
```

在自、己的分支上进行开发 ： `git add` ，`git commit` 等，push到功能分支上。

功能完成后可以直接合并本地的 developer 分支后 push 到远程仓库，合并的时候很大几率发生冲突，此时需要 merge ，merge的时候确保不影响项目其他成员，如果多个人都操作了同一个类，最好当面确认后在进行修改。等合并完成确认无误后，删除本地开发分支

```
git checkout develop 

git pull origin develop //确保本地 developer 分支为最新的

git merge feature-[name-desc] 

git push 

git branch -d feature-[name-desc] //删除本地分支
```

发布分支

![](/home/devilper/Desktop/systemctl status.png)

```
git checkout -b release-0.1 develop

一旦准备好了发版，合并修改到 master 分支和 developer 分支上，删除发布分支

合并修改到 master 分支
git checkout master 
git merge release-0.1 
git push 

合并修改到 developer 分支
git checkout develop 
git merge release-0.1 
git push 

删除发布分支
git branch -d release-0.1
```

为 master 分支打发版 tag

```
git checkout master 
git tag -a 0.1 -m "Initial public release" master 
git push --tags
```

bug 修复分支，如果正在开发功能的同时，developer 上发现了线上 bug，或者未上线的 bug，我们可以开一个 bugfix 分支来修复 bug

```
git checkout -b bugfix-#001(bug 分支名称) master（或 developer）

/***  去修 bug 吧 */
....
/***  修复完成 */
git checkout master  
git merge bugfix-#001 

git push 
git branch -d bugfix-#001
```