# fast-git

## GitFlow原理

整个代码库中一共有五种分支。
- Master 分支。也就是主干分支，用作发布环境，上面的每一次提交都是可以发布的。
- Feature 分支。也就是功能分支，用于开发功能，其对应的是开发环境。
- Developer 分支。是开发分支，一旦功能开发完成，就向 Developer 分支合并，合并完成后，删除功能分支。这个分支对应的是集成测试环境。
- Release 分支。当 Developer 分支测试达到可以发布状态时，开出一个 Release 分支来，然后做发布前的准备工作。这个分支对应的是预发环境。
之所以需要这个 Release 分支，是我们的开发可以继续向前，不会因为要发布而被 block 住而不能提交。一旦 Release 分支上的代码达到可以上线的状态， 
那么需要把 Release 分支向 Master 分支和 Developer 分支同时合并，以保证代码的一致性。然后再把 Release 分支删除掉。
- Hotfix 分支。是用于处理生产线上代码的 Bug-fix，每个线上代码的 Bug-fix 都需要开一个 Hotfix 分支，完成后，向 Developer 分支和 Master 分支上合并。
合并完成后，删除 Hotfix 分支。这就是整个 GitFlow 协同工作流的工作过程。我们可以看到：我们需要长期维护 Master 和 Developer 两个分支。
其中的方式还是有一定复杂度的，尤其是 Release 和 Hotfix 分支需要同时向两个分支作合并。所以，如果没有一个好的工具来支撑的话，
这会因为我们可能会忘了做一些操作而导致代码不一致。

### git stash

将未完成的操作先保存起来，等处理完事情之后，再`git pop/apply stash`

- pop: 删除stash记录
- apply: 保存stash记录

`git stash list` 查看stash列表

### git cherry-pick

挑选其他的commit到本分支上

`git cherry-pick CommitHASH`

### git rebase

合并分支，通常在还没有push出现但感觉有点乱的commit


### git squash

将多个commit合并为一个commit

```shell
pick c4bc5b4 add dog 2
pick ee97b1f add dog 1
pick 56b5270 add cat 2
pick 2b4e590 add cat 1
     2b4e123
```

`git rebase -i 2b4e123`

```shell
pick c4bc5b4 add dog 2
squash ee97b1f add dog 1
pick 56b5270 add cat 2
squash 2b4e590 add cat 1
     2b4e123
```

将前两个commit合并为一个，将后两个commit合并为一个

### git merge --no-ff

只有 feature 合并到 developer 分支时，使用–no-ff 参数，其他的合并都不使用--no-ff参数来做合并

## 参考资料

- [https://time.geekbang.org/column/article/2440](https://time.geekbang.org/column/article/2440)