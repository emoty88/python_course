# L5.2 Setting Up Graphene-Django

**Installing Graphene-Django:**
To get started with Graphene-Django, you need to install the library along with its dependencies.

```bash
pip install graphene-django
```

**Configuring Django settings:**
Add `graphene_django` to your `INSTALLED_APPS` and configure the GraphQL schema in your `settings.py`.

```python
# settings.py
INSTALLED_APPS = [
    ...
    'graphene_django',
]

GRAPHENE = {
    'SCHEMA': 'myapp.schema.schema'  # Where your GraphQL schema will be defined
}
```

**Creating a basic GraphQL schema:**
Create a new file `schema.py` in your Django app and define a basic schema.

```python
# myapp/schema.py
import graphene
from graphene_django.types import DjangoObjectType
from .models import Author, Book

class AuthorType(DjangoObjectType):
    class Meta:
        model = Author

class BookType(DjangoObjectType):
    class Meta:
        model = Book

class Query(graphene.ObjectType):
    all_authors = graphene.List(AuthorType)
    all_books = graphene.List(BookType)

    def resolve_all_authors(self, info):
        return Author.objects.all()

    def resolve_all_books(self, info):
        return Book.objects.all()

schema = graphene.Schema(query=Query)
```

**Setting Up GraphQL Endpoint:**
To expose the GraphQL schema through a URL endpoint, you need to update your `urls.py` file.

```python
# myapp/urls.py
from django.urls import path
from graphene_django.views import GraphQLView
from django.views.decorators.csrf import csrf_exempt

urlpatterns = [
    path('graphql/', csrf_exempt(GraphQLView.as_view(graphiql=True))),
]
```

With this setup, you have a working GraphQL API endpoint at `/graphql/`. You can access it using any GraphQL client, such as GraphiQL, which provides an interactive interface for testing and exploring your API.