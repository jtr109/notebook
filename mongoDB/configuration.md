# mongoDB 的安装与配置

## 1 安装与配置

### 1.1 安装

`$ sudo apt-get install mongodb-server`

### 1.2 编辑配置文件

#### 1.2.1 关闭 28017 端口

安装完成后, 使用 `$ ps aux | grep mongo` 可以发现. mongoDB 默认打开两个端口, 一个是 27017, 另一个是 28017.

参考 [mongodb笔记(一) 安装启动mongodb - 净土](http://howiefh.github.io/2014/04/26/mongodb-note-1-install-mongodb/) 可以知道:

> mongod还会启动一个非常基本的HTTP服务器，使用端口28017,可以访问http://localhost:28017 来获取数据库的管理信息。要更好利用好管理接口，需要用–rest选项开启REST支持。可以通过–nohttpinterface关闭管理接口。

这个端口我们不需要, 不开放.

1. 使用 `$ sudo vim /etc/mongodb.conf` 编辑 mongoDB 配置文件
2. 将 `nohttpinterface = true` 那行前面的注释去掉
3. 重启服务 `$ sudo service mongodb restart`
4. 使用 `$ ps aux | grep mongo` 查看端口是否正确关闭

#### 1.2.2 允许远程访问

Edit /etc/mongodb.conf, set "bind_ip" and "port" as below:

```
bind_ip = 0.0.0.0
port = 27017
```
