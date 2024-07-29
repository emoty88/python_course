# L3.4 Django Templates

### Brief Explanation and Examples

Django templates are a powerful way to separate the presentation layer from the logic layer in your Django applications. Templates are used to generate dynamic HTML content based on the data provided by the views.

**Creating a Template:**

1. Create a directory named `templates` in your app directory.
2. Inside the `templates` directory, create an HTML file (e.g., `index.html`).

**Example:**

```html
<!-- myapp/templates/index.html -->
<!DOCTYPE html>
<html>
<head>
    <title>My Django App</title>
</head>
<body>
    <h1>Hello, {{ name }}!</h1>
</body>
</html>

```

**Using a Template in a View:**
To use a template in a view, you need to import the `render` function from `django.shortcuts` and pass the template name along with the context data to the `render` function.

**Example:**

```python
# myapp/views.py
from django.shortcuts import render

def index(request):
    context = {'name': 'World'}
    return render(request, 'index.html', context)

```

**Rendering the Template:**
To render the template, you need to map a URL to the view in your `urls.py` file.

**Example:**

```python
# myapp/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

**Template Inheritance:**
Django templates support inheritance, which allows you to create a base template and extend it in other templates. This helps to avoid redundancy and maintain consistency across your templates.

**Base Template:**

```html
<!-- myapp/templates/base.html -->
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}My Django App{% endblock %}</title>
</head>
<body>
    {% block content %}
    {% endblock %}
</body>
</html>
```

**Child Template:**

```html
<!-- myapp/templates/index.html -->
{% extends 'base.html' %}

{% block title %}Home{% endblock %}

{% block content %}
    <h1>Hello, {{ name }}!</h1>
{% endblock %}

```

**Template Filters and Tags:**
Django templates provide a variety of built-in filters and tags to manipulate data and control the flow of the template rendering.

**Example:**

```html
<!-- Using filters -->
<p>{{ value|lower }}</p> <!-- Converts value to lowercase -->

<!-- Using tags -->
{% if user.is_authenticated %}
    <p>Welcome, {{ user.username }}!</p>
{% else %}
    <p>Please log in.</p>
{% endif %}

```

For more detailed information and advanced features, refer to the [official Django documentation on templates](https://docs.djangoproject.com/en/stable/ref/templates/).