# Django REST framework:

## Getting Started:
* Create the project and the app
* Create the model
* Adding the "rest_framework" to the Installed App as a 3rd party application
* Give permission to use rest framework:  In settings.py:
```
REST_FrAMEWORK = {'DEFAULT_PERMISSION_CLASSES': [
    'rest_framework.permissions.AllowAny', // means allow any app to use this framework
]
}
```
* add urls.py of the app in the url.py of the project
* in the urls.py of the app -> add:
```
from django.urls import path
urlpatterns = [
    path('',  ), # api/v1/posts
    path('/<int:pk>') # /api/v1/posts/<int:pk>


]
```
* Creating the view:

