# Django 单元测试

## 1 单元测试语句

### 1.1 全局测试

默认情况下会对当前路径下的所有名为 `test*.py` 的文件内发现测试.

```shell
$ python manage.py test
```
也可以使用对应的目录名, 或者 `-p`, `--pattern` 参数指定文件

```shell
$ python ./manage.py test ./animals
$ python ./manage.py test --pattern="tests_*.py"
```

## 2 测试环境的搭建

测试环境的搭建过程中可能遇到这样一个错误, `django.db.utils.ProgrammingError: hstore type not found in the database. please install it from your 'contrib/hstore.sql' file`.

出现这个问题的原因是 Django 的测试找不到 hstore 这个扩展, 它需要被手动安装到 template1 这个 database 中 (这一点存疑, 以及我需要用到的库中是否需要新建这个扩展. 之前单单在目标 database 中新建了该扩展, 仍然失败). 执行语句如下:

```shell
$ psql -d template1 -c 'create extension hstore;'
```

Reference:

- [Django test fail at postgres hstore migration](http://stackoverflow.com/questions/36322750/django-test-fail-at-postgres-hstore-migration)
- [How to install PostgreSQL's hstore to your default database template](https://dwradcliffe.com/2013/01/10/install-hstore-to-default-template.html)

## 3 fixture in Django test

A fixture is a collection of data that Django knows how to import into a database. For example, if your site has user accounts, you might set up a fixture of fake user accounts in order to populate your database during tests.

The most straightforward way of creating a fixture is to use the `manage.py dumpdata` command. 

TestCase loads fixtures once for the entire test class, before setUpTestData(), instead of before each test, and it use transactions to clean the database before each test.

Reference:

- [Fixture loading](https://docs.djangoproject.com/en/1.10/topics/testing/tools/#fixture-loading)
