
# Content Table

* [Nested Function](#Nested-Function)
* [Decorator](#Decorator)

[Return to README.md](https://github.com/KatrinaaDing/cs1531/blob/master/README.md)


# Nested Function
Python allows to assign a function reference to a variable.  
e.g.

```python
def hello():
	print("hello world")

my_function = hello
my_function()

=> hello world
```
Using nested function:

```python
def get_greeter():
	message = "Hello"
	
	def greeter():		# insede get_greeter()
		print(message)	# can reference a variable outside it's scope
	
	return greeter

my_func = get_greeter()
myfunc()
greeter()

=> Hello
=> ERROR	# as greeter() is inside get_greeter's, not global scope
```
[python can only access variable outward, but not inward]

Function can be pass in to another function as parameter.  
e.g.

```python
def get_lo(message):
	return message.lower()
	
def get_up(message):
	return message.upper()

def greet(text_transformer):
	message = text_transformer("Hello World")
	print(message)

greet(get_lo)	
greet(get_up)

=> hello world
=> HELLO WORLD
```
`get_lo/up` is assigned to the variable `text_transformer`, and `text_transformer`, which actually is `get_lo/up`, accept the parameter `"Hello Word"`, then `get_lo/up` return the result and pass it to `message` inside `greet()`.

For further usage see *Decorator* below.

[Content Table](#Content-Table)

# Decorator

```python
@my_decorator	# "my_function() is @ my_decorator"
def my_function():	
	...
```
Decorator is dynamically alter the functionality of a function, like a **wrapper** to the function and let us execute **specific code** before and after the function runs.

The **specific code** can be written by our own or use python proporties.

Decorator can accept custom parameters.  
example:

```python
def add_name(name):
	def my_decorator(function):		# function accepted from global scope
		def add_name_wrapper():
			return function() + name
		
		return add_name_wrapper
	return my_decorator

@add_name("John")	# pass in "John" as parameter
def say_hello():	# [say_hello() might be auto passed into decorator]
	return "Hello "

@add_name("Lucy")
def say_hi():
	reuturn "Hi "

print(say_hello())
print(say_hi())

=> Hello John
=> Hi Lucy
```
[Content Table](#Content-Table)
