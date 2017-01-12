# MySQL 配置与应用笔记

## 1 mysql-server

### 1.1 下载与安装

在 ubuntu 环境下, 使用 `$ sudo apt-get install mysql-server` 即可安装.

### 1.2 常见问题

#### 1.2.1 Can't connect to MySQL server on '<remote-ip>' (61)

1. 查看 mysql 是否运行: `$ netstat -tulpen | grep 3306` 
2. 修改 mysql 配置文件: `$ vim /etc/mysql/my.cnf`
    - 修改 bind-address: `bind-address = 0.0.0.0`
3. 进入 mysql 修改权限: `$ sudo mysql -p`

    ```
    GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'%'IDENTIFIED BY 'mypassword' WITH GRANT OPTION;
    FLUSH PRIVILEGES;
    ```
    - 注意修改用户名(myuser)和密码(mypassword)
    - 附取消权限方法: [REVOKE Syntax - MySQL](http://dev.mysql.com/doc/refman/5.7/en/revoke.html)
4. 重启 mysql: `$ sudo /etc/init.d/mysql restart`

##### 1.2.1.1 Reference

- [Can't connect to remote MySQL server with error 61](http://stackoverflow.com/questions/16161889/cant-connect-to-remote-mysql-server-with-error-61)


### 常用指令

- 重启 mysql-server: `$ /etc/init.d/mysql restart`
- 登录 mysql: `$ mysql -h <remote-ip> -P <port> -u <username> -p`
