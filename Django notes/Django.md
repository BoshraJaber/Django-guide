# Starting with Django:

## Folder Structure:
![](https://studygyaan.com/wp-content/uploads/2019/07/Best-Practice-to-Structure-Django-Project-Directories-and-Files.png)


## Getting Started:
1. <span style="color:Green">Poetry Environment:</span>
   * `poetry init -n`
   * `poetry shell`
   * `poetry add django`
   * `poetry add --dev black`
  
  
2. <span style="color:Green">Setting up the project:</span>
   
    <span style="color:Grey">note: once Django installed, django-admin will be created automatically </span>

   * `django-admin startproject project_name .`
   
     <span style="color:Grey">note: the dot means create the folder in the same directory, removing the dot means create a folder and put the project inside it</span>

   * `python manage.py runserver`
  
     <span style="color:Grey">note: Running the server will give this message:  </span>
    <span style="color:red">You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
    Run 'python manage.py migrate' to apply them.</span>

   * `python manage.py migrate`


3. <span style="color:Green">Setting up the app:</span>
   
    <span style="color:Grey">note: One project can include multiple apps, we can divide each feature into app</span>
    * `python manage.py startapp app_name`

4. <span style="color:Green">Add app to project:</span>
   
   *  in project folder -> settings.py: (setting is the brain of the project)
```
    INSTALLED_APPS = [
     'app_name',
]
```

5. <span style="color:Green"> Add Template (MVT)</span>:
   * create a `templates` folder at the same level of the project.
   * create the required html files
   * we can create a base.html to avoid reputation and use *jinja template language*, [Jinja Documentation](https://jinja.palletsprojects.com/en/3.0.x/templates/)
   * Linking the templates folder to the project: in project folder -> settings.py:
```
TEMPLATES = [
    {

        'DIRS': [BASE_DIR/ 'templates'],
]
```
 

6. <span style="color:Green"> Add View (MVT)</span>:
    
   *  in app folder -> views.py:
```
from django.views.generic import TemplateView

class HomePage(TemplateView):
    template_name = 'home.html'
```
   

7. <span style="color:Green"> Add Model (MVT)</span>:
   *  in app folder -> views.py:
```
from django.db import models

class HomePage(models.Model):
    title= models.TextField()
    
    def__str__():
       return self.title

    
       
```

8. <span style="color:Green"> Add the URLS of my app to the project </span> (one time for each app):
      *  in project folder -> urls.py:
```
urlpatterns = [
    
    path('', include('app_name.urls')),
]
```
9. <span style="color:Green"> Add the URLS to my app  </span>:
      *  in app folder -> create urls.py:
```
from django.urls import path
from .views import HomePage

urlpatterns = [
    path('', HomePage.as_view(), name='home'),
]

```


10. <span style="color:Green"> Using sqlite3:</span>
 
   * install sqlite3 extension
   * press ctrl + shift+ p
   * type sqlite and chose: `SQLite: Open Database`
   * Check SQLite Explorer for details about the databases
  

11.  <span style="color:Green"> Jinja notes:</span>
    * `{% ... %}` for Statements
    * `{{ ... }}` for Expressions to print to the template output
    * `{# ... #} `for Comments not included in the template output
    * Adding a link: `<a href= {% url 'home'%}`, where `home` is the name of the url.
    * Example:
    ```
   {% for item in navigation %}
        <li><a href="{{ item.href }}">{{ item.caption }}</a></li>
   {% endfor %}
    ```

12.  <span style="color:Green"> Add model to admin :</span>
  * In admin.py: 
```
from .models import model_name

@admin.register(model_name)

class AdminSomething(admin.models):
   # specify the columns names
```

## Django Flow:
* The browser is hitting a url
* Django search in project/urls.py for that endpoint and check the urlpatterns and which app I am trying to use
* From app/urls.py will check which view to use
* From app/views.py will check which template 
* The template will be rendered to the Browser

![](https://miro.medium.com/max/1142/0*z4K0hNJUynqnKmSE.png)


