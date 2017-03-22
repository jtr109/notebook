# Model of Django

## 1 create()

create() 时需要填入对应的参数, 包括外键, 外键可以是某个模型的实例.

```Python
from django.db import models

class City(models.Model):
    name = models.CharField(max_length=60)
    phone_code = models.CharField(max_length=60)


class People(models.Model):
    name = models.CharField(max_length=60)
    city = models.ForeignKey(City, verbose_name="born in city")


info = {'name': 'shanghai', 'phone_code': '021'}
sh = City.objects.create(**info)  # 对于模型的值可以这样作为字典传入, 函数内部 unpack)
tom = People.objects.create(name='Tom', city=sh)
```
    
## 2 模型实例的创建

无论是哪种关系模型, 都必须保存后才能作为参数传入其他模型. 因为只有保存以后, 实例才能获得相应的 id.

### 2.1 多对一关系的建立

```Python
from django.db import models

class Province(models.Model):
    name = models.CharField(max_length=200)


class City(models.Model):
    name = models.CharField(max_length=200)
    province = models.ForeignKey(Province)
```

建立 City 的实例时, 需要赋值参数 province, 即 Province. 所以必须先创建一个 Province, 再创建 City 的实例, 并把 Province 的实例赋给它.

```Python
jiangsu = Province.objects.create(name="jiangsu")
suzhou = City.objects.create(name="suzhou", province=jiangsu)
```

Reference:

- [Many-to-one relationships](https://docs.djangoproject.com/en/1.10/topics/db/examples/many_to_one/)

### 2.2 多对多关系

```Python
from django.db import models

class Publication(models.Model):
    title = models.CharField(max_length=30)

    def __str__(self):              # __unicode__ on Python 2
        return self.title

    class Meta:
        ordering = ('title',)

class Article(models.Model):
    headline = models.CharField(max_length=100)
    publications = models.ManyToManyField(Publication)

    def __str__(self):              # __unicode__ on Python 2
        return self.headline

    class Meta:
        ordering = ('headline',)
```

在 Django 中建立多对多关系时, 必须先创建在具有 ManyToMany 那一侧的字段也保存后, 才能调用 add 方法加入关系实例.

```Python
p0 = Publication(title="The Django Journal")
p0.save()
a0 = Article(headline="Django lets you build Web apps easily")
a0.save()  # important!
a1.publications.add(p0)
```
Reference:

- [Many-to-many relationships](https://docs.djangoproject.com/en/1.10/topics/db/examples/many_to_many/)

# Dumpdata

You can use `dumpdata` to get the whole database for you project. The file output can be used for fixture.

The command should be like below:

```bash
$ python ./manage.py dumpdata mysite.ModelName --indent 2 -o ./path/to/save
```

Reference:

- [dumpdata - Django Documentation](https://docs.djangoproject.com/en/1.10/ref/django-admin/#dumpdata)
