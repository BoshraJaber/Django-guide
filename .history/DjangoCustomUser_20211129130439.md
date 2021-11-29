# Django Custom User Model: Lecture 33

## Getting Started:
1.  Create a project named courses
2.  Create two app, accounts and projects
3.  Link the apps to the project from settings.py
4.  Include the urls of the apps in the url of the project

5.  Create a model:
   * in accounts app -> models.py:
```
  from django.contrib.auth.models import AbstractBaseUser, PermissionMixin, BaseUserManager
  from django.utils.translation import gettext as _

// gettext used when language is changed
  class User(abstractBaseUser, PermissionMixin):
    email = models.EmailField( _('email address'))
    etc .....
    USERNAME_FIELD = 'email' it is the required field for login 
    REQUIRED_FIELDS is for super admin user

  class Meta:
   // will define the name of the model and its plural

class CustomUserManger(BaseUserManager):
when I register a user, it has two methods:
- create a user 
- create a superuser
```
  * Run the command to test the results without actually runing the command:`python manage.py makemigrations --dry-run` 
  
6. To tell the project ot use my custom model:
   * in project folder -> settings.py:
  `AUTH_USER_MODEL =app_name.model_name `

7. Create the view to return list of users (list of models):
   * we need to create a view class and add to it the queryset and the serializer
   * Usually the serializer is created in a different folder
   * In app folder -> views.py:
```
from rest_framework.generic import ListAPIView
from .model import Person# (my custom user)

class ListUsers(ListAPIView):
    queryset = Person.objects.all()  # Which nodel is linked to this view
    serializer = 
```
 * in the app folder -> create serializer.py:
```
```
   


##  AbstractUser model vs AbstractBaseUser model: 
* [Documentation](https://docs.djangoproject.com/en/3.0/topics/auth/customizing/#extending-the-existing-user-model)
* abstract user model is the base class of the user model
* 
  