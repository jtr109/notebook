# 基础知识整理

## 1 Python

实践考点:

- 写一个装饰器

```
# 计算函数时间
def exe_time(func):
    def wrapper(*args, **kwargs):
        st = time.time()
        print "@%s, {%s} start" % (time.strftime("%X", time.localtime()), func.__name__)
        back = func(*args, **args2)
        print "@%s, {%s} end" % (time.strftime("%X", time.localtime()), func.__name__)
        print "@%.3fs taken for {%s}" % (time.time() - st, func.__name__)
        return back
```

### 1.1 特点

- Python 是一种解释型语言. 代码在运行前不需要编译.
- Python 是一种动态类型语言. 使用变量之前不需要声明变量类型.
- Python 的类支持组合和继承. 适合面对对象编程.
- Python 中的函数和类都能作为参数和返回.
- Python 运行速度比变易语言慢, 不过其允许基于C编写的扩展. 

### 1.2 多线程

Python 没有真正的多线程, GIL 确保多线程中只有一个线程会被执行, 这大大拖慢了运行速度.

### 1.3 函数参数默认值

不要为函数的参数赋可变的数据类型, 例如:

```
def f(x, l=[]):
    for i in range(x):
        l.append(i*i)
    print l

f(2)
f(3,[3,2,1])
f(3)
```

中的局部变量 l 会在使用中发生变化, 见[例子](http://codingpy.com/article/essential-python-interview-questions/#6).

### 1.4 @classmethod, @staticmethod, @property

- 普通方法的第一个参数是其实例 (self)
- 类方法的第一个参数是其类 (cls)
- 静态方法只传入给定的参数, 没有实例或类被传入
- property 与 setter 组合使用

具体见[例子](http://codingpy.com/article/essential-python-interview-questions/#9)

### 1.5 super 和多重继承

super 保证每个父类只被调用一次. 继承顺序自下而上, 广度优先, 自左向右. 与执行顺序相反. 具体顺序可由 `Cls.__mro__`  得到.

### 1.6 垃圾回收机制

- Python 在内存中存储了每个对象的引用计数, 如果计数变成0, 则回收内存
- 对于引用循环会定时查找并回收
- 启发式算法

详见[问题](http://codingpy.com/article/essential-python-interview-questions/#12)


## 2 Web 框架

### 2.1 Flask

#### 2.1.1 单文件 demo

##### Hello world

```
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

if __name__ == "__main__":
    app.run()
```

##### post json

```
from flask import Flask, request, jsonify

app = Flask(__name__)


@app.route('/', methods=["POST"])
def root():
    content = request.get_json(force=True)
    info = content.get('info')
    if info:
        res = jsonify({'info': info})
        return res
    else:
        return jsonify({'error': 'info not exists.'}), 400


if __name__ == '__main__':
    app.run(debug=True)
```

#### 2.1.2 结构化框架

- 看书

### 2.2 Django

### 2.3 Tornado

## 3 Linux

### 3.1 定时调度 crontab

#### 3.1.1 主配置文件路径

/etc/crontab

#### 3.1.2 基础命令

- `-e`: 编辑当前 crontab
- `-l`: 显示当前 crontab 任务列表
- `-r`: 删除当前用户的 crontab

#### 3.1.3 编辑格式

minute hour day month dayofweek command

- 范围:
  - 第1列表示分钟1～59 每分钟用*或者 */1表示
  - 第2列表示小时1～23（0表示0点）
  - 第3列表示日期1～31
  - 第4列表示月份1～12
  - 第5列标识号星期0～6（0表示星期天）
  - 第6列要运行的命令

详情可查询[链接](http://blog.csdn.net/yangkai_hudong/article/details/13774895)

## 4 爬虫

## 5 前端

### 5.1 HTML / HTML5

### 5.2 CSS

### 5.3 JavaScript

## 6 SQL / NoSQL

* 关系型数据库：Mysql,pgsql
* NoSQL: Mongo, Redis

### 6.1 MySQL

#### 6.1.1 基础操作

通过SQL语句[增删改查](../mysql/usage.md)

- 进入
- 查询
- 创建数据库, 表格
- 删除

#### 6.1.2 Python 操作

通过 Python 操作数据库: [MySQL With Python](../mysql/with_python.md)

### 6.2 MongoDB

#### 6.2.1 基础操作

[通过终端语句操作数据库](../MongoDB/usage.md)

#### 6.2.2 Python 操作

[通过 Python 语句操作数据库](../MongoDB/pymongo.md)

### 6.3 Redis

#### 6.3.1 基础操作

#### 6.3.2 Python 操作

## 7 Git

## 8 部署相关

### 8.1 Nginx

## 9 TCP / IP

### 9.1 HTTP

## 10. RESTFul规范

### 10.1 含义

representation state transfer

### 10.2 核心概念

*一切都是资源*

### 10.3 资源和URI / URL

用URI (Uniform Resource Identifier)表示单一资源，用URL表示资源集合

### 10.4 资源设计理念

URI的设计应该遵循可寻址性原则，具有自描述性，需要在形式上给人以直觉上的关联。

### 10.5 URI设计技巧

* 单词用`-`隔开
* `/`体现层级关系
* 用`?`过滤资源：如，`/pulls?state=closed`
* `,`或`;`表示同级关系：如，`/git/git/compare/master;next`

### 10.6 请求与响应

请求：

* `GET`
* `POST`
* `PUT` ( /`PATCH`)
* `DELETE`

响应码：

* 200 (OK)
* 201 (Created)
* 204 (No Content)
* 303 (See Other)
* 400 (Bad Request)
* 404 (Not Found)
* 500 (Internal Server Error)
* 503 (Service Unavalible)

### 10.7 URI规范

*URI中不能使用动词，只能使用名词*

### 10.8 超媒体概念

超媒体即应用状态引擎 (hypermedia as the engine of application state)：把一个个把资源链接起来

### 10.9 无状态通行原则

服务器不应该保存客户端的状态。客户端负责维护应用状态，而服务端维护资源状态。

### 10.10 状态转移

“会话”状态不是作为资源状态保存在服务端的，而是被客户端作为应用状态进行跟踪的。客户端应用状态在服务端提供的超媒体的指引下发生变迁。

### 10.11 待学习知识

* 学习使用缓存

* 学习如何在head中包含版本号




## 3 TCP/IP, HTTP等常用协议

### 2.1 完整叙述一次HTTP请求从客户端到服务器端所经过的各个环节

#### 2.1.1 在浏览器中输入URL

#### 2.1.2 DNS通过域名查找IP地址

DNS查找顺序：

1. 浏览器缓存
2. 系统缓存
3. 路由器缓存
4. ISP DNS 缓存
5. 递归搜索

#### 2.1.3 浏览器给服务器发送HTTP请求

请求中一般包含：

1. URL
1. 控制转发，管理连接(Connection)
1. 浏览器自身定义(User-Agent)
1. 用户代理能够处理的媒体类型、内容编码、语言等及其优先级(Accept, Accept-Encoding...)
1. 请求的资源所处的互联网主机名和端口号(Host)
1. 希望获得管理支持(Cookie)

#### 2.1.4 永久重定向响应

#### 2.1.5 重定向地址请求

#### 2.1.6 服务端处理请求

#### 2.1.7 服务器返回响应

#### 2.1.8 客户端显示响应

#### 2.1.9 客户端发送内嵌对象的请求

#### 2.1.10 客户端发送异步(AJAX)请求

### 2.2 TCP/IP

#### 2.2.1 建立连接：三次握手

1. 客户端向服务器发送标有SYN的数据包
2. 服务器返回标有SYN/ACK的数据包
3. 客户端发送标有ACK的数据包

#### 2.2.2 断开连接：四次握手

1. 客户端发送带有FIN的报文
2. 服务器返回带有ACK的报文确认收到带有FIN的报文。
3. 服务器发送带有FIN的报文
4. 客户端返回带有ACK的报文确认收到带有FIN的报文，并等待，防止ACK未到达。

![握手图解][1]

参考文章：[TCP协议中的三次握手和四次挥手(图解)](http://blog.csdn.net/whuslei/article/details/6667471)

### 2.3 TCP/IP 协议族分层

![TCP/IP 通信传输流][2]


## WSGI：Web Server Gateway Interface

实现一个函数即可调用

    def application(environ, start_response):
        start_response('200 OK', [('Content-Type', 'text/html')])
        return '<h1>Hello, web!</h1>'
        
上面的`application()`函数就是符合WSGI标准的一个HTTP处理函数，它接收两个参数：

`environ`：一个包含所有HTTP请求信息的dict对象；

`start_response`：一个发送HTTP响应的函数。

在`application()`函数中，调用：

    start_response('200 OK', [('Content-Type', 'text/html')])
    
_`application()`函数必须由WSGI服务器来调用。_

------


1. 环境包：OpenStack,Docker,VirtualEnv

1. 开发框架,例如:twisted/tornado/django/gevent/libevent等

1. 精通Python具备良好的代码风格（PEP-8）


1. 有基本的前端技能，了解基本的网页设计知识，如 HTML、CSS、JavaScript、jQuery

1. Linux系统操作

1. git操作


[1]: http://hi.csdn.net/attachment/201108/7/0_131271823564Rx.gif

[2]: https://ws3.sinaimg.cn/mw690/3fb9d30bgw1f7aqos63wnj219d0z1wic.jpg


