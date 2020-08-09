## Запись в INSTALLED_APPS

\#Django \#Python

Различия между записи в INSTALLED_APPS, просто названия приложения:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog', # <-
]
```

Либо более расширенной версии с указанием класса приложения:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog.apps.BlogConfig', # <-
]
```

Класс **BlogConfig** находится в файле `[имя_проекта]/blog/apps.py`

Оба варианта работать будут одинаково, только во втором случае, мы сможем что-то переопределить, дополнительно дописать и тп.