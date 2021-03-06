# Omari_DjangoLearning
This repo is for tracking my Django learning path.

# Instructions
## Django
### Create a Django project
```
django-admin startproject PROJECT_NAME
```

### Add a new app to Django project
```
python3 manage.py startapp APP_NAME
```

### Run Django server
```
python3 manage.py runserver
```

### Make database migrations
```
python3 manage.py makemigrations APP_NAME
```
### Migrate database
```
python3 manage.py migrate
```

### Enable admin for an application
1. Create admin user: `python3 manage.py createsuperuser`
1. In `admin.py` file, register the models you have in `models.py` file for each app as follows:
```
from .models import MODEL1, MODEL2

admin.site.register(MODEL1)
admin.site.register(MODEL2)
```

### Steps to do after starting a new app
1. Add the app name to `INSTALLED_APPS` list in `settings.py` file.
1. Create `urls.py` file inside the new app and add `urlpatterns` list containing the paths for your app. Also, add the variable `app_name = "APP_NAME"` to avoid name collisions.
1. In the main `urls.py` file for the project, include the urls for the new app. (e.g `path('APP_NAME/', include('APP_NAME.urls')),`)
1. If the app will have html content, create `templates/APP_NAME` folder to add the html files in it.
1. Also, you can create `static/APP_NAME` for static files such as `css` and `js` files and images.

### Connect MySQL DB
In `settings.py` file, change the `DATABASES` variable to the following:
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'DB_SCHEMA_NAME',
        'USER': 'DB_USER',
        'PASSWORD': 'DB_PASSWORD',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

## Git
### Add description to your commit message
```
git commit -m "Commit message" -m "Commit description line #1" -m "Commit description line #2"
```

### Upload your work to your Repo
1. `git clone https://github.com/HackerSpaceJUST/<repo>`
1. Make a branch with a clear name for the feature you want to add: `git checkout -b BRANCH_NAME`. If the branch is already exist, then no need for the `-b` in the command.
1. Modify your changes on your local device.
1. When the modifications are finished: `git add .` to add all of the modified files.
1. Commit your work and write a clear message for your commit: `git commit -m "Your Message"`.
1. Push your work: `git push origin BRANCH_NAME`.
1. Go to `https://github.com/HackerSpaceJUST/<repo>`, add your commit as a pull request.
1. Go to Pull Requests and review your code.
1. If your changes got approved then merge it to the main branch.
1. Delete the used branch once the feature you're working on is finished.

### Common .gitignore content
```
**/__pycache__
**/migrations
.vscode
*.sqlite3
```

## MySQL
### Install MySQL
* `sudo apt-get install libmysqlclient-dev` (For `mysql_config`)
* `sudo apt-get install mysql-server`
* `python3 -m pip install mysqlclient`

### Fix 'Access denied for user 'root'@'localhost'
* `sudo mysql`
* `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'YOUR_PASSWORD';`

# Code Samples
## Python
### Redirect to another page
```
from django.http import HttpResponseRedirect
from django.urls import reverse

return HttpResponseRedirect(reverse('APP_NAME:PATH_NAME'))
```
Alternatively:
```
from django.shortcuts import redirect
return redirect('APP_NAME:PATH_NAME')
```

## HTML
### Link to another page
```
<a href="{% url 'APP_NAME:PATH_NAME'%}">Some Text</a>
```

### Add CSRF token to html form
```
<form action="{% url 'APP_NAME:PATH_NAME'%}" method="post">
    {% csrf_token %}
    <input type="submit">
</form>
```
### Sample layout page
```
<!DOCTYPE html>
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        {% block body %}{% endblock %}
    </body>
</html>
```

### Import layout page
```
{% extends "tasks/layout.html" %}

{% block body %}
    HTML CONTENT
{% endblock %}
```
