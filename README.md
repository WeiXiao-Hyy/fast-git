# fast-git

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
