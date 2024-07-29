# L3.3 Django Models and ORM

### Defining and Migrating Models

In Django, models are defined as Python classes. Each model maps to a single database table. You define the fields of the model and their behavior.

**Example:**

```python
# myapp/models.py
from django.db import models

class Author(models.Model):
    first_name = models.CharField(max_length=100)
    last_name = models.CharField(max_length=100)
    birth_date = models.DateField()
    biography = models.TextField()
    metadata = models.JSONField()  # Requires PostgreSQL or MySQL 5.7.8+ for JSON support

    def __str__(self):
        return f"{self.first_name} {self.last_name}"
```

**Common Field Types:**

- `CharField`: A string field for small-to-medium-sized strings.
- `TextField`: A large text field.
- `IntegerField`: An integer field.
- `DateField`: A date field.
- `DateTimeField`: A date and time field.
- `BooleanField`: A true/false field.
- `JSONField`: A field for storing JSON-encoded data. Requires PostgreSQL or MySQL 5.7.8+ for JSON support.

For more information on model fields, refer to the [official Django documentation on model field types](https://docs.djangoproject.com/en/stable/ref/models/fields/).

**Creating Migrations:**
Migrations are Django's way of propagating changes you make to your models (adding a field, deleting a model, etc.) into your database schema. They are designed to be mostly automatic but flexible to let you manually tweak the changes if needed.

**Creating Migrations:**

```bash
python manage.py makemigrations
```

**Applying Migrations:**

```bash
python manage.py migrate
```

**Example:**

```bash
python manage.py makemigrations myapp
python manage.py migrate myapp
```

### Basic ORM Queries

The Django ORM allows you to interact with your database using Python code. Here are some basic queries you can perform using the ORM:

**Creating Objects:**

```python
author = Author.objects.create(first_name="John", last_name="Doe", birth_date="1970-01-01")
```

**Retrieving Objects:**

```python
# Get all objects
authors = Author.objects.all()

# Filter objects
john_does = Author.objects.filter(first_name="John")

# Get a single object
john_doe = Author.objects.get(pk=1)
```

**Updating Objects:**

```python
author = Author.objects.get(pk=1)
author.last_name = "Smith"
author.save()
```

**Deleting Objects:**

```python
author = Author.objects.get(pk=1)
author.delete()
```

For more detailed information, refer to the [official Django documentation on making queries](https://docs.djangoproject.com/en/stable/topics/db/queries/).

### Django Object Manager

Django provides a powerful object-relational mapping (ORM) layer that simplifies interaction with the database. The `Manager` is the interface through which database query operations are provided to Django models.

**Using the Default Manager:**
Every Django model has at least one `Manager`, and by default, it's named `objects`.

**Custom Managers:**
You can define custom managers by extending the `models.Manager` class.

**Example:**

```python
class PublishedManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(is_published=True)

class Article(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    is_published = models.BooleanField(default=False)

    objects = models.Manager()  # The default manager
    published = PublishedManager()  # Our custom manager
```

**Using Custom Managers:**

```python
# This will use the custom manager to get only published articles
published_articles = Article.published.all()
```

For more information, refer to the [official Django documentation on managers](https://docs.djangoproject.com/en/stable/topics/db/managers/).