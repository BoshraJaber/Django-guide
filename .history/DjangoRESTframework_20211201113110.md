# Django REST framework:

## Getting Started:
* `poetry add django djangorestframework`
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
fro,m .views import PostsListView,PostsDetailsView
urlpatterns = [
    path('', PostsListView,as_view(),  ), # api/v1/posts
    path('/<int:pk>', PostsDetailsView.as_view()) # /api/v1/posts/<int:pk>


]
```
* Creating the view: 
```
from rest_framework import generics
from .model import Post
from .serializers import PostSerializer

class PostsListView(generics.ListAPIView): # for hget requests
    serializer_class =  PostSerializer # instead of Template name, it will give me the data as a json file
    queryset = Post.objects.all() # instead of model


class PostsDetailsView(generics.ListCreateAPIView): # For post requests
   serializer_class =  PostSerializer
   queryset = Post.objects.all()

```
* create Serializer :
 * Serializer read the data from the table of the database and turn it into json and give it to the view
 * In app folder, create serializer.py:
```
from rest_framework import serializers

class PostSerializer(serializers.ModelSerializer):
  class Meta:
   fields = ('columns1', 'columns2') # the files I want to see in the json files.
   model = Post
]
```

* For testing the requests in another folder:in terminal -> `poetry shell` -> `poetry add requests` -> `python` -> `import requests` -> `r=requests.get('http://127.0.0.1:8000/api/v1/posts')` -> `r.status_code` =200 -> `r.json()` = my data

## Docker:
* we use it instead on the environment, It is like a container.
* It is responsible of containers, each container has everything you need like the requirement, the python version, the frameworks and libraries, we install them all in a docker file

### setting up docker:
* exit the environment
* create a file `Dockerfile` with no extension on the same level as manage.py, it should be named so.
* Run docker on your machine
* We are not going to change anything in the project, just run it on docker
* Copy a code to the Dockerfile 
* Create another file called : `docker-compose.yml`, copy another code to it
* inside the code there is a command to run the server
* running the code : `docker-compose up` it will give an error
* `poetry export -f requirements.txt -o requirements.txt` export everything in poetry to a file called requirements.txt and create it if it doesn't exists
* `docker-compose up` it will shows an error because we didn't add docker to the settings.py
* in settings.py -> `Allowed_HOSTS = [0.0.0.0]`
* `ctrl+c` to shutdown docker