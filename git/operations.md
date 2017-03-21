# Operations of Git

## 1 git mv

Git 管理的项目中, 重命名等情况请使用 `git mv` 代替 `mv`, 避免 Git 忽略文件变化.

### 1.1 修改文件(夹) 大小写

特别注意, 当希望使用 `git mv` 改变文件及文件夹大小写时, 不能直接写成:

```
$ git mv foo FOO
```

会报错误:

```
fatal: renaming 'foo' failed: Invalid argument
```

Git 无法识别. 需要进行中间转换:

```
$ git mv foo foo2
$ git mv foo2 FOO
```

## 2 git clean

### 2.1 删除空目录

_参考[文章](http://blog.csdn.net/skykingf/article/details/44078837)_

使用 `git rm -rf dir` 命令删除非空目录之后，本地还是会有空的目录存在，这时候空目录已经是untracked状态了。

解决办法是再删除掉untracked状态的目录，命令如下

```
$git clean -fd  
```

执行以上命令后，本地的空目录就没有了。


## 3 git rebase

### 3.1 简介

变基拉取, 将源分支的改动作为补丁加入当前分支, 再将当前分支的改动添加到后面. 即 change the base.

### 3.2 语句

```shell
$ git checkout dev  # go to the dev branch
$ git rebase master  # rebase from master
```
## 4 git reset

Three mode in git reset

- `--soft`: 缓存区和工作目录都不会改变, 只是提交历史改变, 即只有 HEAD 指针被前移
- `--mixed`: 默认选项, 缓存区和指定的提交同步, 单工作目录不受影响. 即缓存区里的数据被抛回工作区, HEAD 指针前移.
- `--hard`: 缓存区和工作目录都回退到指定的提交状态. 即缓存区和工作目录的内容清空到上一次提交的状态.

Tips on checkout:

This is useful for quickly inspecting an old version of your project. However, since there is no branch reference to the current HEAD, this puts you in a detached HEAD state. This can be dangerous if you start adding new commits because there will be no way to get back to them after you switch to another branch. For this reason, you should always create a new branch before adding commits to a detached HEAD.

Benefit to revert:

Reverting undoes a commit by creating a new commit. This is a safe way to undo changes, as it has no chance of re-writing the commit history. 

Reference:

- [Resetting, Checking Out and Reverting](https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting)
- [5.2 代码回滚：Reset、Checkout、Revert的选择 (上文翻译)](https://github.com/geeeeeeeeek/git-recipes/wiki/5.2-%E4%BB%A3%E7%A0%81%E5%9B%9E%E6%BB%9A%EF%BC%9AReset%E3%80%81Checkout%E3%80%81Revert%E7%9A%84%E9%80%89%E6%8B%A9) 

