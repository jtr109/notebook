# Usage of MongoDB

详情查看 [runoob 教程](http://www.runoob.com/mongodb/mongodb-tutorial.html)

## 1 连接

```
mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]
```

## 2 操作数据库

### 2.1 创建

```
> use db_name
```

如果数据库不存在, 插入则创建

### 2.2 查看

```
> show dbs
```

### 2.3 删除

```
> use db_name
> db.dropDatabase()
```

## 3 操作集合

### 2.1 创建

通过插入文档创建集合

### 2.2 删除

```
> db.col.drop()
```

## 4 操作文档

### 4.1 插入

```
> db.col.insert(doc)
```

doc 为 JSON 类型

### 4.2 更新

```
db.collection.update(
   <query>,
   <update>,
   {
     upsert: <boolean>,
     multi: <boolean>,
     writeConcern: <document>
   }
)
```

或使用 save() 语句

```
db.collection.save(
   <document>,
   {
     writeConcern: <document>
   }
)
```

### 4.3 删除

```
db.collection.remove(
   <query>,
   {
     justOne: <boolean>,
     writeConcern: <document>
   }
)
```

### 4.4 查询

```
db.col.find({key1:value1, key2:value2}).pretty()
```





