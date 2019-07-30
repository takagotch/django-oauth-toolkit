### django-oauth-toolkit
---
https://github.com/jazzband/django-oauth-toolkit

https://django-oauth-toolkit.readthedocs.io/en/latest/

```py
INSTALLED_APPS = (
  'oauth2_provider',
)

urlpatterns = [
  url(r'^o/', include('oauth2_provider.urls', namespace='oauth2_provider')),
]
```

```sh
pip install django-oauth-toolkit

```

```
```


