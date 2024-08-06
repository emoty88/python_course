# L5.3 Defining GraphQL Schemas

**Types, Queries, and Mutations:**
In GraphQL, the schema is made up of types, queries, and mutations. Types define the shape of the data, queries are used to fetch data, and mutations are used to modify data.

**Creating a schema for models:**
Use `DjangoObjectType` to define types for your Django models.

**Example: Creating a schema for `Author` and `Book` models:**

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
    author_by_id = graphene.Field(AuthorType, id=graphene.Int())
    book_by_id = graphene.Field(BookType, id=graphene.Int())

    def resolve_all_authors(self, info):
        return Author.objects.all()

    def resolve_all_books(self, info):
        return Book.objects.all()

    def resolve_author_by_id(self, info, id):
        return Author.objects.get(pk=id)

    def resolve_book_by_id(self, info, id):
        return Book.objects.get(pk=id)

schema = graphene.Schema(query=Query)
```

**Explanation:**

- **Types**: `AuthorType` and `BookType` are defined using `DjangoObjectType`, which automatically maps Django models to GraphQL types.
- **Queries**: The `Query` class defines the queries available in the schema. In this example, `all_authors`, `all_books`, `author_by_id`, and `book_by_id` are defined as queries.
    - **resolve_all_authors** and **resolve_all_books**: These methods fetch all authors and books, respectively.
    - **resolve_author_by_id** and **resolve_book_by_id**: These methods fetch a specific author or book by their ID.

**Creating and Updating Data:**
To create and update data, you need to define mutations.

**Example: Creating and updating `Author` and `Book` models:**

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
    author_by_id = graphene.Field(AuthorType, id=graphene.Int())
    book_by_id = graphene.Field(BookType, id=graphene.Int())

    def resolve_all_authors(self, info):
        return Author.objects.all()

    def resolve_all_books(self, info):
        return Book.objects.all()

    def resolve_author_by_id(self, info, id):
        return Author.objects.get(pk=id)

    def resolve_book_by_id(self, info, id):
        return Book.objects.get(pk=id)

class CreateAuthor(graphene.Mutation):
    class Arguments:
        first_name = graphene.String()
        last_name = graphene.String()
        birth_date = graphene.Date()

    author = graphene.Field(AuthorType)

    def mutate(self, info, first_name, last_name, birth_date):
        author = Author(first_name=first_name, last_name=last_name, birth_date=birth_date)
        author.save()
        return CreateAuthor(author=author)

class UpdateAuthor(graphene.Mutation):
    class Arguments:
        id = graphene.Int()
        first_name = graphene.String()
        last_name = graphene.String()
        birth_date = graphene.Date()

    author = graphene.Field(AuthorType)

    def mutate(self, info, id, first_name=None, last_name=None, birth_date=None):
        author = Author.objects.get(pk=id)
        if first_name:
            author.first_name = first_name
        if last_name:
            author.last_name = last_name
        if birth_date:
            author.birth_date = birth_date
        author.save()
        return UpdateAuthor(author=author)

class CreateBook(graphene.Mutation):
    class Arguments:
        title = graphene.String()
        author_id = graphene.Int()

    book = graphene.Field(BookType)

    def mutate(self, info, title, author_id):
        author = Author.objects.get(pk=author_id)
        book = Book(title=title, author=author)
        book.save()
        return CreateBook(book=book)

class UpdateBook(graphene.Mutation):
    class Arguments:
        id = graphene.Int()
        title = graphene.String()
        author_id = graphene.Int()

    book = graphene.Field(BookType)

    def mutate(self, info, id, title=None, author_id=None):
        book = Book.objects.get(pk=id)
        if title:
            book.title = title
        if author_id:
            book.author = Author.objects.get(pk=author_id)
        book.save()
        return UpdateBook(book=book)

class Mutation(graphene.ObjectType):
    create_author = CreateAuthor.Field()
    update_author = UpdateAuthor.Field()
    create_book = CreateBook.Field()
    update_book = UpdateBook.Field()

schema = graphene.Schema(query=Query, mutation=Mutation)
```

**Explanation:**

- **Mutations**: `CreateAuthor`, `UpdateAuthor`, `CreateBook`, and `UpdateBook` are defined to handle creating and updating authors and books.
    - **CreateAuthor** and **CreateBook**: These mutations take the necessary arguments and create new instances of `Author` and `Book`.
    - **UpdateAuthor** and **UpdateBook**: These mutations update existing instances based on the provided ID and optional fields.
- **Mutation Class**: The `Mutation` class registers the mutations in the schema.

This setup allows you to query and mutate data for `Author` and `Book` models in your GraphQL API. You can now perform operations like creating, updating, and fetching authors and books using GraphQL.