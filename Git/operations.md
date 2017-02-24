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

