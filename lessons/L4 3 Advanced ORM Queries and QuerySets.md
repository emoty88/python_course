# L4.3 Advanced ORM Queries and QuerySets

### Filtering Related Objects Using `__`

In Django ORM, you can filter related objects using double underscores (`__`) to separate relationships and field lookups. This allows you to query across relationships.

**Example:**

```python
# Get all books by authors with the last name "Doe"
books = Book.objects.filter(author__last_name="Doe")

# Print the SQL query
print(books.query)
```

### Field Lookups

Django provides a variety of field lookups that you can use to filter your queries. These lookups allow you to perform complex queries using intuitive syntax.

**Common Field Lookups:**

- `__exact`: Exact match.
- `__iexact`: Case-insensitive exact match.
- `__contains`: Contains a substring.
- `__icontains`: Case-insensitive contains.
- `__in`: In a given list.
- `__gt`: Greater than.
- `__gte`: Greater than or equal to.
- `__lt`: Less than.
- `__lte`: Less than or equal to.
- `__startswith`: Starts with a substring.
- `__istartswith`: Case-insensitive starts with.
- `__endswith`: Ends with a substring.
- `__iendswith`: Case-insensitive ends with.

**Examples:**

```python
# Get all books with titles containing "Django"
books = Book.objects.filter(title__icontains="Django")

# Get all books with more than 300 pages
books = Book.objects.filter(pages__gt=300)

# Get all books published in the years 2020 or 2021
books = Book.objects.filter(published_date__year__in=[2020, 2021])

# Print the SQL queries
print(books.query)
```

For more detailed information on field lookups, refer to the [official Django documentation on field lookups](https://docs.djangoproject.com/en/stable/ref/models/querysets/#field-lookups).

### Query Expressions

Query expressions allow you to perform calculations and operations on the fields within the database. Django provides a variety of built-in expressions for performing arithmetic operations, value transformations, and aggregations.

**Example:**

```python
from django.db.models import F

# Increase the price of all books by 10
Book.objects.update(price=F('price') + 10)

# Get all books where the number of pages is greater than the author's age
books = Book.objects.filter(pages__gt=F('author__age'))

# Print the SQL queries
print(books.query)
```

For more detailed information on query expressions, refer to the [official Django documentation on query expressions](https://docs.djangoproject.com/en/stable/ref/models/expressions/).

### Using `Q` Objects for Complex Queries

The `Q` object in Django is used to encapsulate a collection of keyword arguments. These keyword arguments are used to define complex database queries. `Q` objects allow you to combine queries using logical operators (`&` for AND, `|` for OR).

**Example:**

```python
# Import Q
from django.db.models import Q

# Complex query using Q objects
# Find all books by authors named "John" or books with titles containing "Django"
books = Book.objects.filter(Q(author__first_name="John") | Q(title__icontains="Django"))

# Print the SQL query
print(books.query)
```

**Combining Queries:**
You can use `Q` objects to combine multiple conditions in a single query. This is especially useful for filtering based on multiple fields.

**Example:**

```python
# Find all books by authors named "John" and published after 2020
books = Book.objects.filter(Q(author__first_name="John") & Q(published_date__year__gt=2020))

# Print the SQL query
print(books.query)
```

**Building Complex Queries with `Q` Objects:**`Q` objects can be nested to build more complex queries.

**Example:**

```python
# Find all books by authors named "John" or "Jane", and either published after 2020 or having more than 500 pages
books = Book.objects.filter(
    (Q(author__first_name="John") | Q(author__first_name="Jane")) &
    (Q(published_date__year__gt=2020) | Q(pages__gt=500))
)

# Print the SQL query
print(books.query)
```

### Query Optimization

**Efficient Querying Techniques:**
To optimize your queries, it's important to minimize the number of database hits and fetch only the data you need.

- **Use `only` and `defer` to fetch specific fields:**
    
    ```python
    # Fetch only the title and author of books
    books = Book.objects.only('title', 'author')
    
    # Print the SQL query
    print(books.query)
    ```
    
- **Use `select_related` and `prefetch_related` for related objects:**
    
    ```python
    # Use select_related for foreign key relationships
    books = Book.objects.select_related('author').all()
    
    # Use prefetch_related for many-to-many relationships
    books = Book.objects.prefetch_related('genres').all()
    
    # Print the SQL queries
    print(books.query)
    ```
    

**Reducing Query Count:**
To reduce the number of queries, you can use aggregation and annotation to perform calculations at the database level rather than in Python.

**Examples:**

```python
# Import aggregate functions
from django.db.models import Count, Avg, Max, Min

# Count the number of books for each author
author_books_count = Author.objects.annotate(num_books=Count('books'))

# Calculate the average number of pages for each author
author_avg_pages = Author.objects.annotate(avg_pages=Avg('books__pages'))

# Get the maximum and minimum prices of books
book_price_stats = Book.objects.aggregate(max_price=Max('price'), min_price=Min('price'))

# Print the SQL queries
print(author_books_count.query)
print(author_avg_pages.query)
print(book_price_stats)
```

### Getting SQL Queries from ORM

**Using the `query` Attribute:**
The `query` attribute of a queryset returns the SQL query that will be executed.

**Example:**

```python
# Create a queryset
books = Book.objects.filter(title__icontains="Django")

# Print the SQL query
print(books.query)
```

**Analyzing and Debugging Queries:**
Django provides tools to analyze and debug SQL queries, such as the Django Debug Toolbar and database logging.

**Using Django Debug Toolbar:**

1. Install the Django Debug Toolbar:
    
    ```bash
    pip install django-debug-toolbar
    ```
    
2. Add it to your `INSTALLED_APPS` and `MIDDLEWARE` in `settings.py`:
    
    ```python
    INSTALLED_APPS = [
        ...
        'debug_toolbar',
    ]
    
    MIDDLEWARE = [
        ...
        'debug_toolbar.middleware.DebugToolbarMiddleware',
    ]
    ```
    
3. Add the debug toolbar URLs to your `urls.py`:
    
    ```python
    from django.urls import include, path
    
    urlpatterns = [
        ...
        path('__debug__/', include('debug_toolbar.urls')),
    ]
    ```
    

**Enabling Database Logging:**
Add the following configuration to your `settings.py` to log all database queries:

```python
LOGGING = {
    'version': 1,
    'handlers': {
        'console': {
            'level': 'DEBUG',
            'class': 'logging.StreamHandler',
        },
    },
    'loggers': {
        'django.db.backends': {
            'handlers': ['console'],
            'level': 'DEBUG',
        },
    },
}
```

For more detailed information on query optimization and debugging, refer to the [official Django documentation on queries](https://docs.djangoproject.com/en/stable/topics/db/queries/).