# L3.1 Introduction to Django

### 3.1 Introduction to Django

### Overview of Django Framework

Django is a high-level Python web framework that encourages rapid development and clean, pragmatic design. It follows the "batteries included" philosophy, providing many built-in features and tools.

**Key Features of Django:**

- **Reusability and "Pluggability" of Components**: Django promotes reusable components, allowing developers to use and share code across projects.
- **Rapid Development**: Django includes ready-to-use features for user authentication, content administration, and more, reducing development time.
- **Secure and Scalable**: Django helps developers avoid common security mistakes and can handle high-traffic sites.
- **Comprehensive Documentation**: Django has extensive and well-maintained documentation, making it easier for developers to find help and guidance.

 [Django official Django documentation](https://docs.djangoproject.com/en/stable/)

### Setting Up a Django Project

To set up a new Django project, follow these steps:

1. **Install Django:**
Make sure you have Django installed. You can install it using pip:
    
    ```bash
    pip install django
    ```
    
2. **Create a New Project:**
Use the `django-admin` tool to create a new project:
    
    ```bash
    django-admin startproject myproject
    ```
    
3. **Start the Development Server:**
Navigate to your project directory and start the development server:
    
    ```bash
    cd myproject
    python manage.py runserver
    ```
    
4. **Access the Development Server:**
Open your web browser and go to `http://127.0.0.1:8000/` to see the Django welcome page.