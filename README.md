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

Now we have to add some settings to out ``mysite/settings.py``
first: we’ve to registered the DRF and CORS headers packages with our project by adding them to ```INSTALLED_APPS```.
Then, we added a piece of custom CORS middleware

first, we have to set ```DEFAULT_PERMISSION_CLASSES``` which in this case will require a request to be authenticated, then we have to set ```DEFAULT_AUTHENTICATION_CLASSES```which determines which authentication methods the server will try when it receives a request.

And finally: we will have to add ```localhost:3000``` to the ```CORS_ORIGIN_WHITELIST```, because that's where the request from our React app will be coming

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
Now we have to apply migrations and make a superuser to check everythings working perfeectly
```python manage.py migrate```

