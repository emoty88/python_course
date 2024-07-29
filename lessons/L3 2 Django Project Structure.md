# 3.2 Django Project Structure

### Understanding the Project Directory Structure

When you create a new Django project, Django sets up a default directory structure. Understanding this structure is crucial for efficiently navigating and managing your Django projects.

**Example Structure:**

```markdown
myproject/
    manage.py
    myproject/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```

**Key Files and Folders:**

- **manage.py**: A command-line utility that lets you interact with this Django project. You can use it to start a development server, create applications, and more.
- **myproject/**: The inner project directory. This name is the same as the project name you chose.
    - **init.py**: An empty file that tells Python this directory should be considered a Python package.
    - **settings.py**: This file contains all the configuration settings for your project, such as database configuration, installed apps, middleware, and more.
    - **urls.py**: This file contains the URL declarations for the project. It maps URLs to views.
    - **wsgi.py**: An entry-point for WSGI-compatible web servers to serve your project.

### Creating an Application

In Django, an application is a web application that does something, e.g., a blog system, a database of public records, or a simple poll app. A project can contain multiple applications.

**Steps to Create an Application:**

1. **Create the Application:**
Use the `startapp` command to create an application:
    
    ```bash
    python manage.py startapp myapp
    ```
    
2. **Add the Application to INSTALLED_APPS:**
Open `settings.py` and add your application to the `INSTALLED_APPS` list:
    
    ```python
    INSTALLED_APPS = [
        ...
        'myapp',
    ]
    ```
    

**Application Structure:**

```markdown
myapp/
    __init__.py
    admin.py
    apps.py
    models.py
    tests.py
    views.py
    migrations/
        __init__.py
```

**Key Files:**

- **admin.py**: Register your models here so they can be managed through the Django admin interface.
- **apps.py**: Configuration for the application.
- **models.py**: Define your application’s data models here.
- **tests.py**: Write your application’s tests here.
- **views.py**: Define your application’s views here.
- **migrations/**: This directory contains migration files that allow Django to track changes to your models and apply them to your database.

For more detailed information, refer to the [official Django documentation on applications](https://docs.djangoproject.com/en/stable/ref/applications/).