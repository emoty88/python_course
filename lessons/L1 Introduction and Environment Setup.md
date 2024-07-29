# L1: Introduction and Environment Setup

### 1.1 Introduction to Python and Setting Up the Environment

### Introduction to Python

Python is a high-level, interpreted programming language known for its simplicity and readability. It was created by Guido van Rossum and first released in 1991. Python is widely used for web development, data analysis, artificial intelligence, scientific computing, and more.

**Key Features of Python**:

- Simple and readable syntax
- Interpreted language
- Dynamic typing
- Extensive standard library
- Versatile and portable

### Installing Python

**For macOS**:
Open the Terminal and run the following command to install Python using Homebrew:

```bash
brew install python
```

**For Linux**:
Open the Terminal and run the following command to install Python using the package manager:

```bash
sudo apt-get update
sudo apt-get install python3
```

### Setting Up a Virtual Environment

**Introduction to Virtual Environments**:
A virtual environment is a self-contained directory that contains a Python installation for a particular version of Python, plus a number of additional packages.

**Using `virtualenv`**:

1. Install `virtualenv`:

   ```bash
   pip install virtualenv
   ```

2. Create a virtual environment:

   ```bash
   virtualenv myenv
   ```

3. Activate the virtual environment:
   - **macOS/Linux**:
     ```bash
     source myenv/bin/activate
     ```

**Using `virtualenvwrapper`**:

1. Install `virtualenvwrapper`:

   ```bash
   pip install virtualenvwrapper
   ```

2. Add the following lines to your shell startup file (`~/.bashrc` or `~/.zshrc`):

   ```bash
   export WORKON_HOME=$HOME/.virtualenvs
   export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
   source /usr/local/bin/virtualenvwrapper.sh
   ```

3. Source the shell startup file:

   ```bash
   source ~/.bashrc  # or source ~/.zshrc
   ```

4. Create a new environment:

   ```bash
   mkvirtualenv myproject
   ```

5. Activate the environment:

   ```bash
   workon myproject
   ```

6. Deactivate the environment:

   ```bash
   deactivate
   ```

### 1.2 PIP and Package Management

**Introduction to PIP**:
PIP is a package management system used to install and manage software packages written in Python. It is the most widely used tool for managing Python packages.

**Basic PIP Commands**:

- Install a package:
  ```bash
  pip install package_name
  ```
- Uninstall a package:
  ```bash
  pip uninstall package_name
  ```
- List installed packages:
  ```bash
  pip list
  ```
- Freeze installed packages:
  ```bash
  pip freeze > requirements.txt
  ```

### 1.3 Installing Necessary Packages

**Installing Jupyter**:

```bash
pip install jupyter
```

**Installing Django**:

```bash
pip install django
```

**Installing Graphene**:

```bash
pip install graphene-django
```

### 1.4 Introduction to Jupyter

**Overview of Jupyter Notebook**:
Jupyter Notebook is an open-source web application that allows you to create and share documents that contain live code, equations, visualizations, and narrative text. It is widely used for data cleaning and transformation, numerical simulation, statistical modeling, data visualization, machine learning, and much more.

**Key Features of Jupyter Notebook**:

- **Interactive Code Execution**: Write and execute code in a web-based environment.
- **Rich Media Support**: Embed images, videos, and HTML elements directly in the notebook.
- **Narrative Text**: Use Markdown to write text, create headings, and format content.
- **Data Visualization**: Integrate with libraries like Matplotlib, Seaborn, and Plotly to create visualizations.
- **Extensibility**: Support for multiple programming languages through kernels (e.g., Python, R, Julia).

For more detailed information and advanced features, refer to the official Jupyter documentation.
