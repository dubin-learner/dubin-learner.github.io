# Git常见使用技巧

推荐git相关的书籍：

[Pro Git](http://git-scm.com/book/zh/v2)：官方书籍，有中文版，有基础有提高；

Git权威指南：在Pro Git看完的基础上可以做进一步的提升。

## git add 后如何撤销
`git reset HEAD file`将file退回到unstage区。

## Git HEAD detached from XXX （git HEAD 游离）解决办法
处于游离状态的分支，其实就是一个匿名分支。如果此时进行分支切换，则游离分支上的修改和提交就会丢失。

如果想要保留游离分支上的修改，只需要把“匿名”变成正常分支即可。即在游离状态下新建一个分支。

> [Git中HEAD游离的原因与解决方法](https://cloud.tencent.com/developer/news/249871)

## git log获取短hash值
比如显示两条log，只需要：`git log -2`

但此时的commit id是一个比较长的hash值。如果想要获取短hash值：
```bash
git log -2 --abbrev-commit
```

## git切换到指定tag
个人感觉，tag像是一个不可修改的匿名branch，可以通过checkout来切换：
```bash
git checkout tag_name
```
此时会提示处于detached HEAD的状态。

> tag相当于一个快照，是不能更改它的代码的。

如果想在此tag的基础上进行修改，需要创建一个新分支：
```bash
git checkout -b branch_name tag_name
```

> [git切换到指定tag](https://blog.csdn.net/qq_20817327/article/details/121877017)
