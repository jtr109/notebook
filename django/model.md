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
    


