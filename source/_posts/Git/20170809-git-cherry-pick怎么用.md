---
title: git cherry-pick怎么用
tags:
  - git
  - cherry-pick怎么用
categories: git
abbrlink: 22302843
date: 2017-08-09 14:36:12
---

<!-- toc -->
<!-- more -->

# 1. git cherry-pick使用步骤

当需要把在调试分支修改的代码提交到主线分支时，需要使用cherry-pick操作

- 基于debug分支clone的git库，使用git log查看，先记录需要挑选的 `commit-id`；
- git remote update
- git checkout -b 【个人分支名】 remotes/origin/XXX_Int
- git cherry-pick commit-id1 commit-id2 …  （要push的commit-id，从旧到新）
- git push origin HEAD:refs/for/XXX_Int

注：由于cherry-pick合并到本地分支时可能出现冲突需要解决：
- 用`git status`检查冲突原因，根据git提示解决冲突;
- 并用`git add` 或者 `git rm` 让git知道冲突已解决;
- 冲突文件处理完毕后，用`git commit –c commit-id` 完成cherry-pick的提交，如果没有出现冲突，则不需要执行git commit –c 操作;
- 最后再进行push操作;
- 如果挑选的commit可以合并为一个commit提交，最好使用 `git reset --soft` 进行合并后再提交。

# 2. 详细介绍

`git cherry-pick`可以把某一个分支中的一个或几个commit(s)合并到另一个分支。
例如，假设我们有个稳定版本的分支，叫 master ，另外还有个开发版本的develop分支，我们不能直接把两个分支合并，这样会导致稳定版本混乱，但是又想增加一个开发分支develop中的功能到master中，这里就可以使用cherry-pick了,其实也就是对已经存在的commit 进行再次提交.

# 3. 简单用法

```
git cherry-pick <commit id>
```
在整个git仓库中，commit id 是唯一的，只需要记住你要合并的活动id,然后切换到要需要合入的分支执行命令就可以。
注意：当执行完 cherry-pick 以后，将会生成一个新的提交；这个新的提交的哈希值和原来的不同，但标识名一样，也就是信息等一样；

例如：

```bash
$ git checkout master
$ git cherry-pick 12345678  #这个 12345678  位于develop分支中，你也可以复制完整的Hash值
```

如果顺利，就会正常提交

# 4. 如果在cherry-pick 的过程中出现了冲突

就跟普通的冲突一样，手工解决：

看哪些文件出现冲突  `git status`
用编辑器打开文件编辑修改。

提交编辑的结果

```bash
git add  .
git commit
```

# 5. git cherry-pick 一整段的 commit

cherry-pick 的使用方法很簡單，加上 commit hash 就好了，如下：

```
git cherry-pick COMMIT_SHA1
```
也可以 cherry-pick 一整段的 commit：

```
git cherry-pick START_SHA1^..END_SHA1
```

# 6. 参考文献

[4. cherry-pick【教程3 改写提交！】| 猴子都能懂的GIT入门| 贝格乐（Backlog）](http://backlogtool.com/git-guide/cn/stepup/stepup7_4.html)
[git cherry-pick 使用指南](http://www.jianshu.com/p/08c3f1804b36)
[一个可以提高开发效率的 Git 命令-- Cherry-Pick - DiyCode](https://www.diycode.cc/topics/596)