# Pymongo 学习笔记

[Pymongo 使用参考](http://www.cnblogs.com/hangxin1940/archive/2012/07/29/2806471.html)

## 1 登录认证

```
from pymongo import MongoClient
client = MongoClient("mongodb://user:password@localhost:27017/")
```

## 2 数据操作

### 2.1 Mongo 结构

db.collection.document

### 2.2 collections

#### 2.2.1 查看

```
db = client.db_name
db.collection_names(include_system_collections=False)
```

#### 2.2.2 插入

没有的 collection 在插入其下的 document 的时候会自动生成

```
post = {"name": "post", "foo": "bar"}
db.collection.insert_one(post)
```

### 2.3 documents

#### 2.2.1 插入

```
posts = db.posts
posts.insert(post)
```

#### 2.2.2 查询

- 查询单个

```
posts.find_one({"author": "Mike"})
```

- 查询多个

```
for post in posts.find():   
    post 
```

- 计数

```
posts.count()
```

#### 2.2.3 修改

```
post = db.collection.find_one({"name": "post"})
post["foo"] = "bar2"
db.collection.save(post)
```
