# Content Table

* [Functions](#Functions)
	* [Default arguments](#Default-arguments)
	* [Flexible arguments](#Flexible-arguments)
* [Modules](#Modules)
* [Virtual Environment](#Virtual-Environment)

[Return to README.md](https://github.com/KatrinaaDing/cs1531/blob/master/README.md)



# Functions

The keyword to define funciton is `def`.


```python
def funcName(arg1, arg2):
	...
	return sth 	
```
If not returning anything, Python return `None` (similar to `NULL` in C) **by default.**

As C, function should be defined **before** calling it.



## Default arguments

python support "default argument" in function.

```python
def print_hello(name="World"):
	print("Hello " + name)

print_hello("Anna")		# Hello Anna
print_hello()			# Hello World
```


## Flexible arguments

python funciton allow to accept arbitrary argument.  

```python
def add_numbers(*numbers):
	sum = 0
	for number in numbers:
		sum += number
	return sum

result = add_nubmers(5, 10, 8, 3)
print(result)	# 26
```
[Return to Content Table](#Content-Table)



# Modules

 Just `.py` files.

For example, if we want to call functions from helper.py in marks_calculator.py:

 In helper.py:

 ```python
def get_marks():
 	...
    return marks

def average(numbers):
 	... 
    return avg
 
 ```
 To use those functions, in marks_calculator.py:  

```python
from helper import get_marks,average 

marks = get_marks()
ave = average(marks)
print(ave)
```
or

```python
import helper

marks = helper.get_marks()
ave = helper.average(marks)
print(ave)
```
common library in python:  

* **math** (for calculating)
* **random** (for enerating random nubmers)
* **os** (providing interface for operating system functionality such as opening files, changing directories or accessing environment variables)
* **sys** (for system specific parameters and functions such as using `argv` to get the list of command-line arguments pass into python script)

example:

```python
import math
x = math.sqrt(16)
print(x)
```
*Note: divide `/` always return `float`, so we need:*

```python
int(x/y)
```
or

```python
x//y
```
to get the integer result.

[Return to Content Table](#Content-Table)



# Virtual Environment

To install:  

1. `sudo apt install python3-pip`
2. `pip3 install virtualenv`. 
3.  `mkdir xxxx` make new directory for project
4. cd into the directory
5. `virtualenv --python=python3 venv` choosing version of python and name the enviornment
6. `. venv/bin/activate` activate the virtual environment using it's name
7. `pip3 install numpy` install package for python
8. `pip3 freeze` showing package and it's version in this environment
9. `deactivate` to deactivate the environment

[More Here](http://www.cse.unsw.edu.au/~cs1531/19T1/extra/virtualenv.html)

[Return to Content Table](#Content-Table)
