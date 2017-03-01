# Questions of Python

## 1 实践考点

### 1.1 写一个装饰器

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

## 2 理论考点

### 2.1 特点

- Python 是一种**解释型**语言. 代码在运行前不需要编译.
- Python 是一种**动态**类型语言. 使用变量之前不需要声明变量类型.
- Python 的类支持组合和继承. 适合**面对对象**编程.
- Python 中的函数和类都能作为参数和返回.
- Python 运行速度比变易语言**慢**, 不过其允许基于C编写的扩展. 

### 2.2 多线程

Python 没有真正的多线程, GIL 确保多线程中只有一个线程会被执行, 这反而大大拖慢了运行速度.

### 2.3 函数参数默认值

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

### 2.4 @classmethod, @staticmethod, @property

- 普通方法的第一个参数是其实例 (self)
- 类方法的第一个参数是其类 (cls)
- 静态方法只传入给定的参数, 没有实例或类被传入
- property 与 setter 组合使用

具体见[例子](http://codingpy.com/article/essential-python-interview-questions/#9)

### 2.5 super 和多重继承

super 保证每个父类只被调用一次. 继承顺序自下而上, 广度优先, 自左向右. 与执行顺序相反. 具体顺序可由 `Cls.__mro__`  得到.

### 2.6 垃圾回收机制

- Python 在内存中存储了每个对象的引用计数, 如果计数变成0, 则回收内存
- 对于引用循环会定时查找并回收
- 启发式算法

详见[问题](http://codingpy.com/article/essential-python-interview-questions/#12)

