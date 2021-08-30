---
layout: post
title: 记一次git使用undo commit指令
date: 2020-08-02 01:15:40 +08:00
categories: [Git]
---

## 记一次git使用undo commit指令

### 起因

>  因漏提交了代码，想撤回提交内容，重新提交，所以使用了``undo commit`` 指令，当我执行完后，看到提交记录已经消失，顿感满足，然而仔细一👀代码，发现了一丝不对劲，握草，这不是修改之前的代码吗！！代码不见了还得了，肯定不愿意再重写一遍！

### 寻找方法

百度搜索 ``undo commit操作之后代码消失``，果然找到了有人遇见过类似的情况，

1. 首先是文件[History]( https://www.jianshu.com/p/6eb31304fbf3 )，但是我这依然看不到记录。此方法失败

2. 然后是解决我遇见问题的

   **使用git的指令重置工作树**，[这里]( https://www.jianshu.com/p/5b3166c855b2 )

### 解决问题

```shell
git reflog
```

首先使用 **``git reflog ``** 查询变更记录，会看到一堆![这样](/assets/img/git-about-undo-commit.png)

类似这样的日志，

接着使用 ``git reset``指令重置代码状态

推荐使用``--soft``参数，[官方文档]( https://git-scm.com/docs/git-reset#Documentation/git-reset.txt---mixed ) 说这个会将代码重置到指定的版本，但不重置工作树，也就是恢复代码到已修改但未提交的时候。

我使用的是``--soft`` 参数，将工作区全部文件恢复到指定版本的状态，并且后续错误提交的修改后的代码，会保留下来

### 恢复的指令

```shell
git reset --soft HEAD@{7}
```

``soft``可换成``mixed``，或其它参数。hard为不保留任何修改的代码，仅恢复到指定版本

``HEAD@{7}``距离Head多少个版本之前。具体多少个版本，由数字指定

然后，执行`git reset`后，`reflog`记录也会更新，并且最新的依然是0，之前的1会递增为2，以此类推，
