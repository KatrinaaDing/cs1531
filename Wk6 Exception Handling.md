# Exception Handling

Example of built-in exceptions:

* ZeroDivisionError: division by zero
* TypeError: unsupported operand type(s)

## Exception
Exception is a base class and all errors are childclass.  
Hence we can make own error inheriting from the base exception class.  
e.g. `class BookingError(Exception)`  


### raise Exception()
`raise Exception()` means if the program reach that line, stop the execution of the code.

### try and except

```python
try:
	function()
except:
	# Exception was raised
else:
	# code run without exception
finally:
	# no matter there is or isn't an exception, run this code
```

example:

```python
def add(x, y):
	try:
		return x + y
	except: 
		print("Please enter only numbers")
```
In the code, instead of stop the execution of the code, use `except` to catch the Error and execute `print()`. So the code will keep excuting (but giving wrong output).  

We can choose a **specific** Error to handle:

```python
# capturing all kinds of error
except:
	...

# only capturing TypeError (i.e. run the code only for TypeError)
except TypeError:
	...

# er will be the TypeError object in the code
except TypeError as er:
	...
	
```

## Application
Exception is best used for checking unexpected input before pass it into funciton.

More useful way is to use with test function.

example:

```python
# define a personal (not built-in) error
class NumError(Exception):
	def __init__(self, msg):
		self.msg = msg
	
	def __str__(self):
		return self.msg

# a function that check if the input is valid
def add(a, b):
	if NaN(a) or NaN(b):
		raise NumError("input is not a nubmer")
	
	if a < 0 or b < 0:
		raise NumErro("only accept +ve number)
	
	sum = a + b
	return sum

# a simple test example (using only assert())
def test_simple():
	sum = add(3, 4)
	assert(sum == 7)

# test with try and except
def test_non_num():
	# try this action, which is supposed to be false
	try:
		sum = add("a",5)
	
	# as in "try", there is an excpected Error, 
	# assert that there must be an error and 
	# the error msg must be "input is not a number"
	except NumError as err:
		assert(err.msg == "input is not a nubmer")
	
	# If the expected Error isn't captured,
	# the test must indicate "fail"
	else:
		assert(False)


```
