# Django Model
* [Documentation](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Models)

## Create a superuser:
* run `python manage.py createsuperuser` then add the required fields.
*  Go to [http://127.0.0.1:8000/admin]( http://127.0.0.1:8000/admin) and sign in to access the admin panel
* Groups and Users are default from Django
* Groups has permissions for CRUD to the database.

## Create the model (MVT):
* define each table as a class and columns as properties to this class
* More details in the documentation.
* in the app folder -> models.py:
```
from django.db import models
from django.contrib.auth import get_user_model

class TableName(models.Model):
   column1 = models.TextField()
   column2 = models.CharField(max_length=255)
   fk = models.ForeignKey(get_user_model(),on_delete=models.CASCADE)

   def __str__(self) -> str:
     return self.column1 
     # or return self.fk.column_of_fk
     
```
  

## Register the model to the admin panel:
* in app folder -> admin.py:
  ```
  from django.contrib import admin
  from .models import modelName

  admin.site.register(modelName)
  ```
* After that, we need to migrate the new database so that django is aware of it
* `python manage.py makemigrations` this command will look at all models in all the application 
* to specify a certain application: `python manage.py makemigrations app_name`
* To apply the changes: `python manage.py migrate`
* 

## Create the view for the model (MVT):
* To link the db with the template
* in app folder -> views.py: 
* ```
  from django.views.generic import TemplateView, ListView 
  class ListView(ListView):
     template_name = 'list.html'
     model = modelName //table name

* ```
* In generic:
  1. ListView: refers to a view (logic) to display multiple instances of a table in the database.
  2. DetailView:  should be used when you want to present detail of a single model instance.
  3. 
## Create the template for the model (MVT):
* in templates folder -> create the html files
* create a base.html to avoid repetition.
* To extend from base.html:
```
{%extends 'base.html' %}

{%block blockName%}
{% for item in object_list %} where object_list is a reserved word
{{item.column_name}}
{{<a href="{% url 'name' item.pk%}">}} // to redirect to each item by its id, pk( primary key)
{%endfor%}
// I write this in the template
// the view will send all the info needed to the template
{%endblock blockName%}
```