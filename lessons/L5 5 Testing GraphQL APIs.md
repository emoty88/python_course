# L5.5 Testing GraphQL APIs

**Writing tests for GraphQL queries and mutations:**
Testing your GraphQL API is crucial to ensure its reliability and correctness. You can use Django's test framework along with `graphene.test.Client` to write tests for your GraphQL queries and mutations.

**Example:**

```python
from django.test import TestCase
from graphene.test import Client
from myapp.schema import schema

class GraphQLTestCase(TestCase):
    def setUp(self):
        self.client = Client(schema)

    def test_all_authors_query(self):
        query = '''
        {
            allAuthors {
                id
                firstName
                lastName
            }
        }
        '''
        executed = self.client.execute(query)
        self.assertIsNone(executed.errors)
        self.assertIsNotNone(executed.data['allAuthors'])

    def test_create_author_mutation(self):
        mutation = '''
        mutation {
            createAuthor(firstName: "John", lastName: "Doe", birthDate: "1990-01-01") {
                author {
                    id
                    firstName
                    lastName
                }
            }
        }
        '''
        executed = self.client.execute(mutation)
        self.assertIsNone(executed.errors)
        self.assertEqual(executed.data['createAuthor']['author']['firstName'], "John")
```

**Using GraphiQL for testing and debugging:**
GraphiQL is an in-browser tool for writing, validating, and testing GraphQL queries. It provides an interactive environment where you can execute GraphQL queries and mutations against your API.

To enable GraphiQL in your Django project, add the following to your `urls.py`:

```python
from django.urls import path
from graphene_django.views import GraphQLView
from django.views.decorators.csrf import csrf_exempt

urlpatterns = [
    path('graphql/', csrf_exempt(GraphQLView.as_view(graphiql=True))),
]
```

Once GraphiQL is enabled, you can access it by navigating to `/graphql/` in your browser. You can use it to:

- Write and execute GraphQL queries and mutations.
- View the results of your queries in real time.
- Explore the schema using the built-in schema explorer.
- Test various edge cases and error scenarios.