# Random of Python

## 1 randint

randint 用于返回单个随机数, 语法为: `random.randint(a, b)`, 其取值范围为 [a, b]

## 2 sample

### 2.1 生成不重复随机数 

```Python
import random
print(random.sample(range(10), 5)
```

### 2.2 从 list 中取出随机不重复元素

```Python
import random
print(random.sample(['a', 'b', 'c', 'd'], 5)
```

