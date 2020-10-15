# FLASK WEB DEVELOPMENT

____

# Introduction 

## Git Commands in Command Line Interface (CLI)

1. Cloning repositories (downloading to computer):

Syntax: ```git clone repositoryName```
    
Example:

```
git clone https://github.com/miguelgrinberg/flasky.git
```

2. 

Syntax: ```git ```

Example:

```
git 
```

3. 

Syntax: ```git ```

Example:

```
git 
```

4. 

Syntax: ```git ```

Example:

```
git 
```

5. 

Syntax: ```git ```

Example:

```
git 
```

6. 

Syntax: ```git ```

Example:

```
git 
```

7. 

Syntax: ```git ```

Example:

```
git 
```

8. 

Syntax: ```git ```

Example:

```
git 
```

### CHPATER 1 - SET UP - Introduction

From time to time, you may want to refresh your local repository from the one on GitHub, where bug fixes and improvements may have been applied. The commands that achieve this are:

```
git fetch --all

git fetch --tags

git reset --hard origin/master
```

The ```git fetch``` commands are used to update the commit history and the tags in your local repository from the remote one on GitHub, but none of this affects the actual source files, which are updated with the ```git reset``` command that follows.

Once again, be aware that any time ```git reset``` is used you will lose any local changes you have made.


Another useful operation is to view all the differences between two versions of the application. This can be very useful to understand a change in detail. From the command line, the ```git diff``` command can do this. For example, to see the difference between revisions 2a and 2b, use:

```git diff 2a 2b```

The differences are shown as a patch, which is not a very intuitive format to review changes if you are not used to working with patch files. You may find that the graphical comparisons shown by GitHub are much easier to read. For example, the differences between revisions 2a and 2b can be viewed on GitHub at https://github.com/ miguelgrinberg/flasky/compare/2a...2b.


### Virtual Environment

The command that creates a virtual environment has the following structure:

```python -m venv virtual-environment-name```

You are now going to create a virtual environment inside the _flasky_ directory. A commonly used convention for virtual environments is to call them ```venv```, but you can use a different name if you prefer. Make sure your current directory is set to _flasky_, and then run this command:

```python -m venv venv```


#### Activating Virtual Environment

If you are using Microsoft Windows Power Shell, the activation command is:

```venv\Scripts\Activate```

When a virtual environment is activated, the location of its Python interpreter is added to the ```PATH``` environment variable in your current command session, which determines where to look for executable files.

After a virtual environment is activated, typing ```python``` at the command prompt will invoke the interpreter from the virtual environment instead of the system-wide interpreter.

#### Desactivating Virtual Environment

When you are done working with the virtual environment, type ```deactivate``` at the command prompt to restore the PATH environment variable for your terminal session and the command prompt to their original states.

# CHAPTER 2 - Basic Application Structure

## Initialization

All Flask applications must create an _application instance_. The web server passes all requests it receives from clients to this object for handling, using a protocol called **Web Server Gateway Interface** (WSGI, pronounced “wiz-ghee”). **The application instance is an object of class Flask**, usually created as follows:

```py
from flask import Flask
app = Flask(__name__)
```

The only required argument to the ```Flask``` class constructor is the name of the main module or package of the application.


## Routes and View Functions

### Routes

Clients such as web browsers send requests to the web server, which in turn sends them to the Flask application instance. The Flask application instance needs to know what code it needs to run for each URL requested, so it keeps a mapping of URLs to Python functions. **The association between a URL and the function that handles it is called a *route***.

The most convenient way to define a **route** in a Flask application is through the ```app.route``` decorator exposed by the application instance.

```py
@app.route('/')
def index():
    return '<h1>Hello World!</h1>'
```

The previous example registers function ```index()``` as the handler for the application’s root URL. While the ```app.route``` decorator is the preferred method to register view functions, Flask also offers a more traditional way to set up the application routes with the ```app.add_url_rule()``` method, which in its most basic form takes three arguments: **the URL, the endpoint name, and the view function**. The following example uses ```app.add_url_rule()``` to register an ```index()``` function that is equivalent to the one shown previously:

```py
def index():
    return '<h1>Hello World!</h1>'

app.add_url_rule('/', 'index', index)
```

### View Functions

Functions like ```index()``` that handle application URLs are called **view functions**. If the application is deployed on a server associated with the _www.example.com_ domain name, then navigating to _http://www.example.com/_ in your browser would trigger ```index()``` to run on the server. The return value of this **view function** is the response the client receives. If the client is a web browser, this response is the document that is displayed to the user in the browser window. _A response returned by a view function can be a simple string with HTML content, but it can also take more complex forms, as you will see later._

If you pay attention to how some URLs for services that you use every day are formed, you will notice that **many have variable sections**.
For example, the URL for your Facebook profile page has the format _https://www.facebook.com/<your-name>_. Flask supports these types of URLs using a special syntax in the ```app.route``` decorator. The following example defines a route that has a dynamic component:

```py
@app.route('/user/<name>')
def user(name):
    return '<h1>Hello, {}!</h1>'.format(name)
```

The dynamic components in routes are strings by default but can also be of different types. For example, the route ```/user/<int:id>``` would match only URLs that have an integer in the id dynamic segment, such as ```/user/123```. Flask supports the types ```string```, ```int```, ```float```, and ```path``` for routes. The ```path``` type is a special string type that can include forward slashes, unlike the string type.


#### A complete Flask application

The _hello.py_ application script shown in Example 2-1 defines an application instance and a single route and view function, as described earlier.

Example 2-1. hello.py: 

```py
from flask import Flask
app = Flask(__name__)

@app.route('/')
def index():
    return '<h1>Hello World!</h1>'
```


#### Running App

**Flask applications include a development web server that can be started with the ```flask run``` command. This command looks for the name of the Python script that contains the application instance in the ```FLASK_APP``` environment variable.**

The ```flask``` command is installed by Flask, not your application; it must be told where to find your application in order to use it. The ```FLASK_APP``` environment variable is used to specify how to load the application.

Unix Bash (Linux, Mac, etc.):

```
$ export FLASK_APP=hello
$ flask run
```

Windows CMD:

```
set FLASK_APP=hello
flask run
```

Windows PowerShell:

```
$env:FLASK_APP="hello.py"
flask run
```

With the server running, open your web browser and type ```http://localhost:5000/``` in the address bar


_Additional Note:_

>The Flask development web server can also be started programmatically by invoking the ```app.run()``` method. Older versions of Flask that did not have the ```flask``` command required the server to be started by running the application’s main script, which had to include the following snippet at the end:

```py
if __name__ == '__main__':
app.run()
```

>While the ```flask run``` command makes this practice unnecessary, the ```app.run()``` method can still be useful on certain occasions, such as unit testing.


### Flask application with dynamic route

The second version of the application, adds a second route that is dynamic. When you visit the dynamic URL in your browser, you are presented with a personalized greeting that includes the name provided in the URL.

_hello.py_: Flask application with a dynamic route

```py
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return '<h1>Hello World!</h1>'

@app.route('/user/<name>')
def user(name):
    return '<h1>Hello, {}!</h1>'.format(name)
```

### Debug Mode

Flask applications can optionally be executed in **debug mode**. In this mode, two modules of the development server called the **reloader** and the **debugger** are enabled by default.

When the **reloader** is enabled, Flask watches all the source code files of your project and automatically restarts the server when any of the files are modified. Having a server running with the **reloader** enabled is extremely useful during development, because every time you modify and save a source file, the server automatically restarts and picks up the change.

The **debugger** is a web-based tool that appears in your browser when your application raises an unhandled exception. The web browser window transforms into an interactive stack trace that allows you to inspect source code and evaluate expressions in any place in the call stack

If you want to control debug mode separately, use ```FLASK_DEBUG```. The value ```1``` enables it, ```0``` disables it.


#### Running debugger:

For Windows Power Shell:

```
$env:FLASK_APP="hello.py"
$env:FLASK_DEBUG=1
flask run
```

_Additional Note:_
>Never enable debug mode on a production server. The debugger in particular allows the client to request remote code execution, so it makes your production server vulnerable to attacks.


### Command Line Options

The ```flask``` command supports a number of options. To see what’s available, you can run ```flask --help``` or just ```flask```

The ```flask shell``` command is used to start a Python shell session in the context of the application. You can use this session to run maintenance tasks or tests, or to debug issues. 

You are already familiar with the ```flask run``` command, which, as its name implies, runs the application with the development web server. This command has many options:

```flask run --help```

The ```flask run --host``` argument is particularly useful because **it tells the web server what network interface to listen to for connections from clients**. By default, Flask’s development web server listens for connections on localhost, so only connections originating from the computer running the server are accepted. **The following command makes the web server listen for connections on the public network interface, enabling other computers in the same network to connect as well**:

```
flask run --host 0.0.0.0
* Serving Flask app "hello"
* Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

The web server should now be accessible from any computer in the network at _http://a.b.c.d:5000_, where _a.b.c.d_ is the **IP address of the computer running the server in your network**.


### Application and Requests Contexts

**To avoid cluttering view functions with lots of arguments that may not always be needed, Flask uses contexts to temporarily make certain objects globally accessible.** Thanks to contexts, view functions like the following one can be written:

```py
from flask import request

@app.route('/')
def index():
    user_agent = request.headers.get('User-Agent')
    return '<p>Your browser is {}</p>'.format(user_agent)
```

**IMPORTANT!**

Note how in this view function, ```request``` is used as if it were a global variable. In reality, ```request``` cannot be a global variable; in a multithreaded server several threads can be working on different requests from different clients all at the same time, so each thread needs to see a different object in ```request```. **Contexts enable Flask to make certain variables globally accessible to a thread without interfering with the other threads**.


_Additional Note:_

>A thread is the smallest sequence of instructions that can be managed independently. Multithreaded web servers start a pool of threads and select a thread from the pool to handle each incoming request.


#### Flaks Contexts

____

[Contexts in Flask](https://overiq.com/flask-101/contexts-in-flask/#:~:text=Flask%20uses%20something%20called%20Contexts,Application%20Context.)
____

**IMPORTANT!**

There are two contexts in Flask: the **application context** and the **request context**.

Variable name       | Context              | Description

```current_app``` -> Application context -> The application instance for the active application.

```g``` ->           Application context -> An object that the application can use for temporary storage during the handling of a request.
                     This variable is reset with each request.

```request``` ->     Request context -> The request object, which encapsulates the contents of an HTTP request sent by the client.

```session``` ->     Request context -> The user session, a dictionary that the application can use to store values that are “remembered” between requests.


**IMPORTANT!**

Flask activates (or _pushes_) the application and request contexts before dispatching a request to the application, and removes them after the request is handled. When the application context is pushed, the ```current_app``` and ```g``` variables become available to the thread.

Likewise, when the request context is pushed, ```request``` and ```session``` become available as well. If any of these variables are accessed without an active application or request context, an error is generated.


#### Request Dispatching

When the application receives a request from a client, it needs to find out what view function to invoke to service it. For this task, Flask looks up the URL given in the request in the application’s URL *map*, which contains a mapping of URLs to the view functions that handle them.
Flask builds this map using the data provided in the ```app.route``` decorator.

>Basicamente Flask crea un **indice** de URLs

To see what the URL map in a Flask application looks like, you can inspect the map created for ```hello.py``` in the Python shell.

```py
(venv) python
>>> from hello import app
>>> app.url_map

Map([<Rule '/' (HEAD, OPTIONS, GET) -> index>,
<Rule '/static/<filename>' (HEAD, OPTIONS, GET) -> static>,
<Rule '/user/<name>' (HEAD, OPTIONS, GET) -> user>])
```

1. The ```/``` and ```/user/<name>``` routes were defined by the ```app.route``` decorators in the application. The ```/static/<filename>``` route is a special route added by Flask to give access to static files.

2. The ```(HEAD, OPTIONS, GET)``` elements shown in the URL map are the request methods that are handled by the routes. The HTTP specification defines that all requests are issued with a method, which normally indicates what action the client is asking the server to perform. Flask attaches methods to each route so that different request methods sent to the same URL can be handled by different view functions.

The ```HEAD``` and ```OPTIONS``` methods are managed automatically by Flask, so in practice it can be said that in this application the three routes in the URL map are attached to the GET method, which is used when the client wants to request information such as a web page.


_Additional Note:_

>```GET```: solicita una representación de un recurso específico. Las peticiones que usan el método ```GET``` sólo deben recuperar datos.

>```HEAD```: pide una respuesta idéntica a la de una petición ```GET```, pero sin el cuerpo de la respuesta.

>```OPTIONS```: es utilizado para describir las opciones de comunicación para el recurso de destino.


### The Request Object

You have seen that Flask exposes a request object as a context variable named ```request```. **This is an extremely useful object that contains all the information that the client included in the HTTP request.** 
The following table enumerates the most commonly used attributes and methods of the Flask request object.

Attribute or Method | Description

```form        ```    A dictionary with all the form fields submitted with the request.
```args        ```    A dictionary with all the arguments passed in the query string of the URL.
```values      ```    A dictionary that combines the values in form and args.
```cookies     ```    A dictionary with all the cookies included in the request.
```headers     ```    A dictionary with all the HTTP headers included in the request.
```files       ```    A dictionary with all the file uploads included with the request.
```get_data()  ```    Returns the buffered data from the request body.
```get_json()  ```    Returns a Python dictionary with the parsed JSON included in the body of the request.
```blueprint   ```    The name of the Flask blueprint that is handling the request.
```endpoint    ```    The name of the Flask endpoint that is handling the request. Flask uses the name of the view function as the endpoint name for a route.
```method      ```    The HTTP request method, such as GET or POST.
```scheme      ```    The URL scheme (http or https).
```is_secure() ```    Returns True if the request came through a secure (HTTPS) connection.
```host        ```    The host defined in the request, including the port number if given by the client.
```path        ```    The path portion of the URL.
```query_string```    The query string portion of the URL, as a raw binary value.
```full_path   ```    The path and query string portions of the URL.
```url         ```    The complete URL requested by the client.
```base_url    ```    Same as url, but without the query string component.
```remote_addr ```    The IP address of the client.
```environ     ```    The raw WSGI environment dictionary for the request.


### Request Hooks

Sometimes it is useful to execute code before or after each request is processed. **For example, at the start of each request it may be necessary to create a database connection or authenticate the user making the request. Instead of duplicating the code that performs these actions in every view function, Flask gives you the option to register common functions to be invoked before or after a request is dispatched**.

Request hooks are implemented as decorators. These are the **four hooks supported** by Flask:

1. ```before_request```: Registers a function to run **before each request**.

2. ```before_first_request```: Registers a function to run only **before the first request** is handled. This can be a **convenient way to add server initialization tasks**.

3. ```after_request```: Registers a function to **run after each request**, but only **if no unhandled exceptions occurred**.

4. ```teardown_request```: Registers a function to **run after each request, even if unhandled exceptions occurred**.

_Additional Note:_
>**Request hooks** porque en vez de existir en cada función, se *hookean* desde afuera a esas funciones que requieren ese **Request Hook**


A common pattern to share data between request hook functions and view functions is to use the ```g``` context global as storage. For example, a ```before_request``` handler can load the logged-in user from the database and store it in ```g.user```. Later, when the view function is invoked, it can retrieve the user from there.


### Responses

When Flask invokes a view function, it expects its return value to be the response to the request. In most cases the response is a simple string that is sent back to the client as an HTML page. But the HTTP protocol requires more than a string as a response to a request. A very important part of the HTTP response is the status code, which Flask by default sets to 200, the code that indicates that the request was carried out successfully.

**When a view function needs to respond with a different status code, it can add the numeric code as a second return value after the response text**. For example, the following view function returns a 400 status code, the code for a bad request error:

```py
@app.route('/')
def index():
    return '<h1>Bad Request</h1>', 400
```

Instead of returning one, two, or three values as a tuple, **Flask view functions have the option of returning a *response object***. The ```make_response()``` function takes one, two, or three arguments, the same values that can be returned from a view function, and returns an equivalent response object. **Sometimes it is useful to generate the response object inside the view function, and then use its methods to further configure the response.**

The following example creates a response object and then sets a cookie in it:


```py
from flask import make_response

@app.route('/')
def index():
    response = make_response('<h1>This document carries a cookie!</h1>')
    response.set_cookie('answer', '42')
    return response
```

_Additional Note:_
>**What are cookies?**
>A cookie is a small amount of text data given to a web browser by a web server. The data is then stored on the visitor's hard drive and returned to the specific web server each time the browser requests a page from that server. The main purpose of cookies is to assign a unique identifier to each visitor to a specific website, which allows that website to track that visitor as they navigate through that site. The name cookie is derived from UNIX objects called magic cookies. These are tokens that are attached to a user or program and change depending on the areas entered by the user or program.

>**Cookies can be either temporary or persistent**. A temporary cookie, commonly referred to as a session cookie, is stored only as long as the user is actively using the website. Once the browser is closed or the session is expired the cookie is deleted from the local hard drive. In contrast, a persistent cookie is stored on the user's hard drive even after the browser is closed. If the user returns to the website in the following days, the server would recognize the cookie and be able to combine the data from the previous visit with the data from the current visit.

>**Cookies are truly an important tool**. *Cookies allow users to conveniently store passwords and other information. They also allow companies to understand the navigation of their site in order to improve the site to meet users' needs.* However, in the effort to dispel confidentiality fears, it is important to note what cookies cannot do.:
>* Cookies cannot execute programs on a users' computer.
>* Cookies cannot collect confidential personal information


Most commonly used attributes and methods available in response objects:

Attribute or Method | Description

```status_code```      The numeric HTTP status code
```headers```          A dictionary-like object with all the headers that will be sent with the response
```set_cookie()```     Adds a cookie to the response
```delete_cookie()```  Removes a cookie
```content_length```   The length of the response body
```content_type```     The media type of the response body
```set_data()```       Sets the response body as a string or bytes value
```get_data()```       Gets the response body


#### Redirect response

There is a special type of response called a ```redirect```. This response does not include a page document; it just gives the browser a new URL to navigate to. A very common use of redirects is when working with web forms.

A ```redirect``` is typically indicated with a **302 response status code and the URL to go to** given in a ```Location``` header. A ```redirect``` response can be generated manually with a three-value return or with a response object, but given its frequent use, Flask provides a ```redirect()``` helper function that creates this type of response.

```py
from flask import redirect

@app.route('/')
def index():
    return redirect('http://www.example.com')
```

#### Abort response

Another special response is issued with the ```abort()``` function, which is used for error handling. The following example **returns status code 404 if the id dynamic argument given in the URL does not represent a valid user**:

```py
from flask import abort

@app.route('/user/<id>')
def get_user(id):
    user = load_user(id)
    if not user:
        abort(404)
    return '<h1>Hello, {}</h1>'.format(user.name)
```

_Additional Note:_
>Flask is designed to be extended. It intentionally stays out of areas of important functionality such as database and user authentication, giving you the freedom to select the packages that fit your application the best, or to write your own if you so desire.


# CHAPTER 3 - Templates

## Introduction

Flask view functions have two completely independent purposes disguised(_disfrazado_) as one, which creates a problem:

* **Generate a response to a request:** For the simplest requests this is enough, but in many cases a request also triggers a change in the state of the application, and the view function is where this change is generated.


*Example with steps:*

1. Consider a user who is registering a new account on a website. The user types an email address and a password in a web form and clicks the Submit button.

2. On the server, a request with the data provided by the user arrives

3. Flask dispatches it to the view function that handles registration requests. 

4. This view function needs to talk to the database to get the new user added (*business logic*), and then generate a response
to send back to the browser that includes a success or failure message (*presentation logic*). 

These two types of tasks are formally called _business logic_ and _presentation logic_, respectively.

Mixing business and presentation logic leads to code that is hard to understand and maintain. Imagine having to build the HTML code for a large table by concatenating data obtained from the database with the necessary HTML string literals. **Moving the presentation logic into templates helps improve the maintainability of the application.**

### What's a TEMPLATE?

**A template is a file that contains the text of a ```response```, with placeholder variables for the dynamic parts that will be known only in the context of a request. The process that replaces the variables with actual values and returns a final response string is called *rendering***. 

For the task of rendering templates, **Flask uses a powerful template engine called Jinja2**.

### Jinja2 Template Engine

In its simplest form, a Jinja2 template is a file that contains the text of a response.

The response returned by the ```user()``` view function has a dynamic component, which is represented by a variable. The example shows the template that implements this response.

Example 1:

_templates/user.html_: Jinja2 template

```html
<h1>Hello, {{ name }}!</h1>
```

Example 2:

```py
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/user/<name>')
def user(name):
    return render_template('user.html', name=name)
```

The function ```render_template()``` provided by Flask integrates the Jinja2 template engine with the application. This function takes the filename of the template as its first argument. Any additional arguments are key-value pairs that represent actual values for variables referenced in the template such in the last example, where the second template is receiving a name variable.

**IMPORTANT!**

Keyword arguments like ```name=name``` in the previous example are fairly common, but they may seem confusing and hard to understand if you are not used to them. **The “name” on the left side represents the argument name, which is used in the placeholder written in the template. The “name” on the right side is a variable in the current scope that provides the value for the argument of the same name**. While this is a common pattern, using the same variable name on both sides is not required.

#### Variables

Jinja2 recognizes variables of any type, even complex types such as lists, dictionaries, and objects. The following are some more examples of variables used in templates:

```html
<p>A value from a dictionary: {{ mydict['key'] }}.</p>

<p>A value from a list: {{ mylist[3] }}.</p>

<p>A value from a list, with a variable index: {{ mylist[myintvar] }}.</p>

<p>A value from an object's method: {{ myobj.somemethod() }}.</p>
```

Variables can be modified with _filters_, which are added after the variable name with a pipe character as separator. For example, the following template shows the ```name``` variable capitalized:

```html
Hello, {{ name|capitalize }}
``` 

Commonly used filters that come with Jinja2.

Filter name     |   Description

```safe```          Renders the value without applying escaping
```capitalize```    Converts the first character of the value to uppercase and the rest to lowercase
```lower```         Converts the value to lowercase characters
```upper```         Converts the value to uppercase characters
```title```         Capitalizes each word in the value
```trim```          Removes leading and trailing whitespace from the value
```striptags```     Removes any HTML tags from the value before rendering

_Additional Note:_
>The ```safe``` filter is interesting to highlight. By default Jinja2 escapes all variables for security purposes. For example, if a variable is set to the value '<h1>Hello</h1>', Jinja2 will render the string as ```'&lt;h1&gt;Hello&lt;/h1&gt;'```, which will cause the h1 element to be displayed and not interpreted by the browser. Many times it is necessary to display HTML code stored in variables, and for those cases the safe filter is used.

[Jinja 2 Built-In Filters](https://jinja.palletsprojects.com/en/2.11.x/templates/#builtin-filters)


### Control Structures

Jinja2 offers several control structures that can be used to alter the flow of the template. The following example shows how conditional statements can be entered in a template:


```
{% if user %}
    Hello, {{ user }}!
{% else %}
    Hello, Stranger!
{% endif %}
```

1. Another common need in templates is to render a list of elements:

```html
<ul>
    {% for comment in comments %}
        <li>{{ comment }}</li>
    {% endfor %}
</ul>
```

2. Jinja2 also supports _macros_, which are similar to functions in Python code. For example:

```html
<!-- Define de macro -->
{% macro render_comment(comment) %}
    <li>{{ comment }}</li>
{% endmacro %}

<!-- implement the macro -->
<ul>
    {% for comment in comments %}
        {{ render_comment(comment) }}
    {% endfor %}
</ul>
```

To make macros more reusable, they can be stored in standalone files that are then _imported_ from all the templates that need them:

```html
{% import 'macros.html' as macros %}
<ul>
    {% for comment in comments %}
        {{ macros.render_comment(comment) }}
    {% endfor %}
</ul>
```

3. Portions of template code that need to be repeated in several places can be stored in a separate file and _included_ from all the templates to avoid repetition:

```html
    {% include 'common.html' %}
```

4. Yet another powerful way to reuse is through template inheritance, which is similar to class inheritance in Python code. First, a base template is created with the name _base.html_:

```html
<html>
    <head>
    {% block head %}
    <title>{% block title %}{% endblock %} - My Application</title>
    {% endblock %}
</head>
<body>
    {% block body %}
    {% endblock %}
</body>
</html>
```

**Base templates define blocks that can be overridden by derived templates**. The Jinja2 ```block``` and ```endblock``` directives define blocks of content that are added to the base template. In this example, there are blocks called ```head```, ```title```, and ```body```. The following example is a derived template of the base template:

```html
{% extends "base.html" %}

{% block title %}Index{% endblock %}

{% block head %}
{{ super() }}
    <style>
    </style>
{% endblock %}

{% block body %}
<h1>Hello, World!</h1>
{% endblock %}
```

The ```extends``` directive declares that this template derives from _base.html_. This directive is followed by new definitions for the three blocks defined in the base template, which are inserted in the proper places. *When a block has some content in both the base and derived templates, the content from the derived template is used*. Within this block, **the derived template can call ```super()``` to reference the contents of the block in the base template**.

### Bootstrap Integration with Flask-Bootstrap

The naive approach to integrating Bootstrap with the application is to make all the necessary changes to the HTML templates, following the recommendations given by the Bootstrap documentation. But this is an area where the use of a Flask extension makes an integration task much simpler, while helping keep these changes nicely organized.

The extension is called Flask-Bootstrap, and it can be installed with pip:

```(venv) pip install flask-bootstrap```

Flask extensions are initialized at the same time the application instance is created.

```py
from flask_bootstrap import Bootstrap
# ...
bootstrap = Bootstrap(app)
```

**IMPORTANT!**

The extension is usually imported from a ```flask_<name>``` package, where ```<name>``` is the extension name. Most Flask extensions follow one of two consistent patterns for initialization. In the last example, **the extension is initialized by passing the application instance as an argument in the constructor.**

Once Flask-Bootstrap is initialized, a base template that includes all the Bootstrap files and general structure is available to the application. The application then takes advantage of Jinja2’s template inheritance to extend this base template.


_Additional Note:_
>This blocks (structure) are the ones contained by the base bootstrap template (and more):
```
{% block doc -%} {%- block html %} {%- block head %} {%- block metas %} {%- endblock metas %} {%- block styles %} {%- endblock styles %} {%- endblock head %} {% block body -%} {% block navbar %} {%- endblock navbar %} {% block content -%} {%- endblock content %} {% block scripts %} {%- endblock scripts %} {%- endblock body %} {%- endblock html %} {% endblock doc -%}
```
>[Base Bootstrap Templates - VENV File](file:///C:/Users/Marcos/flasky/venv/Lib/site-packages/flask_bootstrap/templates/bootstrap/base.html)


```html
{% extends "bootstrap/base.html" %}

{% block title %}Flasky{% endblock %}

{% block navbar %}
<div class="navbar navbar-inverse" role="navigation">
    <div class="container">
        <div class="navbar-header">
            <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                <span class="sr-only">Toggle navigation</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>
            <a class="navbar-brand" href="/">Flasky</a>
        </div>
        <div class="navbar-collapse collapse">
            <ul class="nav navbar-nav">
                <li><a href="/">Home</a></li>
            </ul>
        </div>
    </div>
</div>
{% endblock %}

{% block content %}
<div class="container">
    <div class="page-header">
        <h1>Hello, {{ name }}!</h1>
    </div>
</div>
{% endblock %}
```

The Jinja2 ```extends``` directive implements the template inheritance by referencing _bootstrap/base.html_ from Flask-Bootstrap. The base template from Flask-Bootstrap provides a skeleton web page that includes all the Bootstrap CSS and JavaScript files.

Block name | Description

```doc```           The entire HTML document
```html_attribs```  Attributes inside the ```<html>``` tag
```html```          The contents of the ```<html>``` tag
```head```          The contents of the ```<head>``` tag
```title```         The contents of the ```<title>``` tag
```metas```         The list of ```<meta>``` tags
```styles```        CSS definitions
```body_attribs```  Attributes inside the ```<body>``` tag
```body```          The contents of the ```<body>``` tag
```navbar```        User-defined navigation bar
```content```       User-defined page content
```scripts```       JavaScript declarations at the bottom of the document

Many of the blocks are used by Flask-Bootstrap itself, so overriding them directly would cause problems. For example, the ```styles``` and ```scripts``` blocks are where the Bootstrap CSS and JavaScript files are declared. If the application needs to add its own content to a block that already has some content, then Jinja2’s ```super()``` function must be used. For example, this is how the ```scripts``` block would need to be written in the derived template to add a new JavaScript file to the document:

```html
{% block scripts %}
{{ super() }}
    <script type="text/javascript" src="my-script.js"></script>
{% endblock %}
```

### Custom Errors Pages

When you enter an invalid route in your browser’s address bar, you get a code 404 error page. Flask allows an application to define custom error pages that can be based on templates, like regular routes. 

The two most common error codes are 404, triggered when the client requests a page or route that is not known, and 500, triggered when there is an unhandled exception in the application.

```py
@app.errorhandler(404):
def page_not_found(e):
    return render_template('404.html'), 404

@app.errorhandler(500):
def page_not_found(e):
    return render_template('500.html'), 500
```

Error handlers return a response, like view functions, but they also need to return the numeric status code that corresponds to the error, which Flask conveniently accepts as a second return value. The templates referenced in the error handlers need to be written.

Jinja2’s template inheritance can help with this. In the same way Flask-Bootstrap provides a base template with the basic layout of the page, the application can define its own base template with a uniform page layout that includes the navigation bar and leaves the page content to be defined in derived templates.

```html
{% extends "bootstrap/base.html" %}
{% block title %}Flasky{% endblock %}
{% block navbar %}
<div class="navbar navbar-inverse" role="navigation">
    <div class="container">
        <div class="navbar-header">
            <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                <span class="sr-only">Toggle navigation</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>
            <a class="navbar-brand" href="/">Flasky</a>
        </div>
        <div class="navbar-collapse collapse">
            <ul class="nav navbar-nav">
                <li><a href="/">Home</a></li>
            </ul>
        </div>
    </div>
</div>
{% endblock %}
{% block content %}
<div class="container">
    {% block page_content %}{% endblock %}
</div>
{% endblock %}
```


The ```content``` block of this template is just a container ```<div>``` element that wraps a new empty block called ```page_content```, which derived templates can define. The templates of the application will now inherit from this template instead of directly from Flask-Bootstrap.


_404.html_ template example (inherits from _template/base.html_):

```html
{% extends "base.html" %}
{% block title %}Flasky - Page Not Found{% endblock %}
{% block page_content %}
<div class="page-header">
    <h1>Not Found</h1>
</div>
{% endblock %}
```

The _templates/user.html_ template can now be simplified by making it inherit from the base template:

```html
{% extends "base.html" %}
{% block title %}Flasky{% endblock %}
{% block page_content %}
<div class="page-header">
    <h1>Hello, {{ name }}!</h1>
</div>
{% endblock %}
```

### Links

Any application that has more than one route will invariably need to include links that connect the different pages, such as in a navigation bar.

Writing the URLs as links directly in the template is trivial for simple routes, but for dynamic routes with variable portions it can get more complicated to build the URLs right in the template. Also, URLs written explicitly create an unwanted dependency on the routes defined in the code. If the routes are reorganized, links in templates may break.

**IMPORTANT!**

To avoid these problems, Flask provides the ```url_for()``` helper function, **which generates URLs from the information stored in the application’s URL map.**

#### Static URLs

This function takes the view function name as its single argument and returns its URL. For example, in the current version of _hello.py_ the call ```url_for('index')``` would return ```/```, the root URL of the application. Calling ```url_for('index', _external=True)``` would instead return an absolute URL, which in this example is _http://localhost:5000/_. 

**Relative URLs are sufficient when generating links that connect the different routes of the application. Absolute URLs are necessary only for links that will be used outside of the web browser, such as when sending links by email**. 

#### Dynamic URLs

**Dynamic URLs can be generated with ```url_for()``` by passing the dynamic parts as keyword arguments**. For example, ```url_for('user', name='john', _external=True)``` would return http://localhost:5000/user/john. Keyword arguments sent to ```url_for()``` are not limited to arguments used by dynamic routes. The function will add any arguments that are not dynamic to the query string. For example, ```url_for('user', name='john', page=2, version=1)``` would return ```/user/john?page=2&version=1```.


### Static Files

Web applications are not made of Python code and templates alone. _Most applications also use static files such as images, JavaScript source files, and CSS files that are all referenced from the HTML code in templates._ 

**IMPORTANT!**

You may recall that when the _hello.py_ application’s URL map was inspected in Chapter 2, a static entry appeared in it. **Flask automatically supports static files by adding a special route to the application defined as ```/static/<filename>```.** For example, a call to ```url_for('static', filename='css/styles.css', _external=True)``` would return ```http://localhost:5000/static/css/styles.css```.

In its default configuration, Flask looks for static files in a subdirectory called _static_ located in the application’s root folder. Files can be organized in subdirectories inside this folder if desired. 


### Localization of Dates and Times with Flask-Moment

Handling of dates and times in a web application is not a trivial problem when users work in different parts of the world.

The server needs uniform time units that are independent of the location of each user, so typically _Coordinated Universal Time_ (UTC) is used.
For users, however, seeing times expressed in UTC can be confusing, as users always expect to see dates and times presented in their local time and formatted according to the customs of their region.

An elegant solution that allows the server to work exclusively in UTC (_Universal Time Coordination_) is to send these time units to the web browser, where they are converted to local time and rendered using JavaScript. There is library written in JavaScript that renders dates and times in the browser called Moment.js. Flask-Moment is an extension for Flask applications that makes the integration of Moment.js into Jinja2 templates very easy.

Install: ```pip install flask-moment```

Initialize: 

```py
from flask_moment import Moment
moment = Moment(app)
```

Flask-Moment depends on jQuery.js in addition to Moment.js. **These two libraries need to be included somewhere in the HTML document**—either directly or through the helper functions provided by the extension, which reference to _content delivery network_ (CDN). Because Bootstrap already includes _jQuery.js_, only _Moment.js_ needs to be added in this case. The example shows how this library is loaded in the scripts block of the template, while also preserving the original contents of the block provided by the base template. Note that since this is a predefined block in the Flask-Bootstrap base template, the location in _templates/base.html_ where this block is inserted does not matter.


1. Add to _template/base.html_:

```html
{% block scripts %}
{{ super() }}
{{ moment.include_moment() }}
{% endblock %}
```

2. Add to _hello.py_:

```py
from flask_moment import Moment
from datetime import datetime

# Instanciate flask app
# Instanciate flask-bootstrap object
moment = Moment(app)

@app.route('/')
def index():
    return render_template('index.html', current_time=datetime.utcnow())
```

3. Add to _template/index.html_

```html
<p>The local date and time is {{ moment(current_time).format('LLL') }}.</p>
<p>That was {{ moment(current_time).fromNow(refresh=True) }}</p>
```

**About datetime ```format()```:**

The argument determines the rendering style, from ```'L'``` to ```'LLLL'``` for four different levels of verbosity. The ```format()``` function
can also accept a long list of custom format specifiers.


**About fromNow():**

The ```fromNow()``` renders a relative timestamp(_marca de tiempo_) and automatically refreshes it as time passes. Initially this timestamp will be shown as _“a few seconds ago,”_ but the ```refresh=True``` option will keep it updated as time passes, so if you leave the page open for a few minutes you will see the text changing to _“a minute ago,”_ then _“2 minutes ago,”_ and so on.


Flask-Moment implements the ```format()```, ```fromNow()```, ```fromTime()```, ```calendar()```, ```valueOf()```, and ```unix()``` methods from Moment.js.

[Consult the Moment.js documentation to learn about all the formatting options](https://momentjs.com/docs/#/displaying/)


The timestamps rendered by Flask-Moment can be localized to many languages. A language can be selected in the template by passing the two-letter language code to function ```locale()```, right after the Moment.js library is included. For example, here is how to configure Moment.js to use Spanish:

```
{% block scripts %}
{{ super() }}
{{ moment.include_moment() }}
{{ moment.locale('es') }}
{% endblock %}
```


# CHAPTER 4 - Web Forms

The templates we worked with in are so far _unidirectional_: they allow information to flow from the server to the user. 

There is also a need to have information that flows in the other direction, with the user providing data that the server accepts and processes. With HTML, it is possible to create web forms, in which users can enter information. The form data is then submitted by the web browser to the server, typically in the form of a ```POST``` request. **The Flask ```request```  object, exposes all the information sent by the client in a ```request``` and, in particular for ```POST``` requests containing form data, provides access to the user information through ```request.form```.**

When handling web forms, there are a number of tasks that can become tedious and repetitive. Two good examples are the generation of HTML code for the forms and the validation of the submitted form data.

## Flask-WTF

The _Flask-WTF_ extension makes working with web forms a much more pleasant experience. This extension is a Flask integration wrapper around the framework-agnostic WTForms package.

Flask-WTF install:

```(venv) pip install flask-wtf```

### Secret Key

**Flask-WTF** does not need to be initialized at the application level, but it **expects the application to have a _secret key_ configured**. A **secret key is a string with any random and unique content that is used as an encryption or signing key to improve the security of the application** in several ways. Flask uses this key to protect the contents of the user session against tampering(_manipulación_)

```py
app = Flask(__name__)
app.config['SECRET_KEY'] = 'hard to guess string'
```

[```app.config``` Documentation](https://flask.palletsprojects.com/en/1.1.x/config/)


The ```app.config``` dictionary is a general-purpose place to store configuration variables used by Flask, extensions, or the application itself. Configuration values can be added to the ```app.config``` object using standard dictionary syntax.

Flask-WTF requires a secret key to be configured in the application because this key is part of the mechanism the extension uses to protect all forms against _cross-site request forgery_ (CSRF) attacks.

A CSRF attack occurs when a malicious website sends requests to the application server on which the user is currently logged in. Flask-WTF
generates security tokens for all forms and stores them in the user session, which is protected with a cryptographic signature generated from the secret key.

### Form Classes

**When using Flask-WTF, each web form is represented in the server by a class that inherits from the class ```FlaskForm```**. The class defines the list of fields in the form, each represented by an object. **Each field object can have one or more validators attached** which checks whether the data submitted by the user is valid.

```py
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
from wtforms.validators import DataRequired

class NameForm(FlaskForm):
    name = StringField('What is your name?', validators=[DataRequired()])
    submit = SubmitField('Submit')
```

The fields in the form are defined as class variables, and each class variable is assigned an object associated with the field type. In this example, the ```NameForm``` form has a text field called ```name``` and a submit button called ```submit```. The ```StringField``` class represents an HTML ```<input>``` element with a ```type="text"``` attribute. The ```SubmitField``` class represents an HTML ```<input>``` element with a ```type="submit"``` attribute. **The first argument to the field constructors is the label that will be used when rendering the form to HTML.**

The optional ```validators``` argument included in the ```StringField``` constructor defines a list of checkers that will be applied to the data submitted by the user before it is accepted. The ```DataRequired()``` validator ensures that the field is not submitted empty.

**List of standard HTML fields supported by WTForms:**

[Fields - WTForms Documentation](https://wtforms.readthedocs.io/en/stable/fields/)

Field type | Description

```BooleanField```          Checkbox with True and False values
```DateField```             Text field that accepts a datetime.date value in a given format
```DateTimeField```         Text field that accepts a datetime.datetime value in a given format
```DecimalField```          Text field that accepts a decimal.Decimal value
```FileField```             File upload field
```HiddenField```           Hidden text field
```MultipleFileField```     Multiple file upload field
```FieldList```             List of fields of a given type
```FloatField```            Text field that accepts a floating-point value
```FormField```             Form embedded as a field in a container form
```IntegerField```          Text field that accepts an integer value
```PasswordField```         Password text field
```RadioField```            List of radio buttons
```SelectField```           Drop-down list of choices
```SelectMultipleField```   Drop-down list of choices with multiple selection
```SubmitField```           Form submission button
```StringField```           Text field
```TextAreaField```         Multiple-line text field


**List of WTForms built-in validators:**

[Validators - WTForms Documentation](https://wtforms.readthedocs.io/en/2.2.1/validators/)

Validator | Description

```DataRequired```      Validates that the field contains data after type conversion
```Email```             Validates an email address
```EqualTo```           Compares the values of two fields; useful when requesting a password to be entered twice for confirmation
```InputRequired```     Validates that the field contains data before type conversion
```IPAddress```         Validates an IPv4 network address
```Length```            Validates the length of the string entered
```MacAddress```        Validates a MAC address
```NumberRange```       Validates that the value entered is within a numeric range
```Optional```          Allows empty input in the field, skipping additional validators
```Regexp```            Validates the input against a regular expression
```URL```               Validates a URL
```UUID```              Validates a UUID
```AnyOf```             Validates that the input is one of a list of possible values
```NoneOf```            Validates that the input is none of a list of possible values


### HTML Rendering of Forms

Assuming that the view function passes a ```NameForm``` instance to the template as an argument named ```form```, the template can generate a simple HTML form as follows:

```html
<form method="POST">
{{ form.hidden_tag() }}
{{ form.name.label }} {{ form.name(id='my-text-field') }}
{{ form.submit() }}
</form>
```

But even with HTML attributes, the effort required to render a form in this way and make it look good is significant, so it is best to leverage Bootstrap’s own set of form styles whenever possible. The Flask-Bootstrap extension provides a high-level helper function that renders an entire Flask-WTF form using Bootstrap’s predefined form styles. Using Flask-Bootstrap, the previous form can be rendered as follows:

```
{% import "bootstrap/wtf.html" as wtf %}
{{ wtf.quick_form(form) }}
```

The import directive works in the same way as regular Python scripts do and allows template elements to be imported and used in many templates. The imported _bootstrap/wtf.html_ file defines helper functions that render Flask-WTF forms using Bootstrap. The ```wtf.quick_form()``` function takes a Flask-WTF form object and renders it using default Bootstrap styles.


Example: 

_Change ```index()``` view function to:_

```py
@app.route('/', methods=['GET', 'POST'])
def index():
    name = None
    form = NameForm()
    if form.validate_on_submit():
        name = form.name.data
        form.name.data = ''
    return render_template('index.html', form=form, name=name)
```

_Change template/index.html to:_

```html
{% extends "base.html" %}
{% import "bootstrap/wtf.html" as wtf %}
{% block title %}Flasky{% endblock %}
{% block page_content %}
<div class="page-header">
    <h1>Hello, {% if name %}{{ name }}{% else %}Stranger{% endif %}!</h1>
</div>
{{ wtf.quick_form(form) }}
{% endblock %}
```

The content area of the template now has two sections: 

1. _The first section is a page header that shows a greeting:_ Here a template conditional is used. Conditionals in Jinja2 have the format ```{% if condition %}...{% else %}...{% endif %}```. 

* If the condition evaluates to ```True```, then what appears between the ```if``` and ```else``` directives is added to the rendered template.

* If the condition evaluates to ```False```, then what’s between the ```else``` and ```endif``` is rendered instead. The purpose of this is to render ```Hello, {{ name }}!``` when the ```name``` template variable is defined, or the string ```Hello, Stranger!``` when it is not. 

2. The second section of the content renders the ```NameForm``` form using the ```wtf.quick_form()``` function.


### Form Handling in View Functions

In the new version of _hello.py_, the ```index()``` view function will have two tasks. 

1. First it will render the form.
2. Second it will receive the form data entered by the user.

```py
@app.route('/', methods=['GET', 'POST'])
def index():
    name = None
    form = NameForm()
    if form.validate_on_submit():
        name = form.name.data
        form.name.data = ''
    return render_template('index.html', form=form, name=name)
```

**Why adding ```POST``` method?:**

The ```methods``` argument added to the ```app.route``` decorator tells Flask to register the view function as a handler for ```GET``` and ```POST``` requests in the URL map. When ```methods``` is not given, the view function is registered to handle ```GET``` requests only.

Adding ```POST``` to the method list is necessary because form submissions are much more conveniently handled as ```POST``` requests. It is possible to submit a form as a ```GET``` request, but as ```GET``` requests have no body, the data is appended to the URL as a query string and becomes visible in the browser’s address bar. For this and several other reasons, form submissions are almost universally done as ```POST``` requests.

**```index()``` view function:**

The local ```name``` variable is used to hold the name received from the form when available; when the name is not known, the variable is initialized to ```None```. The view function creates an instance of the ```NameForm``` class shown previously to represent the form. **The ```validate_on_submit()``` method of the form returns ```True``` when the form was submitted and the data was accepted by all the field validators. In all other cases, ```validate_on_submit()``` returns ```False```.** The return value of this method effectively serves to determine whether the form needs to be rendered or processed. 

When a user navigates to the application for the first time, the server will receive a ```GET``` request with no form data, so ```validate_on_submit()``` will return False. The body of the if statement will be skipped and the request will be handled by rendering the template, which gets the ```form``` object and the ```name``` variable set to ```None``` as arguments. Users will now see the form displayed in the browser.

When the form is submitted by the user, the server receives a ```POST``` request with the data. The call to ```validate_on_submit()``` invokes the ```DataRequired()``` validator attached to the name field. If the name is not empty, then the validator accepts it and ```validate_on_submit()``` returns ```True```. **Now the name entered by the user is accessible as the ```data``` attribute of the field (_StringField_ object from NameForm subclass of FlaskForm class)**. Inside the body of the ```if``` statement, this name is assigned to the local ```name``` variable and the form field is cleared by setting that ```data``` attribute to an empty string, so that the field is blanked when the form is rendered to the page again. The ```render_template()``` call in the last line renders the template, but this time the name argument contains the name from the form, so the greeting will be personalized.


### Redirect and User Sessions

**IMPORTANT!**

**1st. Issue:**

The last version of _hello.py_ has a usability problem: if you enter your name and submit it, and then click the refresh button in your browser, you will likely get an obscure warning that asks for confirmation before submitting the form again. 

**This happens because browsers repeat the last request they sent when they are asked to refresh a page. When the last request sent is a ```POST``` request with form data, a refresh would cause a duplicate form submission, which in almost all cases is not the desired action.** For that reason, the browser asks for confirmation from the user. 

Many users do not understand this warning from the browser. Consequently, **it is considered good practice for web applications to never leave a ```POST``` request as the last request sent by the browser.**

**Solution:**

**This is achieved by responding to ```POST``` requests with a _redirect_ instead of a normal response.** A _redirect_ is a special type of response that contains a URL instead of a string with HTML code. **When the browser receives a redirect response, it issues a GET request for the redirect URL, and that is the page that it displays**. Now the last request is a ```GET```, so the refresh command works as expected. This trick is known as the ```Post/Redirect/Get``` pattern.

**2nd Issue:**

This approach brings a second problem. **When the application handles the ```POST``` request**, it has access to the name entered by the user in ```form.name.data```, but **as soon as that request ends the form data is lost**. **Because the ```POST``` request is handled with a redirect, the application needs to store the name so that the redirected request can have it and use it to build the actual response**.

Applications can “remember” things from one request to the next by storing them in the _user session_, a private storage that is available to each connected client. The _user session_ was introduced before as one of the variables associated with the request context. It’s called ```session``` and is accessed like a standard Python dictionary.

_Additional Note:_
>By default, user sessions are stored in client-side cookies.


```py
from flask import Flask, render_template, session, redirect, url_for

@app.route('/', methods=['GET', 'POST'])
def index():
    form = NameForm()
    if form.validate_on_submit():
        session['name'] = form.name.data
        return redirect(url_for('index'))
    return render_template('index.html', form=form, name=session.get('name'))
```

In the previous version of the application, a local ```name``` variable was used to store the name entered by the user in the form. That variable is now placed in the user session as ```session['name']``` so that it is remembered beyond the request.

_Additional Note:_
>```redirect()```, a Flask helper function that generates the HTTP redirect response. The ```redirect()``` function takes the URL to redirect to as an argument. The redirect URL used in this case is the root URL, so the response could have been written more concisely as ```redirect('/')``` but instead we use Flask’s URL generator function ```url_for()```. 
>The first and only required argument to ```url_for()``` is the _endpoint_ name, the internal name each route has. By default, the endpoint of a route is the name of the view function attached to it. In this example, the view function that handles the root URL is ```index()```, so the name given to ```url_for()``` is ```index```.

The last change is in the ```render_template()``` function, which now obtains the name argument directly from the session using ```session.get('name')```. As with regular dictionaries, using ```get()``` to request a dictionary key avoids an exception for keys that aren’t found. The ```get()``` method returns a default value of ```None``` for a missing key.

### Message Flashing

Sometimes it is useful to give the user a status update after a request is completed. This could be a confirmation message, a warning, or an error. Flask includes this functionality as a core feature. ```flash()``` function can be used for this purpose.

**Add this to _hello.py_**:

```py
@app.route('/', methods=['GET', 'POST'])
def index():
    form = NameForm()
    if form.validate_on_submit():
        old_name = session.get('name')
        if old_name is not None and old_name != form.name.data:
            flash('Looks like you have changed your name!')
        session['name'] = form.name.data
        return redirect(url_for('index'))
    return render_template('index.html', form = form, name = session.get('name'))
```

Explanation:

* Each time a name is submitted it is compared against the name stored in the user session, which will have been put there during a previous submission of the same form. 
* If the two names are different, the ```flash()``` function is invoked with a message to be displayed on the next response sent back to the client. 

Calling ```flash()``` is not enough to get messages displayed; **the templates used by the application need to render these messages**. The **best place to render** flashed messages **is the base template**, because that will enable these messages in all pages. **Flask makes a ```get_flashed_messages()``` function available to templates to retrieve the messages and render them.**


**Add this to _templates/base.html_:**

```html
{% block content %}
<div class="container">
    {% for message in get_flashed_messages() %}
    <div class="alert alert-warning">
        <button type="button" class="close" data-dismiss="alert">&times;</button>
        {{ message }}
    </div>
    {% endfor %}
    {% block page_content %}{% endblock %}
</div>
{% endblock %}
```

A loop is used because there could be multiple messages queued for display, one for each time ```flash()``` was called in the previous request cycle. Messages that are retrieved from ```get_flashed_messages()``` will not be returned the next time this function is called, so flashed messages appear only once and are then discarded.


# CHAPTER 5 - Databases


A _database_ stores application data in an organized way. The application then issues _queries_ to retrieve specific portions of the data. The most commonly used databases for web applications are those based on the **relational model**, also called **SQL** databases in reference to the ***Structured Query Language*** they use.

## SQL Databases - relational Model

Relational databases store data in **tables**. **A table has a fixed number of _columns_ and a variable number of _rows_**. 

* The **columns** define the data attributes of the entity represented by the table. For example, a customers table will have columns such as _name_, _address_, _phone_, and so on. 

* Each **row** in a table defines an actual data element that assigns values to some or all the columns.


### Primary Key & Foreign Key

#### Primary Key

Tables have a special column called the *primary key*, **which holds a unique identifier for each row stored in the table**.


#### Foreign Key

Tables can also have columns called *foreign keys*, **which reference the primary key of a row in the same or another table**.


**These links between rows are called relationships and are the foundation of the relational database model.**


**IMPORTANT!**

Relational databases store data efficiently and avoid duplication. Renaming a user role in this database is simple because role names exist in a single place. Immediately after a role name is changed in the ```roles``` table, all users that have a ```role_id``` that references the changed role will see the update.

On the other hand, having the data split into multiple tables can be a complication. Producing a listing of users with their roles presents a small problem, because users and user roles need to be read from two tables and joined before they can be presented together. Relational database engines provide the support to perform join operations between tables when necessary.


## NoSQL Databases

Databases that do not follow the relational are collectively referred to as **NoSQL** databases.

NoSQL databases uses _collections_ instead of tables and _documents_ instead of records. **NoSQL databases are designed in a way that makes joins difficult**, so most of them do not support this operation at all.

Listing the users with their roles requires the application itself to perform the join operation by reading the ```role_id``` field of each user and then searching the ```roles``` table for it.

**IMPORTANT!**

A more appropriate design for a NoSQL database consists on applying an operation called **denormalization**, which reduces the number of tables at the expense of data duplication.

* A database with this structure has the ```role``` name explicitly stored with each user. Renaming a role can then turn out to be an expensive operation that may require updating a large number of documents. 

* But it isn’t all bad news with NoSQL databases. Having the data duplicated allows for faster querying. Listing users and their roles is straightforward because no joins are needed.


## SQL or NoSQL?

SQL databases excel at storing structured data in an efficient and compact form. These databases go to great lengths to preserve consistency, based on the ACID paradigm (_Atomicity, Consistency, Isolation, and Durability_).

For small to medium-sized applications, both SQL and NoSQL databases are perfectly capable and have practically equivalent performance.

[Flask-SQLAlchemy intro course](https://courses.prettyprinted.com/courses/168305/lectures/2520266)

## Python Database Frameworks

Python has packages for most database engines. Flask puts no restrictions on what database packages can be used, so you can work with MySQL, Postgres, SQLite, Redis, MongoDB, CouchDB, or DynamoDB.

There are also a number of **database abstraction layer packages**, such as SQLAlchemy or MongoEngine, that **allow you to work at a higher level with regular Python objects instead of database entities such as tables, documents, or query languages**.

## Abstraction Layers Data Base Packages

Abstraction layers, also called _object-relational mappers (ORMs)_ or _object-document mappers (ODMs)_, provide transparent conversion of high-level object-oriented operations into low-level database instructions.

What makes sense is to choose a database abstraction layer that provides optional access to the underlying database in case specific operations need to be optimized by implementing them directly as native database instructions.

Some of these frameworks provide an abstraction layer for a single database engine, others abstract even higher and provide a choice of database engines—all accessible with the same object-oriented interface. **The best example of this is the SQLAlchemy ORM, which supports a list of relational database engines including the popular MySQL, Postgres, and SQLite.**

Based on these goals, the chosen database framework for the examples in this book will be Flask-SQLAlchemy, the Flask extension wrapper for SQLAlchemy.

## Database Management with Flask-SQLAlchemy

Flask-SQLAlchemy is a Flask extension that simplifies the use of SQLAlchemy inside Flask applications. **SQLAlchemy is a powerful relational database framework that supports several database backends. It offers a high-level ORM and low-level access to the database’s native SQL functionality.**

Install: 

```pip install flask-sqlalchemy```

In Flask-SQLAlchemy, a database is specified as a URL.


Database engine   |     URL

MySQL                   _mysql://username:password@hostname/database_
Postgres                _postgresql://username:password@hostname/database_
SQLite (Linux, macOS)   _sqlite:////absolute/path/to/database_
SQLite (Windows)        _sqlite:///c:/absolute/path/to/database_


In these URLs, _hostname_ refers to the server that hosts the database service, which could be _localhost_ or a remote server. Database servers can host several databases, so _database_ indicates the name of the database to use. For databases that need authentication, _username_ and _password_ are the database user credentials.

SQLite databases do not have a server, so _hostname_, _username_, and _password_ are omitted and _database_ is the filename on disk for the
database.

The URL of the application database must be configured as the key ```SQLALCHEMY_DATABASE_URI``` in the Flask configuration object. The Flask-SQLAlchemy documentation also suggests setting key ```SQLALCHEMY_TRACK_MODIFICATIONS``` to ```False``` to use less memory unless signals for object changes are needed.

_Initializing and configuring a simple SQLite database:_

```py
import os
from flask_sqlalchemy import SQLAlchemy
basedir = os.path.abspath(os.path.dirname(__file__))
app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] =\
    'sqlite:///' + os.path.join(basedir, 'data.sqlite')
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
db = SQLAlchemy(app)
```

The ```db``` object instantiated from the class SQLAlchemy represents the database and provides access to all the functionality of Flask-SQLAlchemy.


### Model Definition


**IMPORTANT!**

In the context of an ORM, **a model is typically a Python class with attributes that match the columns of a corresponding database table**.

**The database instance from Flask-SQLAlchemy (```db = SQLAlchemy(app)```) provides a base class for models as well as a set of helper classes and functions that are used to define their structure.**

**Creating Models (tables):**

```py
class Role(db.Model):
    __tablename__ = 'roles'
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(64), unique=True)
    
    def __repr__(self):
        return '<Role %r>' % self.name

class User(db.Model):
    __tablename__ = 'users'
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(64), unique=True, index=True)
    
    def __repr__(self):
        return '<User %r>' % self.username
```

1. The ```__tablename__``` class variable defines the name of the table in the database.

2. The remaining class variables are the attributes of the model, defined as instances of the ```db.Column``` class.

3. The first argument given to the ```db.Column``` constructor is the type of the database column and model attribute.


**Most common SQLAlchemy column types**

Type name              | Python type               | Description

```Integer```           ```int```                   Regular integer, typically 32 bits
```SmallInteger```      ```int```                   Short-range integer, typically 16 bits
```BigInteger```        ```int``` or ```long```     Unlimited precision integer
```Float```             ```float```                 Floating-point number
```Numeric```           ```decimal.Decimal```       Fixed-point number
```String```            ```str```                   Variable-length string
```Text```              ```str```                   Variable-length string, optimized for large or unbounded length
```Unicode```           ```unicode```               Variable-length Unicode string
```UnicodeText```       ```unicode```               Variable-length Unicode string, optimized for large or unbounded length
```Boolean```           ```bool```                  Boolean value
```Date```              ```datetime.date```         Date value
```Time```              ```datetime.time```         Time value
```DateTime```          ```datetime.datetime```     Date and time value
```Interval```          ```datetime.timedelta```    Time interval
```Enum```              ```str```                   List of string values
```PickleType```        Any Python object           Automatic Pickle serialization
```LargeBinary```       ```str```                   Binary blob


The remaining arguments to ```db.Column``` specify configuration options for each attribute.

Option name         | Description

```primary_key```   If set to True, the column is the table’s primary key.
```unique```        If set to True, do not allow duplicate values for this column.
```index```         If set to True, create an index for this column, so that queries are more efficient.
```nullable```      If set to True, allow empty values for this column. If set to False, the column will not allow null values.
```default```       Define a default value for the column.


_Additional Note:_
>Flask-SQLAlchemy requires all models to define a primary key column, which is commonly named ```id```.

Although it’s not strictly necessary, the two models include a ```__repr__()``` method to give them a readable string representation that can be used for debugging and testing purposes.

### Relationships

Relational databases establish connections between rows in different tables through the use of relationships.

The preceding code (class models) is a _one-to-many_ relationship from _roles_ to _users_, because one role can belong to many users, but each user can have only one role.

```py
class Role(db.Model):
# ...
users = db.relationship('User', backref='role')

class User(db.Model):
# ...
role_id = db.Column(db.Integer, db.ForeignKey('roles.id'))
```

**IMPORTANT!**

* A relationship connects two rows through the use of a foreign key. **The ```role_id``` column added to the ```User``` model is defined as a _foreign key_, and that establishes the relationship**. The ```'roles.id'``` argument to ```db.ForeignKey()``` **specifies that the column should be interpreted as having id values from rows in the roles table.**

_Additional Note:_
>A single sales transaction can only apply to one customer, but one customer can have many sales transactions over the course of time. This logic is what is defined by the one-to-many relationship

**IMPORTANT!**

* The ```users``` attribute added to the model ```Role``` represents the view of the relationship. **Given an instance of class ```Role```, the ```users``` attribute will return the _list of users associated with that role_**. The first argument to ```db.relationship()``` indicates what model is on the other side of the relationship. The model class can be provided as a string if the class is defined later in the module.

The ```backref``` argument to ```db.relationship()``` defines the reverse direction of the relationship, by adding a ```role``` attribute to the ```User``` model. This attribute can be used on any instance of ```User``` instead of the ```role_id``` foreign key to access the ```Role``` model as an object.

_Additional Note:_
>```backref```: When you define a relationship in the parent model, you add the "backref" keyword only if you want to access a parent element from a requested child element.

**Common SQLAlchemy relationship options**

Option name     |     Description

```backref```         Add a back reference in the other model in the relationship.
```primaryjoin```     Specify the join condition between the two models explicitly. This is necessary only for ambiguous relationships.

```lazy```            Specify how the related items are to be loaded. Possible values are _select_ (items are loaded on
                      demand the first time they are accessed), _immediate_ (items are loaded when the source object is
                      loaded), _joined_ (items are loaded immediately, but as a join), _subquery_ (items are loaded
                      immediately, but as a subquery), _noload_ (items are never loaded), and _dynamic_ (instead of loading
                      the items, the query that can load them is given).

```uselist```         If set to False, use a scalar instead of a list.
```order_by```        Specify the ordering used for the items in the relationship.
```secondary```       Specify the name of the association table to use in many-to-many relationships.
```secondaryjoin```   Specify the secondary join condition for many-to-many relationships when SQLAlchemy c


## Data Base Operations

### Set up
Before you use this command, make sure the ```FLASK_APP``` environment variable is set to _hello.py_.

### Creating the Tables
1. First thing to do is to instruct Flask-SQLAlchemy to create a database based on the model classes. The ```db.create_all()``` function locates all the subclasses of ```db.Model``` and creates corresponding tables in the database for them:

```shell
(venv) flask shell
>>> from hello import db
>>> db.create_all()
```

2. If you check the application directory, you will now see a new file there called ```data.sqlite```, the name that was given to the SQLite database in the configuration. The ```db.create_all()``` function will not re-create or update a database table if it already exists in the database. 

### Inserting Rows

1. The following example creates a few roles and users:

```shell
>>> from hello import Role, User
>>> admin_role = Role(name='Admin')
>>> mod_role = Role(name='Moderator')
>>> user_role = Role(name='User')
>>> user_john = User(username='john', role=admin_role)
>>> user_susan = User(username='susan', role=user_role)
>>> user_david = User(username='david', role=user_role)
```

The constructors for models accept initial values for the model attributes as keyword arguments. **Note that the ```role``` attribute can be used, even though it is not a real database column but a high-level representation of the one-to-many relationship**. 

The ```id``` attribute of these new objects is not set explicitly: the primary keys in many databases are managed by the database itself. The objects exist only on the Python side so far; they have not been written to the database yet. Because of that, their ```id``` values have not yet been assigned:

```shell
>>> print(admin_role.id)
None
>>> print(mod_role.id)
None
>>> print(user_role.id)
None
```

2. Changes to the database are managed through a database _session_, which Flask-SQLAlchemy provides as ```db.session```. To prepare objects to be written to the database, they must be added to the session:

```shell
>>> db.session.add(admin_role)
>>> db.session.add(mod_role)
>>> db.session.add(user_role)
>>> db.session.add(user_john)
>>> db.session.add(user_susan)
>>> db.session.add(user_david)
```

Or, more concisely:

```shell
>>> db.session.add_all([admin_role, mod_role, user_role, user_john, user_susan, user_david])
```

3. To write the objects to the database, the session needs to be _committed_ by calling its ```commit()``` method:

```shell
>>> db.session.commit()
```

4. Check the id attributes again after having the data committed to see that they are now set:

```shell
>>> print(admin_role.id)
1
>>> print(mod_role.id)
2
>>> print(user_role.id)
3
```

Database sessions are extremely useful in keeping the database consistent. **The commit operation writes all the objects that were added to the session atomically.** If an error occurs while the session is being written, the whole session is discarded. If you always commit related changes together in a session, you are guaranteed to avoid database inconsistencies due to partial updates.

_Additional Note:_
>If ```db.session.rollback()``` is called, any objects that were added to the database session are restored to the state they have in the database.

### Modifying rows

The ```add()``` method of the database session can also be used to update models.

```shell
>>> admin_role.name = 'Administrator'
>>> db.session.add(admin_role)
>>> db.session.commit()
```

### Deleting Rows

The database session also has a ```delete()``` method. The following example deletes the "Moderator" role from the database. Deletions, like insertions and updates, are executed only when the database session is committed.

```shell
>>> db.session.delete(mod_role)
>>> db.session.commit()
```

### Querying Rows

Flask-SQLAlchemy makes a ```query``` object available in each model class. The most basic query for a model is triggered with the ```all()``` method, which returns the entire contents of the corresponding table:

```shell
>>> Role.query.all()
[<Role 'Administrator'>, <Role 'User'>]
>>> User.query.all()
[<User 'john'>, <User 'susan'>, <User 'david'>]
```

**A query object can be configured to issue more specific database searches through the use of filters. The following example finds all the users that were assigned the "User" role:**

```shell
>>> User.query.filter_by(role=user_role).all()
[<User 'susan'>, <User 'david'>]
```

It is also possible to inspect the native SQL query that SQLAlchemy generates by converting the query object to a string:

```shell
>>> str(User.query.filter_by(role=user_role))
'SELECT users.id AS users_id, users.username AS users_username,
users.role_id AS users_role_id \nFROM users \nWHERE :param_1 = users.role_id'
```

If you exit the shell session, the objects created in the previous example will cease to exist as Python objects but will continue to exist as rows in their respective database tables. If you then start a brand-new shell session, you have to re-create the Python objects from their database rows. The following example issues a query that loads the user role with name "User":

```shell
>>> user_role = Role.query.filter_by(name='User').first()
```

____


[VIDEO TO UNDERSTUND LAST TOPIC](https://www.youtube.com/watch?v=juPQ04_twtA)

____ 


Note how in this case, the query was issued with the ```first()``` method instead of ```all()```. ```first()``` returns only the first result or ```None``` if there are no results, so it is a convenient method to use for queries that are known to return one result at the most. 

**Most common filters available to queries:**

Option       |      Description

```filter()```      Returns a new query that adds an additional filter to the original query
```filter_by()```   Returns a new query that adds an additional equality filter to the original query
```limit()```       Returns a new query that limits the number of results of the original query to the given number
```offset()```      Returns a new query that applies an offset into the list of results of the original query
```order_by()```    Returns a new query that sorts the results of the original query according to the given criteria
```group_by()```    Returns a new query that groups the results of the original query according to the given criteria

**Most common SQLAlchemy query executors**

Option      |        Description

```all()```             Returns all the results of a query as a list
```first()```           Returns the first result of a query, or None if there are no results
```first_or_404()```    Returns the first result of a query, or aborts the request and sends a 404 error as the response if there are no 
                        results
```get()```             Returns the row that matches the given primary key, or None if no matching row is found
```get_or_404()```      Returns the row that matches the given primary key or, if the key is not found, aborts the request and sends a 404 
                        error as the response
```count()```           Returns the result count of the query
```paginate()```        Returns a Pagination object that contains the specified range of results


**Relationships work similarly to queries. The following example queries the one-to-many relationship between roles and users from both ends:**

```shell
>>> users = user_role.users
>>> users
[<User 'susan'>, <User 'david'>]
>>> users[0].role
<Role 'User'>
```

The ```user_role.users``` query here has a small problem. The implicit query that runs when the ```user_role.users``` expression is issued internally calls ```all()``` to return the list of users. Because the query object is hidden, it is not possible to refine it with additional query filters. In this particular example, it may have been useful to request that the user list be returned in alphabetical order. In the example, the configuration of the relationship is modified with a ```lazy='dynamic'``` argument to request that the query is not automatically executed.

**Add to _hello.py_**:

```py
class Role(db.Model):
# ...
users = db.relationship('User', backref='role', lazy='dynamic')
# ...
```

With the relationship configured in this way, ```user_role.users``` returns a query that hasn’t executed yet, so filters can be added to it:

```shell
>>> user_role.users.order_by(User.username).all()
[<User 'david'>, <User 'susan'>]
>>> user_role.users.count()
2
```

### Database Use in View Functions

The database operations described in the previous sections can be used directly inside view functions.

**Add this to _hello.py_:**

```py
@app.route('/', methods=['GET', 'POST'])
def index():
    form = NameForm()
    if form.validate_on_submit():
        user = User.query.filter_by(username=form.name.data).first()
        if user is None:
            user = User(username=form.name.data)
            db.session.add(user)
            db.session.commit()
            session['known'] = False
        else:
            session['known'] = True
        session['name'] = form.name.data
        form.name.data = ''
        return redirect(url_for('index'))
    return render_template('index.html', form=form, name=session.get('name'), known=session.get('known', False))
```

In this modified version of the application, each time a name is submitted the application checks for it in the database using the ```filter_by()``` query filter. A ```known``` variable is written to the user session so that after the redirect the information can be sent to the template, where it is used to customize the greeting. Note that for the application to work, the database tables must be created in a Python shell as shown earlier. 

The new version of the associated template is shown in the following example. This template uses the ```known``` argument to add a second line to the greeting that is different for known and new users.

**Add this to _template/index.html_**


```html
{% extends "base.html" %}
{% import "bootstrap/wtf.html" as wtf %}
{% block title %}Flasky{% endblock %}
{% block page_content %}
<div class="page-header">
    <h1>Hello, {% if name %}{{ name }}{% else %}Stranger{% endif %}!</h1>
    {% if not known %}
    <p>Pleased to meet you!</p>
    {% else %}
    <p>Happy to see you again!</p>
    {% endif %}
</div>
{{ wtf.quick_form(form) }}
{% endblock %}
```

### Integration with Python Shell

**Having to import the database instance and the models each time a shell session is started is tedious** work. To avoid having to constantly repeat these steps, the **flask shell command can be configured to automatically import these objects**. To add objects to the import list, a **shell context processor must be created and registered with the ```app.shell_context_processor decorator```**.

**Add this to _hello.py_:**

```py
@app.shell_context_processor
def make_shell_context():
    return dict(db=db, User=User, Role=Role)
```

## Database Migrations with Flask-Migrate

Flask-SQLAlchemy creates database tables from models only when they do not exist already, so the only way to make it update tables is by destroying the old tables first—but of course, this causes all the data in the database to be lost.

**A better solution is to use a database migration framework.** A database migration framework keeps track of changes to a database schema, just like a source code version control tool (i.e.: GIT), allowing incremental changes to be applied.

Flask applications can use the Flask-Migrate extension, a lightweight Alembic wrapper that integrates it with the ```flask``` command.


### Creating a Migration Repository

```pip install flask-migrate```

**Add to _hello.py_:**

```py
from flask_migrate import Migrate
# ...
migrate = Migrate(app, db)
```

To expose the database migration commands, Flask-Migrate adds a ```flask db``` command with several subcommands. When you work on a new project, you can add support for database migrations with the ```init``` subcommand:

```shell
(venv) $ flask db init
Creating directory /home/flask/flasky/migrations...done
Creating directory /home/flask/flasky/migrations/versions...done
Generating /home/flask/flasky/migrations/alembic.ini...done
Generating /home/flask/flasky/migrations/env.py...done
Generating /home/flask/flasky/migrations/env.pyc...done
Generating /home/flask/flasky/migrations/README...done
Generating /home/flask/flasky/migrations/script.py.mako...done
Please edit configuration/connection/logging settings in
'/home/flask/flasky/migrations/alembic.ini' before proceeding.
```

**This command creates a migrations directory, where all the migration scripts will be stored**. The files in a database migration repository must always be added to version control along with the rest of the application.


### Creating a Migration Script

This script has two functions called ```upgrade()``` and ```downgrade()```:

1. The ```upgrade()``` function applies the database changes that are part of the migration

2. The ```downgrade()``` function removes them. 

This ability to add and remove changes means, Alembic can reconfigure a database to any point in the change history.

Alembic migrations can be created manually or automatically using the revision and migrate commands, respectively: 

1. **A manual migration** creates a migration skeleton script with empty ```upgrade()``` and ```downgrade()``` functions that need to be implemented by the developer using directives exposed by Alembic’s Operations object. 

2. **An automatic migration** generate the code for the ```upgrade()``` and ```downgrade()``` functions by looking for differences between the model definitions and the current state of the database. Automatic migrations are not always accurate and can miss some details that are ambiguous


To make changes to your database schema with Flask-Migrate, the following procedure needs to be followed:

1. Make the necessary changes to the model classes.

2. Create an automatic migration script with the ```flask db migrate``` command.

3. Review the generated script and adjust it so that it accurately represents the changes that were made to the models.

4. Add the migration script to source control.

5. Apply the migration to the database with the ```flask db upgrade``` command.

The ```flask db migrate``` subcommand creates an automatic migration script:

```shell
(venv) $ ```flask db migrate -m "initial migration"```
INFO [alembic.migration] Context impl SQLiteImpl.
INFO [alembic.migration] Will assume non-transactional DDL.
INFO [alembic.autogenerate] Detected added table 'roles'
INFO [alembic.autogenerate] Detected added table 'users'
INFO [alembic.autogenerate.compare] Detected added index
'ix_users_username' on '['username']'
Generating /home/flask/flasky/migrations/versions/1bc
594146bb5_initial_migration.py...done
```


### Upgrading the Database

Once a migration script has been reviewed and accepted, it can be applied to the database using the ```flask db upgrade``` command:

```shell
(venv) $ flask db upgrade
INFO [alembic.migration] Context impl SQLiteImpl.
INFO [alembic.migration] Will assume non-transactional DDL.
INFO [alembic.migration] Running upgrade None -> 1bc594146bb5, initial migration
```

For a first migration, this is effectively equivalent to calling ```db.create_all()```, but in successive migrations the ```flask db upgrade``` command applies updates to the tables without affecting their contents.


### Adding More Migrations

As you work on your own projects, you are going to make changes to your database models very often. When you manage the database through a migration framework, all changes must be defined in migration scripts, because anything that is not tracked in a migration will not be repeatable. The procedure to introduce a change in the database is similar to what was done to introduce the first migration:

1. Make the necessary changes in the database models.

2. Generate a migration with the ```flask db migrate``` command.

3. Review the generated migration script and correct it if it has any inaccuracies.

4. Apply the changes to the database with the ```flask db upgrade``` command.


**IMPORTANT!**

Each time the database models change repeat the ```migrate``` and ```upgrade``` commands.


# Email

## Email Support with Flask-Mail


[Flask-Mail Documentation](https://pythonhosted.org/Flask-Mail/)

Although the ```smtplib``` package from the Python standard library can be used to send email inside a Flask application, the Flask-Mail extension wraps ```smtplib``` and integrates it nicely with Flask.

```pip install flask-mail```

The extension connects to a _Simple Mail Transfer Protocol (SMTP)_ server and passes emails to it for delivery. If no configuration is given, Flask-Mail connects to localhost at port 25 and sends email without authentication. 

List of configuration keys that can be used to configure the SMTP server.


Key                   | Default         |  Description
```MAIL_SERVER```       ```localhost```    Hostname or IP address of the email server
```MAIL_PORT```         ```25```           Port of the email server
```MAIL_USE_TLS```      ```False```        Enable Transport Layer Security (TLS) security
```MAIL_USE_SSL```      ```False```        Enable Secure Sockets Layer (SSL) security
```MAIL_USERNAME```     ```None```         Mail account username
```MAIL_PASSWORD```     ```None```         Mail account password


During development it may be more convenient to connect to an external SMTP server. Example shows how to configure the application to send email through a Google Gmail account.

**Add to _hello.py_:**

```py
import os
# ...
app.config['MAIL_SERVER'] = 'smtp.googlemail.com'
app.config['MAIL_PORT'] = 587
app.config['MAIL_USE_TLS'] = True
app.config['MAIL_USERNAME'] = os.environ.get('MAIL_USERNAME')
app.config['MAIL_PASSWORD'] = os.environ.get('MAIL_PASSWORD')
```


_Additional Note:_
>For security reasons, Gmail accounts are configured to require external applications to use OAuth2 authentication to connect to the email server. Unfortunately, Python’s ```smtplib``` library does not support this method of authentication. To make your Gmail account accept standard SMTP authentication, go to your Google account settings page and select “Signing in to Google” from the left menu bar. On that page, locate the “Allow less secure apps” setting and make sure it is enabled. If enabling this setting on your personal Gmail account concerns you, create a secondary account only to test sending emails.

**Add to _hello.py_:**

```py
from flask_mail import Mail
mail = Mail(app)
```

_Additional Note:_
>Never write account credentials directly in your scripts, particularly if you plan to release your work as open source. To protect your account information, have your script import sensitive information from environment variables.


**Setting environmental variables in Windows Powershell:**

```shell
$env:MAIL_USERNAME:'mail user'
$env:MAIL_PASSWORD:'password'
```

## Sending Email from the Python Shell


To test the configuration, you can start a shell session and send a test email (replace ```you@example.com``` with your own email address):

```shell
(venv) $ flask shell
>>> from flask_mail import Message
>>> from hello import mail
>>> msg = Message('test email', sender='you@example.com', recipients=['you@example.com'])
>>> msg.body = 'This is the plain text body'
>>> msg.html = 'This is the <b>HTML</b> body'
>>> with app.app_context():
...     mail.send(msg)

```

Note that Flask-Mail’s ```send()``` function uses ```current_app```, so it needs to be executed with an activated application context.


## Integrating Emails with the Application

**Add to _hello.py_:**

```py
from flask_mail import Message

app.config['FLASKY_MAIL_SUBJECT_PREFIX'] = '[Flasky]'
app.config['FLASKY_MAIL_SENDER'] = 'Flasky Admin <flasky@example.com>'

def send_email(to, subject, template, **kwargs):
    msg = Message(app.config['FLASKY_MAIL_SUBJECT_PREFIX'] + subject, sender=app.config['FLASKY_MAIL_SENDER'], recipients=[to])
    msg.body = render_template(template + '.txt', **kwargs)
    msg.html = render_template(template + '.html', **kwargs)
    mail.send(msg)
```

The function relies on two application-specific configuration keys that define a prefix string for the subject and the address that will be used as the sender. The ```send_email()``` function takes the destination address, a subject line, a template for the email body, and a list of keyword arguments. 

The template name must be given without the extension, so that two versions of the template can be used for the plain text and HTML bodies. The keyword arguments passed by the caller are given to ```render_template()``` so that they can be used by the templates that generate the email body as template variables.

The ```index()``` view function can easily be expanded to send an email to the administrator whenever a new name is received with the form. 


**Add to _hello.py_:**

```py
app.config['FLASKY_ADMIN'] = os.environ.get('FLASKY_ADMIN')
# ...
@app.route('/', methods=['GET', 'POST'])
def index():
    form = NameForm()
    if form.validate_on_submit():
        user = User.query.filter_by(username=form.name.data).first()
        if user is None:
            user = User(username=form.name.data)
            db.session.add(user)
            session['known'] = False
            if app.config['FLASKY_ADMIN']:
                send_email(app.config['FLASKY_ADMIN'], 'New User', 'mail/new_user', user=user)
        else:
            session['known'] = True
        session['name'] = form.name.data
        form.name.data = ''
        return redirect(url_for('index'))
    return render_template('index.html', form=form, name=session.get('name'), known=session.get('known', False))
```

1. The recipient of the email is given in the ```FLASKY_ADMIN``` environment variable that’s loaded into a configuration variable of the same name during startup (```$env:FLASKY_ADMIN='Admin Mail'```). 

2. Two template files need to be created for the text and HTML versions of the email. These files are stored in a _mail_ subdirectory inside _templates_ to keep them separate from regular templates. The email templates expect the user to be given as a template argument, so the call to ```send_email()``` includes it as a keyword argument.


## Sending Asynchronous Email

If you sent a few test emails the ```mail.send()``` function blocks for a few seconds while the email is sent, making the browser look unresponsive during that time. To avoid unnecessary delays during request handling, the email send function can be moved to a background thread.

**Add to _hello.py_ asynchronous email support:**

```py
from threading import Thread

def send_async_email(app, msg):
    with app.app_context():
        mail.send(msg)

def send_email(to, subject, template, **kwargs):
    msg = Message(app.config['FLASKY_MAIL_SUBJECT_PREFIX'] + subject,
    sender=app.config['FLASKY_MAIL_SENDER'], recipients=[to])
    msg.body = render_template(template + '.txt', **kwargs)
    msg.html = render_template(template + '.html', **kwargs)
    thr = Thread(target=send_async_email, args=[app, msg])
    thr.start()
    return thr
```

This implementation highlights an interesting problem. Many Flask extensions operate under the assumption that there are active application and/or request contexts. As mentioned previously, Flask-Mail’s ```send()``` function uses ```current_app```, so it requires the application context to be active. But since contexts are associated with a thread, when the ```mail.send()``` function executes in a different thread it needs the application context to be created artificially using ```app.app_context()```. The app instance is passed to the thread as an argument so that a context can be created.

If you run the application now, you will notice that it is much more responsive, but keep in mind that for applications that send a large volume of email, having a job dedicated to sending email is more appropriate than starting a new thread for each email send operation. For example, the execution of the ```send_async_email()``` function can be sent to a Celery task queue.


# CHAPTER 7 - Large Application Structure

## Project Structure

Basic layout for a Flask application.

```
|-flasky
    |-app/
        |-templates/
        |-static/
        |-main/
            |-__init__.py
            |-errors.py
            |-forms.py
            |-views.py
        |-__init__.py
        |-email.py
        |-models.py
    |-migrations/
    |-tests/
        |-__init__.py
        |-test*.py
    |-venv/
    |-requirements.txt
    |-config.py
    |-flasky.py
```

This structure has four top-level folders:

* The Flask application lives inside a package generically named _app._

* The _migrations_ folder contains the database migration scripts, as before.

* Unit tests are written in a _tests_ package.

* The _venv_ folder contains the Python virtual environment, as before.

There are also a few new files:

* _requirements.txt_ lists the package dependencies so that it is easy to regenerate an identical virtual environment on a different computer.

* _config.py_ stores the configuration settings.

* _flasky.py_ defines the Flask application instance, and also includes a few tasks that help manage the application.

To help you fully understand this structure, the following sections describe the process to convert the _hello.py_ application to it.


## Configuration Options

Applications often need several configuration sets.

Instead of the simple ```app.config``` dictionary-like configuration used by _hello.py_, a hierarchy of configuration classes can be used. Example shows the _config.py_ file, with all the settings imported from _hello.py_.


**Create _config.py_:**


```py
import os

basedir = os.path.abspath(os.path.dirname(__file__))

class Config:
    SECRET_KEY = os.environ.get('SECRET_KEY') or 'hard to guess string'
    MAIL_SERVER = os.environ.get('MAIL_SERVER', 'smtp.googlemail.com')
    MAIL_PORT = int(os.environ.get('MAIL_PORT', '587'))
    MAIL_USE_TLS = os.environ.get('MAIL_USE_TLS', 'true').lower() in \
    ['true', 'on', '1']
    MAIL_USERNAME = os.environ.get('MAIL_USERNAME')
    MAIL_PASSWORD = os.environ.get('MAIL_PASSWORD')
    FLASKY_MAIL_SUBJECT_PREFIX = '[Flasky]'
    FLASKY_MAIL_SENDER = 'Flasky Admin <flasky@example.com>'
    FLASKY_ADMIN = os.environ.get('FLASKY_ADMIN')
    SQLALCHEMY_TRACK_MODIFICATIONS = False

    @staticmethod
    def init_app(app):
        pass

class DevelopmentConfig(Config):
    DEBUG = True
    SQLALCHEMY_DATABASE_URI = os.environ.get('DEV_DATABASE_URL') or \
        'sqlite:///' + os.path.join(basedir, 'data-dev.sqlite')

class TestingConfig(Config):
    TESTING = True
    SQLALCHEMY_DATABASE_URI = os.environ.get('TEST_DATABASE_URL') or \
        'sqlite://'

class ProductionConfig(Config):
    SQLALCHEMY_DATABASE_URI = os.environ.get('DATABASE_URL') or \
        'sqlite:///' + os.path.join(basedir, 'data.sqlite')

config = {
    'development': DevelopmentConfig,
    'testing': TestingConfig,
    'production': ProductionConfig,
    'default': DevelopmentConfig
}
```


The ```Config``` base class contains settings that are common to all configurations; the different subclasses define settings that are specific to a configuration. Additional configurations can be added as needed. To make configuration more flexible and safe, most settings can be optionally imported from environment variables. For example, the value of the ```SECRET_KEY```, due to its sensitive nature, can be set in the environment, but a default value is provided in case the environment does not define it. Typically, these settings can be used with their defaults during development but should each have an appropriate value set in the corresponding environment variable on the production server. The configuration options for the email server are all imported from environment variables as well, with defaults pointing to the Gmail server for convenience during development.

The ```SQLALCHEMY_DATABASE_URI``` variable is assigned different values under each of the three configurations. This enables the application to use a different database in each configuration.

This is very important, as you don’t want a run of the unit tests to change the database that you use for day-to-day development. Each configuration tries to import the database URL from an environment variable, and when that is not available it sets a default one based on SQLite.

For the testing configuration, the default is an in-memory database, since there is no need to store any data outside of the test run.


**IMPORTANT!**

The development and production configurations each have a set of mail server configuration options. **As an additional way to allow the application to customize its configuration, the ```Config``` class and its subclasses can define an ```init_app()``` class method that takes the application instance as an argument**. For now the base ```Config``` class implements an empty ```init_app()``` method.

At the bottom of the configuration script, the different configurations are registered in a ```config``` dictionary. One of the configurations (the one for development, in this case) is also registered as the default.

## Application Package

The application package is where all the application code, templates, and static files live. It is called simply _app_ here, though it can be given an application-specific name if desired. The _templates_ and _static_ directories are now part of the application package, so they are moved inside _app_. The database models and the email support functions are also moved inside this package, each in its own module, as _app/models.py_ and _app/email.py_


_Additional Note:_
> ```from_object``` updates the values from the given object. Just the uppercase variables in that object are stored in the config. Example usage:

```py
app.config.from_object('yourapplication.default_config')
from yourapplication import default_config
app.config.from_object(default_config)
```

>You should not use this function to load the actual configuration but rather configuration defaults. The actual config should be loaded with ```from_pyfile()``` and ideally from a location not within the package because the package might be installed system wide.


For clearer information, checkout this documentation:

[Official Flask Configuration Documentation](https://flask.palletsprojects.com/en/1.1.x/config/)

[ExploreFlask Configuration Documentation](https://exploreflask.com/en/latest/configuration.html)


### Using Application Factory

The single-file version of the application has one big drawback: 

_Because the application is created in the global scope, there is no way to apply configuration changes dynamically: by the time the script is running, the application instance has already been created, so it is already too late to make configuration changes. This is particularly important for unit tests._

The solution to this problem is to delay the creation of the application by moving it into a factory function that can be explicitly invoked from the script. This not only gives the script time to set the configuration, but also the ability to create multiple application instances.


**Application Factory ```__init__.py```**:

```py
from flask import Flask
from flask_bootstrap import Bootstrap
from flask_mail import Mail
from flask_moment import Moment
from flask_sqlalchemy import SQLAlchemy
from config import config

bootstrap = Bootstrap()
mail = Mail()
moment = Moment()
db = SQLAlchemy()


def create_app(config_name):
    app = Flask(__name__)
    app.config.from_object(config[config_name])
    config[config_name].init_app(app)

    bootstrap.init_app(app)
    mail.init_app(app)
    moment.init_app(app)
    db.init_app(app)

    from .main import main as main_blueprint
    app.register_blueprint(main_blueprint)

    return app
```

1. This constructor imports most of the Flask extensions currently in use, but because there is no application instance to initialize them with, it creates them uninitialized by passing no arguments into their constructors. 

2. The ```create_app()``` function is the _application factory_, which takes as an argument the name of a configuration to use for the application. 

3. The configuration settings stored in one of the classes defined in _config.py_ can be imported directly into the application using the ```from_object()``` method available in Flask’s ```app.config``` configuration object.

4. The configuration object is selected by name from the ```config``` dictionary. 

5. Once an application is created and configured, the extensions can be initialized. Calling ```init_app()``` on the extensions that were created earlier completes their initialization. 

* The application initialization is now done in this factory function, using the ```from_object()``` method from the Flask configuration object, which takes as an argument one of the configuration classes defined in _config.py_. 

* The ```init_app()``` method of the selected configuration is also invoked, to allow more complex initialization procedures to take place. 

The factory function returns the created application instance, but note that applications created with the factory function in its current state are incomplete, as they are missing routes and custom error page handlers. This is the topic of the next section.


### Implementing Application Functionality in a Blueprint

In single-script applications, the application instance exists in the global scope, so routes can be easily defined using the ```app.route``` decorator. But now that the application is created at runtime, the ```app.route``` decorator begins to exist only after ```create_app()``` is invoked, which is too late.

**IMPORTANT!**

**Flask offers a better solution using _blueprints_.** 
>A blueprint is similar to an application in that it can also define routes and error handlers. The difference is that when these are defined in a blueprint they are in a dormant state until the blueprint is registered with an application, at which point they become part of it. 

Using a blueprint defined in the global scope, the routes and error handlers of the application can be defined in almost the same way as in the single-script application. 

Like applications, blueprints can be defined all in a single file or can be created in a more structured way with multiple modules inside a package. To allow for the greatest flexibility, **a subpackage inside the application package will be created to host the first blueprint of the application.**

**Create directory and file _app/main/__init__.py_:**

```py
from flask import Blueprint

main = Blueprint('main', __name__)
from . import views, errors
```

Blueprints are created by instantiating an object of class ```Blueprint```. The constructor for this class takes two required arguments: the blueprint name and the module or package where the blueprint is located. As with applications, Python’s ```__name__``` variable is in most cases the correct value for the second argument.


* The routes of the application are stored in an _app/main/views.py_ module inside the package, and the error handlers are in _app/main/errors.py_. 

**IMPORTANT!**

Importing these modules causes the routes and error handlers to be associated with the blueprint. **It is important to note that the modules are imported at the bottom of the _app/main/__init__.py_ script to avoid errors due to circular dependencies.** In this particular example the problem is that _app/main/views.py_ and _app/main/errors.py_ in turn are going to import the ```main``` blueprint object, so the imports are going to fail unless the circular reference occurs after ```main``` is defined.


_Additional Note:_
>The ```from . import <some-module>``` syntax is used in Python to represent relative imports. The ```.``` in this statement represents the current package. You are going to see another very useful relative import soon that uses the form ```from .. import <some-module>```, where ```..``` represents the parent of the current package.


The blueprint is registered with the application inside the ```create_app()``` factory function as seen:

**Add to _app/__init__.py_:**

```py
def create_app(config_name):
# ...
from .main import main as main_blueprint
app.register_blueprint(main_blueprint)

return app
```

If the ```errorhandler``` decorator is used, the handler will be invoked only for errors that originate in the routes defined by the blueprint. To install application-wide error handlers, the ```app_errorhandler``` decorator must be used instead.

**Add to _app/main/errors.py_:**

```py
from flask import render_template
from . import main

@main.app_errorhandler(404)
def page_not_found(e):
    return render_template('404.html'), 404

@main.app_errorhandler(500)
def internal_server_error(e):
    return render_template('500.html'), 500
```


**Add to _app/main/views.py_:**

```py
from flask import render_template, session, redirect, url_for, current_app
from .. import db
from ..models import User
from ..email import send_email
from . import main
from .forms import NameForm


@main.route('/', methods=['GET', 'POST'])
def index():
    form = NameForm()
    if form.validate_on_submit():
        user = User.query.filter_by(username=form.name.data).first()
        if user is None:
            user = User(username=form.name.data)
            db.session.add(user)
            db.session.commit()
            session['known'] = False
            if current_app.config['FLASKY_ADMIN']:
                send_email(current_app.config['FLASKY_ADMIN'], 'New User',
                           'mail/new_user', user=user)
        else:
            session['known'] = True
        session['name'] = form.name.data
        return redirect(url_for('.index'))
    return render_template('index.html',
                           form=form, name=session.get('name'),
                           known=session.get('known', False))
```


There are two main differences when writing a view function inside a blueprint. 

1. First, as was done for error handlers earlier, the route decorator comes from the blueprint, so ```main.route``` is used instead of ```app.route```. 

2. The second difference is in the usage of the ```url_for()``` function. As you may recall, the first argument to this function is the endpoint name of the route, which for application-based routes defaults to the name of the view function. For example, in a single-script application the URL for an ```index()``` view function can be obtained with ```url_for('index')```.

**The difference with blueprints is that Flask applies a namespace to all the endpoints defined in a blueprint, so that multiple blueprints can define view functions with the same endpoint names without collisions.** 

_Additional Note:_
>**Namespace**: Modules can have various functions and classes. A local namespace is created when a function is called, which has all the names defined in it. Similar, is the case with class.


The namespace is the name of the blueprint (the first argument to the ```Blueprint``` constructor) and is separated from the endpoint name with a dot. The ```index()``` view function is then registered with endpoint name ```main.index``` and its URL can be obtained with ```url_for('main.index')```. 

The ```url_for()``` function also supports a shorter format for endpoints in blueprints in which the blueprint name is omitted, such as ```url_for('.index')```. With this notation, the blueprint name for the current request is used to complete the endpoint name. This effectively means that redirects within the same blueprint can use the shorter form, while redirects across blueprints must use the fully qualified endpoint name that includes the blueprint name.


## Application Script

The _flasky.py_ module in the top-level directory is where the application instance is defined.


**Add to _flasky.py_:**
```py
import os
import click
from flask_migrate import Migrate
from app import create_app, db
from app.models import User, Role

app = create_app(os.getenv('FLASK_CONFIG') or 'default')
migrate = Migrate(app, db)


@app.shell_context_processor
def make_shell_context():
    return dict(db=db, User=User, Role=Role)
```


The script begins by creating an application. The configuration is taken from the environment variable ```FLASK_CONFIG``` if it’s defined, or else the default configuration is used. Flask-Migrate and the custom context for the Python shell are then initialized. Because the main script of the application changed from _hello.py_ to _flasky.py_, the ```FLASK_APP``` environment variable needs to be updated accordingly so that the flask command can locate the application instance. It is also useful to enable Flask’s debug mode by setting FLASK_DEBUG=1. 

```shell
(venv) $env:FLASK_APP="flasky.py"
(venv) $env:FLASK_DEBUG=1
```

## Requirements File

It is a good practice for applications to include a _requirements.txt_ file that records all the package dependencies, with the exact version numbers. This is important in case the virtual environment needs to be regenerated on a different machine, such as the machine on which the application will be deployed for production use. This file can be generated automatically by _pip_ with the following command:

```shell
(venv) $ pip freeze >requirements.txt
```

When you need to build a perfect replica of the virtual environment, you can create a new virtual environment and run the following command on it:

```shell
(venv) $ pip install -r requirements.txt
```

## Unit Tests

**Add to _tests/test_basics.py_:**

```py
import unittest
from flask import current_app
from app import create_app, db


class BasicsTestCase(unittest.TestCase):
    def setUp(self):
        self.app = create_app('testing')
        self.app_context = self.app.app_context()
        self.app_context.push()
        db.create_all()

    def tearDown(self):
        db.session.remove()
        db.drop_all()
        self.app_context.pop()

    def test_app_exists(self):
        self.assertFalse(current_app is None)

    def test_app_is_testing(self):
        self.assertTrue(current_app.config['TESTING'])
```

The ```setUp()``` and ```tearDown()``` methods of the test case class run before and after each test, and any methods that have a name that begins with ```test_``` are executed as tests.

1. The ```setUp()``` method tries to create an environment for the test that is close to that of a running application. 

* It first creates an application configured for testing and activates its context. This step ensures that tests have access to ```current_app```, like regular requests do. 

* Then it creates a brand-new database for the tests using Flask- SQLAlchemy’s ```create_all()``` method. 

2. The database and the application context are removed in the ```tearDown()``` method. 

* The first test ensures that the application instance exists. 

* The second test ensures that the application is running under the testing configuration. To make the tests directory a proper package, a _tests/init.py_ module needs to be added, but this can be an empty file, as the unittest package scans all the modules to discover the tests.


To run the unit tests, a custom command can be added to the _flasky.py_ script.

**Add to _flasky.py_:**

```py
@app.cli.command()
@click.argument('test_names', nargs=-1)
def test(test_names):
    """Run the unit tests."""
    import unittest
    if test_names:
        tests = unittest.TestLoader().loadTestsFromNames(test_names)
    else:
        tests = unittest.TestLoader().discover('tests')
    unittest.TextTestRunner(verbosity=2).run(tests)
```

The ```app.cli.command``` decorator makes it simple to implement custom commands. The name of the decorated function is used as the command name, and the function’s docstring is displayed in the help messages. The implementation of the ```test()``` function invokes the test runner from the ```unittest``` package.

```shell
(venv) $ flask test
```


## Database Setup

The database URL is taken from an environment variable as a first choice, with a default SQLite database as an alternative. The environment variables and SQLite database filenames are different for each of the three configurations. 

For example, in the development configuration the URL is obtained from the environment variable ```DEV_DATABASE_URL```, and if that is not defined then an SQLite database with the name ```data-dev.sqlite``` is used. Regardless of the source of the database URL, the database tables must be created for the new database. When working with Flask-Migrate to keep track of migrations, database tables can be created or upgraded to the latest revision with a single command:

```shell
(venv) $ flask db upgrade
```

## Running the Application

The refactoring is now complete, and the application can be started. 

Make sure you have updated the ```FLASK_APP``` environment variable as indicated in “Application Script” on page 93, and then run the application as usual: 

```shell
(venv) $ flask run
```

Having to set the ```FLASK_APP``` and ```FLASK_DEBUG``` environment variables every time a new command-prompt session is started can get tedious, so you should configure your system so that these variables are set by default. 

If you are using bash, you can add them to your ~/.bashrc file. Believe it or not, you have reached the end of Part I.

# PART II

# CHAPTER 8 - User Authentication

The most commonly used method of authentication requires users to provide a piece of identification, which is either their email address or username, and a secret only known to them, which is called the password.

## Authentication Extensions for Flask

This is the list of packages that will be used, and what they’re used for:

* ```Flask-Login```: Management of user sessions for logged-in users

* ```Werkzeug```: Password hashing and verification

* ```itsdangerous```: Cryptographically secure token generation and verification

In addition to authentication-specific packages, the following general-purpose extensions will be used:

* ```Flask-Mail```: Sending of authentication-related emails
* ```Flask-Bootstrap```: HTML templates
* ```Flask-WTF```: Web forms

### Password Security

The safety of user information stored in databases is often overlooked during the design of web applications. It is a known fact that most users use the same password on multiple sites, so even if you don’t store any sensitive information, access to the passwords stored in your database can give the attacker access to accounts your users have on other sites.

**The key to storing user passwords securely in a database relies on not storing the password itself but a _hash_ of it**: 

>**Password _Hashing_:** <br><br>
>**A password hashing function takes a password as input, adds a random component to it (the **salt**), and then applies several one-way cryptographic transformations to it**. <br>The result is a new sequence of characters that has no resemblance to the original password, and has no known way to be transformed back into the original password. Password hashes can be verified in place of the real passwords because hashing functions are repeatable: given the same inputs (the password and the salt), the result is always the same.

### Hashing Passwords with Werkzeug

Werkzeug’s security module conveniently implements secure password hashing. This functionality is exposed with just two functions, used in the registration and verification phases, respectively:

**Registration:** 

```py
generate_password_hash(password, method='pbkdf2:sha256', salt_length=8)
``` 

This function takes a plain-text password and returns the password hash as a string that can be stored in the user database. The default values for ```method``` and ```salt_length``` are sufficient for most use cases.

**Validation:**

```py
check_password_hash(hash, password)
```

This function takes a password hash previously stored in the database and the password entered by the user. A return value of ```True``` indicates that the user password is correct.

Make the following changes to the ```User``` model to accommodate password hashing.

**Add to _app/models.py_:** 

```py
from werkzeug.security import generate_password_hash, check_password_hash

class User(db.Model):
# ...
password_hash = db.Column(db.String(128))

@property
def password(self):
    raise AttributeError('password is not a readable attribute')

@password.setter
def password(self, password):
    self.password_hash = generate_password_hash(password)

def verify_password(self, password):
    return check_password_hash(self.password_hash, password)
```

The password hashing function is implemented through a write-only property called ```password```. When this property is set, the setter method will call Werkzeug’s ```generate_password_hash()``` function and write the result to the ```password_hash``` field. Attempting to read the ```password``` property will return an error, as clearly the original password cannot be recovered once hashed.

The ```verify_password()``` method takes a password and passes it to Werkzeug’s ```check_password_hash()``` function for verification against the hashed version stored in the User model. If this method returns True, then the password is correct.

_____


[```@property``` in Python - GeekForGeeks](https://www.geeksforgeeks.org/getter-and-setter-in-python/)


[@property, @classmethod, @staticmethod - VIDEO](https://www.youtube.com/watch?v=upmOAPk2cK8)
_____

The password hashing functionality is now complete and can be tested in the shell:

```shell
(venv) $ flask shell
>>> u = User()
>>> u.password = 'cat'
>>> u.password
Traceback (most recent call last):
File "<console>", line 1, in <module>
File "/home/flask/flasky/app/models.py", line 24, in password
raise AttributeError('password is not a readable attribute')
AttributeError: password is not a readable attribute
>>> u.password_hash
'pbkdf2:sha256:50000$moHwFH1B$ef1574909f9c549285e8547cad181c5e0213cfa44a4aba4349
fa830aa1fd227f'
>>> u.verify_password('cat')
True
>>> u.verify_password('dog')
False
>>> u2 = User()
>>> u2.password = 'cat'
>>> u2.password_hash
'pbkdf2:sha256:50000$Pfz0m0KU$27be930b7f0e0119d38e8d8a62f7f5e75c0a7db61ae16709bc
aa6cfd60c44b74'
```


Note how trying to access the ```password``` property of a user returns an ```AttributeError```. Also, users ```u``` and ```u2``` have completely different password hashes, even though they both use the same password. To ensure that this functionality continues to work in the future, the preceding tests done manually can be written as unit tests that can be repeated easily. Create new module inside the _tests_ package.

**Create file at *tests/test_user_model.py***:

```py

import unittest
from app.models import User

class UserModelTestCase(unittest.TestCase):
    def test_password_setter(self):
        u = User(password = 'cat')
        self.assertTrue(u.password_hash is not None)
    
    def test_no_password_getter(self):
        u = User(password = 'cat')
        with self.assertRaises(AttributeError):
            u.password
    
    def test_password_verification(self):
        u = User(password = 'cat')
        self.assertTrue(u.verify_password('cat'))
        self.assertFalse(u.verify_password('dog'))

    def test_password_salts_are_random(self):
        u = User(password='cat')
        u2 = User(password='cat')
        self.assertTrue(u.password_hash != u2.password_hash)
```

### Creating an Authentication Blueprint

Using different blueprints for different subsystems of the application is a great way to keep the code neatly organized. In this section, the routes related to the user authentication subsystem will be added to a second blueprint, called ```auth```.

The ```auth``` blueprint will be hosted in a Python package with the same name. The blueprint’s package constructor creates the blueprint object and imports routes from a _views.py_ module.

_Authentication blueprint creation_:

**Create  _app/auth/__init__.py_:** 

```py
from flask import Blueprint

auth = Blueprint('auth', __name__)

from . import views
```

The _app/auth/views.py_ module, imports the blueprint and defines the routes associated with authentication using its ```route``` decorator. For now, a ```/login``` route is added, which renders a placeholder template of the same name.

**Create _app/auth/views.py_:**

```py
from flask import render_template
from . import auth

@auth.route('/login')
def login():
    return render_template('auth/login.html')
```

Note that the template file given to ```render_template()``` is stored inside the _auth_ directory. **This directory must be created inside _app/templates_, as Flask expects the templates’ paths to be relative to the application’s templates directory**. By storing the blueprint templates in their own subdirectory, there is no risk of naming collisions with the main blueprint or any other blueprints that will be added in the future.

>Blueprints can also be configured to have their own independent directories for templates. When multiple template directories have been configured, the ```render_template()``` function searches the templates directory configured for the application first, and then searches the template directories defined by blueprints.


The ```auth``` blueprint needs to be attached to the application in the create_app() factory function, as shown in Example 8-5.

Authentication blueprint registration

**Add to *app/__init__.py*:**

```py
def create_app(config_name):
# ...
from .auth import auth as auth_blueprint
app.register_blueprint(auth_blueprint, url_prefix='/auth')
return app
```

**IMPORTANT!**

The ```url_prefix``` argument in the blueprint registration is optional. When used, all the routes defined in the blueprint will be registered with the given prefix, in this case _/auth_. For example, the _/login_ route will be registered as _/auth/login_, and the fully qualified URL under the development web server then becomes _http://localhost:5000/auth/login_.


## User Authentication with Flask-Login

When users log in to the application, their authenticated state has to be recorded in the user session, so that it is remembered as they navigate through different pages. Flask-Login is a small but extremely useful extension that specializes in managing this particular aspect of a user authentication system

The extension needs to be installed in the virtual environment:

```(venv) $ pip install flask-login```

### Preparing the User Model for Logins

Flask-Login works closely with the application’s own ```User``` objects. To be able to work with the application’s ```User``` model, the Flask-Login extension requires it to implement a few common properties and methods as shown in the following table.

_Flask-Login required items_

Property/method     |       Description
```is_authenticated```      Must be ```True``` if the user has valid login credentials or False otherwise.
```is_active```             Must be ```True``` if the user is allowed to log in or ```False``` otherwise. A ```False``` value can be used for disabled accounts.
```is_anonymous```          Must always be ```False``` for regular users and True for a special user object that represents anonymous users.
```get_id()```              Must return a unique identifier for the user, encoded as a Unicode string.

**IMPORTANT!**

These properties and methods can be implemented directly in the model class, but as an easier alternative Flask-Login provides a ```UserMixin``` class that has default implementations that are appropriate for most cases. The updated ```User``` model is shown in the following example.

Updates to the `` `` model to support user logins

**Add to _app/models.py_:** 

```py
from flask_login import UserMixin

class User(UserMixin, db.Model):
    __tablename__ = 'users'
    id = db.Column(db.Integer, primary_key = True)
    email = db.Column(db.String(64), unique=True, index=True)
    username = db.Column(db.String(64), unique=True, index=True)
    password_hash = db.Column(db.String(128))
    role_id = db.Column(db.Integer, db.ForeignKey('roles.id'))
```

Note that an ```email``` field was also added. In this application, users will log in with their email addresses, as they are less likely to forget those than their usernames. Flask-Login is initialized in the application factory function, as shown in the example.

Flask-Login initialization

**Add to *app/__init__.py*:**

```py
from flask_login import LoginManager

login_manager = LoginManager()
login_manager.login_view = 'auth.login'

def create_app(config_name):
# ...
login_manager.init_app(app)
# ...
```

The ```login_view``` attribute of the ```LoginManager``` object sets the endpoint for the login page. Flask-Login will redirect to the login page when an anonymous user tries to access a protected page. Because the login route is inside a blueprint, it needs to be prefixed with the blueprint name.

Finally, Flask-Login requires the application to designate a function to be invoked when the extension needs to load a user from the database given its identifier. This function is shown in below.

_User loader function_

**Add to *app/models.py*:** 

```py
from . import login_manager

@login_manager.user_loader
def load_user(user_id):
    return User.query.get(int(user_id))
```

**IMPORTANT!**

The ```login_manager.user_loader``` decorator is used to register the function with Flask-Login, which will call it when it needs to retrieve information about the loggedin user. The user identifier will be passed as a string, so the function converts it to an integer before it passes it to the Flask-SQLAlchemy query that loads the user. The return value of the function must be the user object, or None if the user identifier is invalid or any other error occurred.

### Protecting Routes

To protect a route so that it can only be accessed by authenticated users, Flask-Login provides a ```login_required``` decorator. An example of its usage follows:

```py
from flask_login import login_required

@app.route('/secret')
@login_required
def secret():
    return 'Only authenticated users are allowed!'
```

You can see from this example that it is possible to “chain” multiple function decorators. When two or more decorators are added to a function, each decorator only affects those that are below it, in addition to the target function. In this example, the ```secret()``` function will be protected against unauthorized users with ```login_required```, and then the resulting function will be registered with Flask as a route. Reversing the order will produce the wrong result, as the original function will be registered as a route before it receives the additional properties from the ```login_required``` decorator.

Thanks to the ```login_required``` decorator, if this route is accessed by a user who is not authenticated, Flask-Login will intercept the request and send the user to the login page instead.

### Adding a Login Form

The login form that will be presented to users has a text field for the email address, a password field, a “remember me” checkbox, and a submit button. The Flask-WTF form class that defines this form is shown below.

_Login form_

**Creat this at *app/auth/forms.py*:** 

```py
from flask_wtf import FlaskForm
from wtforms import StringField, PasswordField, BooleanField, SubmitField
from wtforms.validators import DataRequired, Length, Email

class LoginForm(FlaskForm):
    email = StringField('Email', validators=[DataRequired(), Length(1, 64), Email()])
    password = PasswordField('Password', validators=[DataRequired()])
    remember_me = BooleanField('Keep me logged in')
    submit = SubmitField('Log In')
```

* The ```PasswordField``` class represents an ```<input>``` element with ```type="password"```. 

* The ```BooleanField``` class represents a checkbox. 

* The email field uses the ```Length()``` and ```Email()``` validators from WTForms in addition to ```DataRequired()```, to ensure that the user not only provides a value for this field, but that it is valid. When providing a list of validators, WTForms will evaluate them in the order provided, and in case of a validation failure the error message shown will be the one of the first validator that failed. 

The template associated with the login page is stored in _auth/login.html_. This template just needs to render the form using Flask-Bootstrap’s ```wtf.quick_form()``` macro.

The navigation bar in the base.html template uses a Jinja2 conditional to display “Log In” or “Log Out” links depending on the logged-in state of the current user. The conditional is shown below.

_Log In and Log Out navigation bar links_

**Add this to _app/templates/base.html_:**

```html
<ul class="nav navbar-nav navbar-right">
    {% if current_user.is_authenticated %}
    <li><a href="{{ url_for('auth.logout') }}">Log Out</a></li>
    {% else %}
    <li><a href="{{ url_for('auth.login') }}">Log In</a></li>
    {% endif %}
</ul>
```

The ```current_user``` variable used in the conditional is defined by Flask-Login and is automatically available to view functions and templates. This variable contains the currently logged-in user, or a proxy anonymous user object if the user is not logged in. Anonymous user objects have the ```is_authenticated``` property set to ```False```, so the expression ```current_user.is_authenticated``` is a convenient way to know whether the current user is logged in.

### Sing users in

The implementation of the ```login()``` view function:

**Add this to *auth/views.py*:**

```py
from flask import render_template, redirect, request, url_for, flash
from flask_login import login_user, logout_user, login_required
from . import auth
from ..models import User
from .forms import LoginForm


@auth.route('/login', methods=['GET', 'POST'])
def login():
    form = LoginForm()
    if form.validate_on_submit():
        user = User.query.filter_by(email=form.email.data.lower()).first()
        if user is not None and user.verify_password(form.password.data):
            login_user(user, form.remember_me.data)
            next = request.args.get('next')
            if next is None or not next.startswith('/'):
                next = url_for('main.index')
            return redirect(next)
        flash('Invalid email or password.')
    return render_template('auth/login.html', form=form)
```

The view function creates a ```LoginForm``` object and uses it like the simple form in Chapter 4. When the request is of type `` ``, the view function just renders the template, which in turn displays the form. When the form is submitted in a ```POST``` request, Flask-WTF’s ```validate_on_submit()``` function validates the form variables, and then attempts to log the user in.

To log a user in, the function begins by loading the user from the database using the ```email``` provided with the form. If a user with the given email address exists, then its ```verify_password()``` method is called with the password that also came with the form.If the password is valid, Flask-Login’s ```login_user()``` function is invoked to record the user as logged in for the user session. The ```login_user()``` function takes the user to log in and an optional “remember me” Boolean, which was also submitted with the form. A value of ```False``` for this argument causes the user session to expire when the browser window is closed, so the user will have to log in again next time. A value of ```True``` causes a long-term cookie to be set in the user’s browser, which Flask-Login uses to restore the user session. The optional ```REMEMBER_COOKIE_DURATION``` configuration option can be used to change the default one-year duration for the remember cookie.

**IMPORTANT!**

**In accordance with the Post/Redirect/Get pattern discussed in Chapter 4, the ```POST``` request that submitted the login credentials ends with a redirect, but there are two possible URL destinations:**

1. If the login form was presented to the user to prevent unauthorized access to a protected URL the user wanted to visit, then Flask-Login (through the ```@login_required``` decorator function) will have saved that original URL in the ```next``` query string argument, which can be accessed from the ```request.args``` dictionary. 

2. If the ```next``` query string argument is not available, a redirect to the home page is issued instead. The URL in ```next``` is validated to make sure it is a relative URL (
    ```py
    if next is None or not next.startswith('/'):
    ```
    ), to prevent a malicious user from using this argument to redirect unsuspecting users to another site. 

For the case where the email address or password provided by the user is invalid, a flash message is set and the form is rendered again for the user to retry.


### About ```next``` query string parameter


____


[Understanding ```next``` query string parameter](https://flask.palletsprojects.com/en/1.1.x/patterns/viewdecorators/)

____

#### From flask_login python package

*C:\Users\Marcos\flasky\venv\Lib\site-packages\flask_login\utils.py*

```py
def login_url(login_view, next_url=None, next_field='next'):
    '''
    Creates a URL for redirecting to a login page. If only `login_view` is
    provided, this will just return the URL for it. If `next_url` is provided,
    however, this will append a ``next=URL`` parameter to the query string
    so that the login view can redirect back to that URL. Flask-Login's default
    unauthorized handler uses this function when redirecting to your login url.
    To force the host name used, set `FORCE_HOST_FOR_REDIRECTS` to a host. This
    prevents from redirecting to external sites if request headers Host or
    X-Forwarded-For are present.

    :param login_view: The name of the login view. (Alternately, the actual
                       URL to the login view.)
    :type login_view: str
    :param next_url: The URL to give the login view for redirection.
    :type next_url: str
    :param next_field: What field to store the next URL in. (It defaults to
                       ``next``.)
    :type next_field: str
    '''
```

____

#### From MDN documentation

The ```url``` read-only property of the Request interface contains the URL of the request.

Example:

```
var myRequest = new Request('flowers.jpg');
var myURL = myRequest.url; // "http://mdn.github.io/fetch-examples/fetch-request/flowers.jpg"
```
____

#### From Flask documentation


>@login_required decorator - ```next``` parameter:
```py
from functools import wraps
from flask import g, request, redirect, url_for

def login_required(f):
    @wraps(f)
    def decorated_function(*args, **kwargs):
        if g.user is None:
            return redirect(url_for('login', next=request.url))
        return f(*args, **kwargs)
    return decorated_function
```

The ```next``` value will exist in request.args after a GET request for the login page. You’ll have to pass it along when sending the POST request from the login form. You can do this with a hidden input tag, then retrieve it from request.form when logging the user in.

```html
<input type="hidden" value="{{ request.args.get('next', '') }}"/>
```



### 

_Login form template_

The login template needs to be updated to render the form. These changes are shown below.

**Add to  *app/templates/auth/login.html*:** 

```html
{% extends "base.html" %}
{% import "bootstrap/wtf.html" as wtf %}
{% block title %}Flasky - Login{% endblock %}
{% block page_content %}
<div class="page-header">
    <h1>Login</h1>
</div>
<div class="col-md-4">
    {{ wtf.quick_form(form) }}
</div>
{% endblock %}
```

### Signing Users Out

The implementation of the logout route is shown below.

_Logout route_

**Add to *app/auth/views.py*:** 

```py
from flask_login import logout_user, login_required

@auth.route('/logout')
@login_required
def logout():
    logout_user()
    flash('You have been logged out.')
    return redirect(url_for('main.index'))
```

To log a user out, Flask-Login’s ```logout_user()``` function is called to remove and reset the user session. The logout is completed with a flash message that confirms the action and a redirect to the home page.

_Additional Note - ```load_user()``` function:_

### About ```load_user()```

Flask-login will try and load a user BEFORE every request. It is used to check what user id is in the current session and will load the user object for that id.

```
@login_manager.user_loader
def load_user(userid):
    #print 'this is executed',userid
    return user(userid, 'asdf')        
```

If you look at the Flask-login source code on github, there is a line under function ```init_app``` which goes:

```py
app.before_request(self._load_user)
```

So before every request, the ```_load_user``` function is called. The ```_load_user``` functions actually calls another function ```reload_user()``` based on conditions. And finally, ```reload_user()``` function calls your callback function that you wrote (```load_user()``` in your example).

### Understanding How Flask-Login Works

Flask-Login is a fairly small extension, but due to the many moving pieces involved in the authentication flow, Flask users often have trouble understanding how the extension works. The following is the sequence of operations that occur when a user logs in to the system:

1. The user navigates to *http://localhost:5000/auth/login* by clicking on the “Log In” link. The handler for this URL returns the login form template.

2. The user enters their username and password, and presses the Submit button. The same handler is invoked again, but now as a ```POST``` request instead of ```GET```.

    * The handler validates the credentials submitted with the form, and then invokes Flask-Login’s ```login_user()``` function to log the user in.
    
    * The ```login_user()``` function writes the ID of the user to the user session as a string. **(See ```login_user()``` function section below to understand how it works)**
    
    * The view function returns with a redirect to the home page.

3. The browser receives the redirect and requests the home page.

    * The view function for the home page is invoked, and it triggers the rendering of the main Jinja2 template.

    * During the rendering of the Jinja2 template, a reference to Flask-Login’s ```current_user``` appears for the first time.
    
    * The ```current_user``` context variable does not have a value assigned for this request yet, so it invokes Flask-Login’s internal function ```_get_user()``` to find out who the user is.

    * The ```_get_user()``` function checks if there is a user ID stored in the user session. If there isn’t one, it returns an instance of Flask-Login’s ```AnonymousUser```. If there is an ID, it invokes the function that the application registered with the ```user_loader``` decorator, with the ID as its argument.
    
    * The application’s ```user_loader``` handler reads the user from the database and returns it. Flask-Login assigns it to the ```current_user``` context variable for the current request.

    * The template receives the newly assigned value of ```current_user```.

The ```login_required``` decorator builds on top of the ```current_user``` context variable by only allowing the decorated view function to run when the expression ```current_user.is_authenticated``` is ```True```. The ```logout_user()``` function simply deletes the user ID from the user session.

#### Machete - Flujograma
**->** = _calls function_

-> ```login_user()``` stores ```user_id``` in ```session``` through ```user``` object generated from query to data base

Template's ```current_user.is_authenticated``` -> ```_get_user()``` checks ID in session and if there is -> ```user_loader```  decorator with ID as argument, which reads the user from the database, returns it and assign it to ```current_user``` context variable for current request.   

#### ```login_user()``` function

```py
def login_user(user, remember=False, duration=None, force=False, fresh=True):
    '''
    Logs a user in. You should pass the actual user object to this. If the
    user's `is_active` property is ``False``, they will not be logged in
    unless `force` is ``True``.

    This will return ``True`` if the log in attempt succeeds, and ``False`` if
    it fails (i.e. because the user is inactive).

    :param user: The user object to log in.
    :type user: object
    :param remember: Whether to remember the user after their session expires.
        Defaults to ``False``.
    :type remember: bool
    :param duration: The amount of time before the remember cookie expires. If
        ``None`` the value set in the settings is used. Defaults to ``None``.
    :type duration: :class:`datetime.timedelta`
    :param force: If the user is inactive, setting this to ``True`` will log
        them in regardless. Defaults to ``False``.
    :type force: bool
    :param fresh: setting this to ``False`` will log in the user with a session
        marked as not "fresh". Defaults to ``True``.
    :type fresh: bool
    '''
    if not force and not user.is_active:
        return False

    user_id = getattr(user, current_app.login_manager.id_attribute)()
    session['_user_id'] = user_id
    session['_fresh'] = fresh
    session['_id'] = current_app.login_manager._session_identifier_generator()

    if remember:
        session['_remember'] = 'set'
        if duration is not None:
            try:
                # equal to timedelta.total_seconds() but works with Python 2.6
                session['_remember_seconds'] = (duration.microseconds +
                                                (duration.seconds +
                                                 duration.days * 24 * 3600) *
                                                10**6) / 10.0**6
            except AttributeError:
                raise Exception('duration must be a datetime.timedelta, '
                                'instead got: {0}'.format(duration))

    current_app.login_manager._update_request_context_with_user(user)
    user_logged_in.send(current_app._get_current_object(), user=_get_user())
    return True
```

### Testing Logins

To verify that the login functionality is working, the home page can be updated to greet the logged-in user by name. The template section that generates the greeting is shown below.

_Greeting the logged-in user_

**Modify _app/templates/index.html_ to this:** 

```html
Hello,
{% if current_user.is_authenticated %}
{{ current_user.username }}
{% else %}
Stranger
{% endif %}!
```

In this template once again ```current_user.is_authenticated``` is used to determine whether the user is logged in.
Because no user registration functionality has been built, a new user can only be registered from the shell at this time:

```shell
(venv) $ $ flask shell
>>> u = User(email='john@example.com', username='john', password='cat')
>>> db.session.add(u)
>>> db.session.commit()
```

The user created previously can now log in.

## New User Registration

When new users want to become members of the application, they must register with it so that they are known and can log in. A link in the login page will send them to a registration page, where they can enter their email address, username, and password.

### Adding a User Registration Form

The form that will be used in the registration page asks the user to enter an email address, username, and password.

_User registration form_

**Add to _app/auth/forms.py_:** 

```py
from flask_wtf import FlaskForm
from wtforms import StringField, PasswordField, BooleanField, SubmitField
from wtforms.validators import DataRequired, Length, Email, Regexp, EqualTo
from wtforms import ValidationError
from ..models import User

class RegistrationForm(FlaskForm):
    email = StringField('Email', validators=[DataRequired(), Length(1, 64), Email()])
    username = StringField('Username', validators=[
        DataRequired(), Length(1, 64),
        Regexp('^[A-Za-z][A-Za-z0-9_.]*$', 0, 'Usernames must have only letters, numbers, dots or underscores')])
    password = PasswordField('Password', validators=[DataRequired(), EqualTo('password2', message='Passwords must match.')])
    password2 = PasswordField('Confirm password', validators=[DataRequired()])
    submit = SubmitField('Register')

    def validate_email(self, field):
        if User.query.filter_by(email=field.data.lower()).first():
            raise ValidationError('Email already registered.')

    def validate_username(self, field):
        if User.query.filter_by(username=field.data).first():
            raise ValidationError('Username already in use.')
```

This form uses the ```Regexp``` validator from WTForms to ensure that the username field starts with a letter and only contains letters, numbers, underscores, and dots. The two arguments to the validator that follow the regular expression are the regular expression flags and the error message to display on failure.

The password is entered twice as a safety measure, but this step makes it necessary to validate that the two password fields have the same content, which is done with another validator from WTForms called ```EqualTo```. This validator is attached to one of the password fields with the name of the other field given as an argument.

**IMPORTANT!**

This form also has two custom validators implemented as methods. When a form defines a method with the prefix ```validate_``` followed by the name of a field, the method is invoked in addition to any regularly defined validators. In this case, the custom validators for ```email``` and ```username``` ensure that the values given are not duplicates. The custom validators indicate a validation error by raising a ```ValidationError``` exception with the text of the error message as an argument.

The template that presents this form is called _/templates/auth/register.html_. Like the login template, this one also renders the form with ```wtf.quick_form()```.

**Create this at _app/templates/auth/registration.html_:**

```html
{% extends "base.html" %}
{% import "bootstrap/wtf.html" as wtf %}

{% block title %}Flasky - Register{% endblock %}


{% block page_content %}
<div class="page-header">
    <h1>Register</h1>
</div>
<div class="col-md-4">
    {{ wtf.quick_form(form) }}
</div>
{% endblock %}
```

The registration page needs to be linked from the login page so that users who don’t have an account can easily find it. This change is shown in Example 8-16.

_Link to the registration page_

**Add to _app/templates/auth/login.html_:** 

```html
<p>
    New user?
    <a href="{{ url_for('auth.register') }}">
        Click here to register
    </a>
</p>
```

### Registering New Users

Handling user registrations does not present any big surprises. When the registration form is submitted and validated, a new user is added to the database using the information provided by the user. The view function that performs this task is shown below. 

_User registration route_

**Add this to _app/auth/views.py_:**

 
```py
@auth.route('/register', methods=['GET', 'POST'])
def register():
    form = RegistrationForm()
    if form.validate_on_submit():
        user = User(email=form.email.data, username=form.username.data, password=form.password.data)
        db.session.add(user)
        db.session.commit()
        flash('You can now login.')
        return redirect(url_for('auth.login'))
    return render_template('auth/register.html', form=form)
```

### Account Confirmation

For certain types of applications, it is important to ensure that the user information provided during registration is valid. A common requirement is to ensure that the user can be reached through the provided email address.

To validate the email address, applications send a confirmation email to users immediately after they register. The new account is initially marked as unconfirmed until the instructions in the email are followed, which proves that the user has received the email. The account confirmation procedure usually involves clicking a specially crafted URL link that includes a confirmation token.

### Generating Confirmation Tokens with ```itsdangerous```

The simplest account confirmation link would be a URL with the format _http:// www.example.com/auth/confirm/<id>_ included in the confirmation email, where ```<id>``` is the numeric ```id``` assigned to the user in the database. When the user clicks the link, the view function that handles this route receives the user ```id``` to confirm as an argument and can easily update the confirmed status of the user. 

But this is obviously not a secure implementation, as any user who figures out the format of the confirmation links will be able to confirm arbitrary accounts just by sending random numbers in the URL. The idea is to replace the ```<id>``` in the URL with a token that contains the same information, but in such a way that only the server can generate valid confirmation URLs.

Flask uses cryptographically signed cookies to protect the content of user sessions against tampering. **The user session cookies contain a cryptographic signature generated by a package called ```itsdangerous```**. If the contents of the user session is altered, the signature will not match the content anymore, so Flask discards the session and starts a new one. The same concept can be applied to confirmation tokens. The following is a short shell session that shows how ```itsdangerous``` can generate a signed token that contains a user ```id``` inside:

```shell
(venv) $ flask shell
>>> from itsdangerous import TimedJSONWebSignatureSerializer as Serializer
>>> s = Serializer(app.config['SECRET_KEY'], expires_in=3600)
>>> token = s.dumps({ 'confirm': 23 })
>>> token
'eyJhbGciOiJIUzI1NiIsImV4cCI6MTM4MTcxODU1OCwiaWF0IjoxMzgxNzE0OTU4fQ.ey ...'
>>> data = s.loads(token)
>>> data
{'confirm': 23}
```

The ```itsdangerous``` package provides several types of token generators. Among them, the class ```TimedJSONWebSignatureSerializer``` generates JSON Web Signatures (JWSs) with a time expiration. The constructor of this class takes an encryption key as an argument, which in a Flask application can be the configured ```SECRET_KEY```. 

The ```dumps()``` method generates a cryptographic signature for the data given as an argument and then serializes the data plus the signature as a convenient token string. The ```expires_in``` argument sets an expiration time for the token, expressed in seconds. 

To decode the token, the serializer object provides a ```loads()``` method that takes the token as its only argument. The function verifies the signature and the expiration time and, if both are valid, it returns the original data. When the ```loads()``` method is given an invalid token or a valid token that is expired, an exception is raised.

Token generation and verification using this functionality can be added to the ```User``` model. The changes are shown below.

_User account confirmation_

**Add to _app/models.py_:** 

```py
from itsdangerous import TimedJSONWebSignatureSerializer as Serializer
from flask import current_app
from . import db
class User(UserMixin, db.Model):
# ...
confirmed = db.Column(db.Boolean, default=False)

def generate_confirmation_token(self, expiration=3600):
    s = Serializer(current_app.config['SECRET_KEY'], expiration)
    return s.dumps({'confirm': self.id}).decode('utf-8')

def confirm(self, token):
    s = Serializer(current_app.config['SECRET_KEY'])
    try:
        data = s.loads(token.encode('utf-8'))
    except:
        return False
    if data.get('confirm') != self.id:
        return False
    self.confirmed = True
    db.session.add(self)
    return True
```

The ```generate_confirmation_token()``` method generates a token with a default validity time of one hour. The ```confirm()``` method verifies the token and, if valid, sets the new ```confirmed``` attribute in the user model to ```True```. 

In addition to verifying the token, the ```confirm()``` function checks that the ```id``` from the token matches the logged-in user, which is stored in ```current_user```. This ensures that a confirmation token for a given user cannot be used to confirm a different user.

The two new methods added to the ```User``` model are easily tested in unit tests. You can find the unit tests in the GitHub repository for the application.

### Sending Confirmation Emails

The current _/register_ route redirects to _/index_ after adding the new user to the database.
Before redirecting, this route now needs to send the confirmation email. This change is shown below.

Registration route with confirmation email

**Add to _app/auth/views.py_:** 

```py
from ..email import send_email
@auth.route('/register', methods=['GET', 'POST'])
def register():
    form = RegistrationForm()
    if form.validate_on_submit():
        user = User(email=form.email.data.lower(),
                    username=form.username.data,
                    password=form.password.data)
        db.session.add(user)
        db.session.commit()
        token = user.generate_confirmation_token()
        send_email(user.email, 'Confirm Your Account',
                   'auth/email/confirm', user=user, token=token)
        flash('A confirmation email has been sent to you by email.')
        return redirect(url_for('auth.login'))
    return render_template('auth/register.html', form=form)
```

Note that a ```db.session.commit()``` call had to be added before the confirmation email is sent out. The problem is that new users get assigned an ```id``` when they are committed to the database, and this ```id``` is needed to generate the confirmation token. 

The email templates used by the authentication blueprint will be added in the _templates/auth/email_ directory to keep them separate from the HTML templates. For each email two templates are needed for the plain-text and HTML versions of the body. The following example shows the plain-text version of the confirmation email template, and you can find the equivalent HTML version in the GitHub repository.

_Text body of confirmation email_

**Create at _app/templates/auth/email/confirm.txt_:** 

```
Dear {{ user.username }},
Welcome to Flasky!
To confirm your account please click on the following link:
{{ url_for('auth.confirm', token=token, _external=True) }}
Sincerely,
The Flasky Team
Note: replies to this email address are not monitored.
```

By default, ```url_for()``` generates relative URLs; so, for example, ```url_for('auth.confirm', token='abc')``` returns the string ```'/auth/confirm/abc'```. This, of course, is not a valid URL that can be sent in an email, since it is only the path portion of the URL. Relative URLs work fine when they are used within the context of a web page because the browser converts them to absolute URLs by adding the hostname and port number from the current page, but when sending a URL over email there is no such context. The ```_external=True``` argument is added to the ```url_for()``` call to request a fully qualified URL that includes the scheme (http:// or https://), hostname, and port.

The view function that confirms accounts is shown below:

_Confirming a user account_

**Add to _app/auth/views.py_:**

```py
from flask_login import current_user

@auth.route('/confirm/<token>')
@login_required
def confirm(token):
    if current_user.confirmed:
        return redirect(url_for('main.index'))
    if current_user.confirm(token):
        db.session.commit()
        flash('You have confirmed your account. Thanks!')
    else:
        flash('The confirmation link is invalid or has expired.')
    return redirect(url_for('main.index'))
```

This route is protected with the ```login_required``` decorator from Flask-Login, so that when the users click on the link from the confirmation email they are asked to log in before they reach this view function. 

The function first checks if the logged-in user is already confirmed, and in that case it redirects to the home page. This can prevent unnecessary work if a user clicks the confirmation token multiple times by mistake. 

Because the actual token confirmation is done entirely in the ```User``` model, all the view function needs to do is call the ```confirm()``` method and then flash a message according to the result. When the confirmation succeeds, the ```User``` model’s ```confirmed``` attribute is changed and added to the session and then the database session is committed. 

Each application can decide what unconfirmed users are allowed to do before they confirm their accounts. One possibility is to allow unconfirmed users to log in, but only show them a page that asks them to confirm their accounts before they can gain further access. 

This step can be done using Flask’s ```before_request``` hook, which was briefly described in Chapter 2. From a blueprint, the ```before_request``` hook applies only to requests that belong to the blueprint. To install a blueprint hook for all application requests, the before_app_request decorator must be used instead. Example 8-22 shows how this handler is implemented.

_Filtering unconfirmed accounts with the ```before_app_request``` handler_

**Add to _app/auth/views.py_:** 

```py
@auth.before_app_request
def before_request():
    if current_user.is_authenticated \
            and not current_user.confirmed \
            and request.blueprint != 'auth' \
            and request.endpoint != 'static':
        return redirect(url_for('auth.unconfirmed'))

@auth.route('/unconfirmed')
def unconfirmed():
    if current_user.is_anonymous or current_user.confirmed:
        return redirect(url_for('main.index'))
    return render_template('auth/unconfirmed.html')
```

The ```before_app_request``` handler will intercept a request when three conditions are true:

1. A user is logged in (```current_user.is_authenticated``` is ```True```).
2. The account for the user is not confirmed.
3. The requested URL is outside of the authentication blueprint and is not for a static file. Access to the authentication routes needs to be granted, as those are the routes that will enable the user to confirm the account or perform other account management functions.

If these three conditions are met, then a redirect is issued to a new _/auth/unconfirmed_ route that shows a page with information about account confirmation.

When a ```before_request``` or ```before_app_request``` callback returns a response or a redirect, Flask sends that to the client without invoking the view function associated with the request. This effectively allows these callbacks to intercept a request when necessary.

The page that is presented to unconfirmed users just renders a template that gives users instructions for how to confirm their accounts and offers a link to request a new confirmation email, in case the original email was lost. The route that resends the confirmation email is shown below.

_Resending the account confirmation email_

**Add to _app/auth/views.py_:** 

```py
@auth.route('/confirm')
@login_required
def resend_confirmation():
    token = current_user.generate_confirmation_token()
    send_email(current_user.email, 'Confirm Your Account',
               'auth/email/confirm', user=current_user, token=token)
    flash('A new confirmation email has been sent to you by email.')
    return redirect(url_for('main.index'))
```

This route repeats what was done in the registration route using ```current_user```, the user who is logged in, as the target user. This route is also protected with ```login_required``` to ensure that when it is accessed, the user that is making the request is authenticated.

## Account Management

Users who have accounts with the application may need to make changes to their accounts from time to time. The following tasks can be added to the authentication blueprint using the techniques presented in this chapter:

**Password updates**

Security-conscious users may want to change their passwords periodically. This is an easy feature to implement, because as long as the user is logged in, it is safe to present a form that asks for the old password and a new password to replace it. This feature is implemented as commit 8f in the GitHub repository. As part of this change, the “Log Out” link in the navigation bar was refactored into a dropdown that contains the “Change Password” and “Log Out” links.

**Password resets**

To avoid locking users out of the application when they forget their passwords, a password reset option can be offered. To implement password resets in a secure way, it is necessary to use tokens similar to those used to confirm accounts. When a user requests a password reset, an email with a reset token is sent to the registered email address. The user then clicks the link in the email and, after the token is verified, a form is presented where a new password can be entered. This feature is implemented as commit 8g in the GitHub repository.

**Email address changes**

Users can be given the option to change their registered email address, but before the new address is accepted it must be verified with a confirmation email. To use this feature, the user enters the new email address in a form. To confirm the email address, a token is emailed to that address. When the server receives the token back, it can update the user object. While the server waits to receive the token, it can store the new email address in a new database field reserved for pending email addresses, or it can store the address in the token along with the id. This feature is implemented as commit 8h in the GitHub repository.

