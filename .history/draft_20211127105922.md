### Poetry Environment:
- `poerty init -n`
- `poetry add django`
- `poetry shell`
- `poetry add --dev black`


### Setting up the project:
once Django installed, djandro-admin will be created automaticlly, 
- `django-admin startproject movies_project .`
- `python manage.py runserver`
- `python manage.py migrate`
- `python manage.py startapp movies_app`


### Add our app to our project:
- (1) in project folder -> settings.py -> Installed_Apps -> app_name.apps.classNameInsideApp.py
connect your app more with the project, the urls is the recevier for every request
- (2) in project folder -> urls.py -> urlpatterns -> path('', include('movies_app.urls'))
- (3) in app: create urls.py -> urlpatterns = [ path('', HomeView.as_view(), name='home' ),]
- (4) in app -> views.py -> create the view as a class
- (5) Create templates -> home.html -> add our code
- (6) settings.py -> Templates -> 'DIRS': [os.path.join(BASE_DIR,'templates')],