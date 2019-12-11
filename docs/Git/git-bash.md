# git 常用操作

## git重命名分支
例如我在master分支，要把dev4命名为dev4.0
```bash
# 切换到dev4分支
$ git checkout dev4
# 重命名
$ git branch -m dev4 dev4.0
# 删除远程分支
$ git push origin :dev4
# 将重命名过的分支提交
$ git push origin dev4.0
# 更新本地,绑定远程分支
$ git branch --unset-upstream
```