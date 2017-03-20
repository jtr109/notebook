# 实践考点

## 1 写一个装饰器

```
 计算函数时间
def exe_time(func):
    def wrapper(*args, **kwargs):
        st = time.time()
        print "@%s, {%s} start" % (time.strftime("%X", time.localtime()), func.__name__)
        ret = func(*args, **args2)
        print "@%s, {%s} end" % (time.strftime("%X", time.localtime()), func.__name__)
        print "@%.3fs taken for {%s}" % (time.time() - st, func.__name__)
        return ret
```

## 2 实现一个单例模式

所谓单例，是指一个类的实例从始至终只能被创建一次。

可以使用一下方法实现:

- 使用 `__new__` 方法
- 共享属性
- 装饰器
- import 方法

具体可见[链接](https://github.com/taizilongxu/interview_python/blob/master/Readme.md#14-%E6%96%B0%E5%BC%8F%E7%B1%BB%E5%92%8C%E6%97%A7%E5%BC%8F%E7%B1%BB)


### 2.1 使用 `__new__` 方法

```
class Singleton(object):
    def __new__(cls, *args, **kw):
        if not hasattr(cls, '_instance'):
            orig = super(Singleton, cls)
            cls._instance = orig.__new__(cls, *args, **kw)
        return cls._instance

class MyClass(Singleton):
    a = 1
```

_值得注意的是, import 调用实例是典型的单例方法, 可以用来建立数据库连接之类的情况, 避免创建重复连接等可能._



# 理论考点

## 1 特点

- Python 是一种**解释型**语言. 代码在运行前不需要编译.
- Python 是一种**动态**类型语言. 使用变量之前不需要声明变量类型.
- Python 的类支持组合和继承. 适合**面对对象**编程.
- Python 中的函数和类都能作为参数和返回.
- Python 运行速度比变易语言**慢**, 不过其允许基于C编写的扩展. 

## 2 多线程

Python 没有真正的多线程, GIL 确保多线程中只有一个线程会被执行, 这反而大大拖慢了运行速度.

## 3 函数参数默认值

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

## 4 @classmethod, @staticmethod, @property

- 普通方法的第一个参数是其实例 (self)
- 类方法的第一个参数是其类 (cls)
- 静态方法只传入给定的参数, 没有实例或类被传入
- property 与 setter 组合使用

具体见[例子](http://codingpy.com/article/essential-python-interview-questions/#9)

## 5 super 和多重继承

super 保证每个父类只被调用一次. 继承顺序自下而上, 广度优先, 自左向右. 与执行顺序相反. 具体顺序可由 `Cls.__mro__`  得到.

## 6 垃圾回收机制

1. Python 在内存中存储了每个对象的引用计数, 如果计数变成0, 则回收内存
2. 对于引用循环会定时查找并回收
3. 启发式算法

问题详见[链接](http://codingpy.com/article/essential-python-interview-questions/#12), 在[这里](https://github.com/taizilongxu/interview_python/blob/master/Readme.md#24-python垃圾回收机制)可以找到更详细的解答.


## 其他

### Python

- Python 函数传入参数是值还是地址
- asyncio 的使用
- dict 是否线程安全
- 什么是装饰器, 有什么优点
- 什么是锁死
- myisam 和 innodb 的特点, 各自优缺点
- `__init__` 是类方法还是实例方法
- RESTful 中认证的过程, 其中 POST 创建了什么?
- 解释一下 flask 请求上下文和应用上下文
- 如何操作 redis 的消息队列
- redis 支持哪些结构
- mysql 的索引 (index) 的原理
- sqlalchemy 的事务 (transaction) 提交
- os.fork() 的应用


