### django-oauth-toolkit
---
https://github.com/jazzband/django-oauth-toolkit

https://django-oauth-toolkit.readthedocs.io/en/latest/

```py
class SongView(views.APIView):
  authentication_classes = [OAuth2Authentication]
  permission_classes = [TokenHasScope]
  required_scopes = ['music']

class SongView(views.APIView):
  authentication_classes = [OAuth2Authentication]
  permission_classes = [TokenHasReadWriteScope]
  required_scopes = ['music']

class SongView(views.APIView):
  authentication_classes = [OAuthentication]
  permission_classes = [TokenHasResourceScope]
  required_scopes = ['music']

class SongView(views.APIView):
  permission_classes = [IsAuthenticatedOrTokenHasScope, DjangoModelPermission]
  required_scopes = ['music']

class SongView(views.APIView):
  authentication_classes = [OAuth2Authentication]
  permission_classes = [TokenMatchesOASRequirements]
  required_alternate_scopes = {
    "GET": [["read"]],
    "POST": [["create"], ["post", "widget"]],
    "PUT": [["update"], ["put", "widget"]],
    "DELETE": [["delete"], ["scope2", "scope3"]],
  }





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
openapi: "3.0.0"
info:
  title: songs
  version: v1
components:
  securitySchemes:
    song_auth:
      type: oauth2
      flows:
        implicit:
          authorizationUrl: http://localhost:8000/o/authorize
          scopes:
            read: read about a song
            create: create a new song
            update: update an existing song
            delete: delete a song
            post: create a new song
            widget: widget scope
            scope2: scope too
            scope3: another scope
paths:
  /songs:
    get:
      security:
        - song_auth: [read]
      responses:
        '200':
          description: A list of songs.
    post:
      security:
        - song_auth: [create]
        - song_auth: [post, widget]
      responses:
        '201':
          description: new song added
    put:
      security:
        - song_auth: [update]
        - song_auth: [put, widget]
      responses:
        '204':
          description: song updated
    delete:
      security:
        - song_auth: [delete]
        - song_auth: [scope2, scope3]
      responses:
        '200':
          description: song deleted

```


