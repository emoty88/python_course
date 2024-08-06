# L5.6 Apollo GraphQL Playground

To set up Apollo GraphQL Playground as the graphical interface for your GraphQL API instead of the default GraphiQL provided by Django-Graphene, you can follow these steps:

### Setting Up Apollo GraphQL Playground

**Step 1: Install Apollo Server**

First, you need to install the Apollo Server dependencies:

```bash
pip install django-graphql-playground
```

**Step 2: Configure Apollo GraphQL Playground**

Next, you need to configure your Django project to use Apollo GraphQL Playground. In your `urls.py` file, replace the GraphiQL view with the Apollo GraphQL Playground view.

**Example:**

```python
# myapp/urls.py
from django.urls import path
from django.views.decorators.csrf import csrf_exempt
from django_graphql_playground.views import GraphQLPlaygroundView

urlpatterns = [
    path('graphql/', csrf_exempt(GraphQLPlaygroundView.as_view(endpoint="/graphql/"))),
]
```

This configuration will set up Apollo GraphQL Playground at the `/graphql/` endpoint, allowing you to use the more modern and feature-rich GraphQL Playground interface.

### Testing GraphQL APIs with Apollo GraphQL Playground

**Using Apollo GraphQL Playground:**

Apollo GraphQL Playground provides a powerful interface for interacting with your GraphQL API. Here are some of the features you can take advantage of:

- **Interactive Querying**: Write and execute GraphQL queries and mutations.
- **Schema Exploration**: Browse and explore your GraphQL schema.
- **Real-time Updates**: View real-time responses from your GraphQL API.
- **Error Handling**: Detailed error messages and stack traces to help with debugging.

To access Apollo GraphQL Playground, simply navigate to `http://localhost:8000/graphql/` in your browser.

**Example Queries and Mutations:**

1. **Querying All Authors:**

```graphql
{
  allAuthors {
    id
    firstName
    lastName
  }
}
```

1. **Querying an Author by ID:**

```graphql
{
  authorById(id: 1) {
    id
    firstName
    lastName
  }
}
```

1. **Creating a New Author:**

```graphql
mutation {
  createAuthor(firstName: "Jane", lastName: "Doe", birthDate: "1990-01-01") {
    author {
      id
      firstName
      lastName
    }
  }
}
```

1. **Updating an Author:**

```graphql
mutation {
  updateAuthor(id: 1, firstName: "John", lastName: "Smith") {
    author {
      id
      firstName
      lastName
    }
  }
}
```

By integrating Apollo GraphQL Playground, you provide a modern and intuitive interface for developers to interact with your GraphQL API, making it easier to test and debug queries and mutations.