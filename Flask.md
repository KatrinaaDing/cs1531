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
app.run()

```

terminal will indicate the port it's running on. 

```python
...
* Running on http://127.0.0.1:5000/
...
```

### debug mode
Debug mode allows us to refresh the page without close (quit) the application.
To endter debug mode, change the run mode:

```python
app.run(debug=True)
```

### set running port
By default the port is 5000.

```python
app.run(port=8085)
``` 

## @app.route()


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

### pasing variable into html
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
