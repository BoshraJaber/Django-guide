# Django Custom User Model:

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

6. Create the view:
   


##  AbstractUser model vs AbstractBaseUser model: 
* [Documentation]()
* abstract user model is the base class of the user model
* 
  