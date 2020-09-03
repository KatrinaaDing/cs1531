[Return to README.md](https://github.com/KatrinaaDing/cs1531/blob/master/README.md)

# Content Table

* [Set up](#set-up)
* [Structure](#structure)
	* [debug mode](#debug-mode)
	* [set running port](#set-running-port)
* [Routes](#routes)
	* [using variable](#using-variable)
	* [defining method](#defining-method)
* [Jinja](#Jinja)
	* [passing variable into html](#pvih)
	* [for loop](#for-loop)
	* [if statement](#if-statement)
	* [filter](#filter)
* [Template Inheritance](#Template-Inheritance)
* [Navigation (href)](#n)
	
	* [url_for](#uf)
* [Forms](#Forms)
	* [Redirecting](#Redirecting) 

	
# Flask

## set up

1. install virtual environment `virtualenv --python=python3.6 env`
2. activate environment `source env/bin/activate`
3. install flask `pip install flask`

## structure

```python
from flask import Flask # import Flask library

# create a flask project, assigning to a variable called app
app = Flask(__name__)

# a handler of root URL
@app.route("/")
def index():
	return "Hello world!"
	

# to run the project
if __name__=="__main__": # optionally add a name guard
	app.run()

```

terminal will indicate the port it's running on. 

```python
...
* Running on http://127.0.0.1:5000/
...
```
[Return to Content Table](#Content-Table)
### debug mode
Debug mode allows us to refresh the page without close (quit) the application.
To endter debug mode, change the run mode:

```python
app.run(debug=True)
```
[Return to Content Table](#Content-Table)
### set running port
By default the port is 5000.

```python
app.run(port=8085)
```
[Return to Content Table](#Content-Table)
## routes


example: `@app.route("/")` `@app.route("/home")`  
This means: when the project goes to the specific route, will run the function under this decorator. The function **must** return a string.  

### Using variable
We can wrap a variable (name) within the route. example:  

Instead of:

``` python
@app.route("/home/sam")
def home():
	...
	
@app.route("/home/amy")
def home1():
	...
	
@app.route("/home/ben")
def home2():
	...
```
We can do:  

```python
@app.route("/home/<name>")
def home(name):
	...
```
_Note: the function variable name **must match** the variable name inside route._

[Return to Content Table](#Content-Table)
### defining method
By default, method is set to `GET`. To change method, define in route:

```python
# default
@app.route("/home", methods=["GET"]

# another useful method. In this case the 
# url only accept "POST" request
@app.route("/home", methods=["POST"]

# to use both
@app.route("/home", methods=["GET", "POST"])
```
[Return to Content Table](#Content-Table)

## Jinja
in the directory, create a new directory called `templates`, and inside `/templates` create a new `.html` file.

To render the template, inside `app.py`, import `render_template` library, and pass in the html file name into the function:

```python
from falsk import Flask, render_template 

app = Flask(__name__)

@app.route("/")
def index():
	# pass in html file into render_template() and return the whole fucntion
	return render_template("index.html")

...

app.run(debug=True)
```
[Return to Content Table](#Content-Table)


### passing variable into html
Jinja2 allows dynamic content on websites. To pass in a variable from `app.py` to the html file:  

inside .py file:

```python
...

@app.route("/profile/<name>")
def profile(name):
	# pass in the html file and variable
	return render_template("names.html", variable_name=name)
	
...
```

inside the html file:

```html
...

<body>
	# double curly brackets with the variable name passed in from .py file
	You are on {{variable_name}}
</body>

...
```
Jinja can pass in any type of variable (such as int, strint, list, etc.) **except for** functions (`print("HELLO")`) and assignment (`x = 5`).

[Return to Content Table](#Content-Table)

### for loop
Jinja allows us to do `for` loop in html file with control struct syntax.

In python:

```python
x = [1, 2, 3]
for i in x:
	print(i)
```

In Jinja:

```html
...
<body>
	# the list x is passed in from .py file
	{% for i in x 5}	# indicate start of loop
		{{i}}			# replace {{}} with i
	{% endfor %}		# indicate end of loop


</body>
...
```

[Return to Content Table](#Content-Table)

### if statement
Also using control structure syntax:

In python:#

```python
if y > 10:
	print("This is large")
elif y > 5;
	print("This is a semi large")
else:
	print("This is a small")
```

In Jinja:

```html
...
<body>
	# again, y is passed in from outside
	{% if y > 10%}
		This is a large
		
	{% elif y > 5 %}
		This is a semi large
		
	{% else %}
		This is a small
		
	{% endif %} # must indicate the end
</body>
...
```

[Return to Content Table](#Content-Table)

### filter
Jinja has useful filters similar to python's method, with syntax `|`.

For example, if want to capitalize the first letter in a list of string:

```html
...
<body>
	{% for name in nale_list %}
		{{ name | capitalize }}
	{% endfor %}
</body>
...
```
For more plz visit [Jinja Homepage](http://jinja.pocoo.org/).

[Return to Content Table](#Content-Table)
<a id='ti'></a>
## Template Inheritance
A layout html file will be like a template, with a flexible block, and any other html file can be the content filled in the block.

To define a block in `layout.html`:  

```html
...
<body>
	<h1>Hello World!</h1>
		{% bock var_name %}
		{% endblock %}
	<footer>Thank you for visiting!</footer>

</body>
...
```

In the inheritance html file(e.g. `home.html`): 

```html
# only need to write the block content
{% extends "lay.out.html" %}  
{% block var_name %}
	Welcome to my page!
{% endblock %}

```

Displaying `home.html` will be:

```html
Hello World!
Welcome to my page!
Thank you for visiting my webpage!
```

[Return to Content Table](#Content-Table)


## Navigation (href)
a link in html is defined by:

```html
<a href="/somepage">Goto page</a>
```

[Return to Content Table](#Content-Table)


### url_for
`url_for()` automatically return the coresponnding route of an specific function name.  
Has to `form flask import url_for`.

```python
@app.route("/")
def index():
	return render_template("index.html")
	
@app.route("/names")
def names():
	return render_template("names.html")

@app.route("/home/<name>")
def home_name(name):
	return render_template("home.html", names=name)
	
# url_for("index") --> /
# url_for("index") --> /names
# url_for("home_name", name="mary") --> /home/mary

```

Using `url_for` within a link (Benifit: don't have to modify every url):

```html
# Notes: must use double large brackets and double quaotation
<a href="{{ url_for('names') }}">Go to Names</a>

# the link will go to the route that defined in names()
```

[Return to Content Table](#Content-Table)


## Forms
To generate an imput text box on webpage:

```html
Username: <input placeholder="Enter Text..." name="username"/>
# input: the text box
# placeholder: comment displayed in the box
# name: the name of the box

Password: <input: placeholder="Enter Password.." name="password" type="password" />
# "password" type will display all input as "*" 
```

a submit button:

```html
<input type="submit" value="Submit">
# this will be a button instead of text box as it has "submit" type
```

Full version of a form (in `login.html`):

```html
# "POST" for pushing data to the server
# if want to use "POST" in this route, have to define method in the .py file (see defining method)
<form method="POST">
	Username: <input placeholder="Enter Text..." name="username"/> <br/> # newline symbol
	Password: <input: placeholder="Enter Password.." name="password" type="password" />
	<input type="submit" value="Submit">
	# the submit button will submit the infomation to server
</form>
```

To handle the data sent from the form, in `app.py`:

```python
@app.route("/login", methods=["GET", "POST"])
def login():
	# only with "POST" request(submit form in this case) this will run
	if request.method == "POST":
		# get data by pass in the name of the particular input from form
		username = request.form["username"]
		password = request.form["password"]
		
		# redirect the user the home page
		return redirect(url_for("index"))
	return render_template("login.html")

```
[Return to Content Table](#Content-Table)

### Redirecting
Use `redirect()` to login different user.  
Has to `from flask import redirect`.

 
