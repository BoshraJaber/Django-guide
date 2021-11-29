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

// gettext used when langauge is changed
  class User(abstractBaseUser, PermissionMixin):
    email = models.EmailField( _('email address'))
    etc .....
    USERNAME_FIELD = 'email' it is the required field for loggin 
    REQUIRED_FIELDS is for super admin user
  ```
  class Meta:
   // will define the name and its plural

6. Create the view:
   


##  Abstract model vs abstract base user model
* abstract user model is the base class of the user model
* 
  