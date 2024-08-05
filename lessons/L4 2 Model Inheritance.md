# L4.2 Model Inheritance

### Class Meta

The `Meta` class is used to define metadata options for Django models. It provides various options to control the model's behavior, such as ordering, verbose name, abstract status, and more.

**Common `Meta` options:**

- `abstract`: If `True`, the model will be an abstract base class.
- `ordering`: A list of fields to use for ordering the query results.
- `verbose_name`: A human-readable name for the object.
- `verbose_name_plural`: The plural name for the object.

**Example:**

```python
class MyModel(models.Model):
    name = models.CharField(max_length=100)

    class Meta:
        ordering = ['name']
        verbose_name = 'My Model'
        verbose_name_plural = 'My Models'
```

### Abstract Base Classes

Abstract base classes are used when you want to put some common information into a number of other models. You don’t want to create a separate table for the base class.

**Example:**

```python
# myapp/models.py
from django.db import models

class CommonInfo(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True

class Author(CommonInfo):
    first_name = models.CharField(max_length=100)
    last_name = models.CharField(max_length=100)
    birth_date = models.DateField()
    biography = models.TextField()

class Book(CommonInfo):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(Author, on_delete=models.CASCADE, related_name='books')
```

### Multi-table Inheritance

Multi-table inheritance is used when each model in the hierarchy is its own database table.

**Example:**

```python
# myapp/models.py
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(Author, on_delete=models.CASCADE, related_name='books')

class EBook(Book):
    file_format = models.CharField(max_length=10)
    download_link = models.URLField()
```

### Proxy Models

Proxy models are used when you want to modify the Python-level behavior of a model without changing the model’s fields.

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

class ActiveAuthor(Author):
    class Meta:
        proxy = True
		
		#The @property decorator allows a method to be accessed like an attribute.
		@property 
    def full_name(self):
        return f"{self.first_name} {self.last_name}"
```

For more detailed information on model inheritance in Django, refer to the [official Django documentation on model inheritance](https://docs.djangoproject.com/en/stable/topics/db/models/#model-inheritance).