twentytab-model-to-bidimensional
================================

A django app that returns a bidimensional representation of a given model and queryset following foreign keys recursively

**It doesn't work with many-to-many fields yet**

## Installation

Use the following command: <b><i>pip install twentytab-model-to-bidimensional</i></b>


## Usage

```py
from django.db import models


class Foo(models.Model):
    name = models.CharField(max_length=250)


class Bar(models.Model):
    foo = models.ForeignKey(Foo)
    name = models.CharField(max_length=250)

```

```py
>>> from bidimensional import Bidimensional
>>> from myapp.models import Bar
>>> b = Bidimensional(Bar, depth=-1, queryset=Bar.objects.all())
>>> b.headers()
[u'id', u'name', u'foo__id', u'foo__name']
>>> b.items()
[{u'foo__id': 1, u'id': 1, u'foo__name': u'foo 1', u'name': u'bar 1'}, {u'foo__id': 2, u'id': 2, u'foo__name': u'foo 2', u'name': u'bar 2'}]
```

The results can be used to create a table like this example:

![ScreenShot](https://raw.github.com/20tab/twentytab-model-to-bidimensional/master/screenshot.png)
