# JWTauth_with_Django_-_React
```git
pipenv install
```
Once that’s done, activate the virtual environment with:
```git
pipenv shell
```
we need to install some packages
```git
pipenv install django
pipenv install djangorestframework
pipenv install djangorestframework-jwt
pipenv install django-cors-headers
```
after that we have to create a django project
```django-admin startproject mysite .```
Note the period at the end there — that denotes that we want to create the project with the current directory as as the root, rather than putting it in a new subdirectory.

know we have to add some settings to out ``mysite/settings.py``
```py
INSTALLED_APPS = [
    # ...
    'rest_framework',
    'corsheaders',
]

MIDDLEWARE = [
    # ...
    'corsheaders.middleware.CorsMiddleware', # Note that this needs to be placed above CommonMiddleware
    'django.middleware.common.CommonMiddleware', # This should already exist
    # ...
]

#...

REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': (
        'rest_framework.permissions.IsAuthenticated',
    ),
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_jwt.authentication.JSONWebTokenAuthentication',
        'rest_framework.authentication.SessionAuthentication',
        'rest_framework.authentication.BasicAuthentication',
    ),
}

CORS_ORIGIN_WHITELIST = (
    'localhost:3000',
)
```
