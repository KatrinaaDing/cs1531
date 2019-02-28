## Functions
The keyword to define funciton is `def`.


```python
def funcName(arg1, arg2):
	...
	return sth 	
	
```
If not returning anything, ==python return `None` by default==.

As C, function should be defined **before** calling it.

####Defult argument
python support "default argument" in function.

```python
def print_hello(name="World"):
	print("Hello " + name)

print_hello("Anna")		# Hello Anna
print_hello()			# Hello World
```
####Flexible arguments
python funciton allow to accept arbitary argument.  

```python
def add_numbers(*numbers):
	sum = 0
	for number in numbers:
		sum += number
	return sum

result = add_nubmers(5, 10, 8, 3)
print(result)	# 26
```

## Virtual Environment
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
## Modules
 Just `.py` files.
 
 In helper.py:
  
 ```python
 def get_marks():
 	...
 def average(numbers):
 	... 
 
 ```
 To use those functions, in marks_calculator.py:  
 
```python
from helper import get_marks,average # or simply import *helper.py

marks = get_marks()
ave = average(marks)
print(ave)
```
or

```python
import helper

marks = helper.get_marks()
ave = healper.average(marks)
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

## List Data Structure
List is a collection data type.  
Four main collection data types:

* List (==ordered, mutable, allows duplicate==)
* Tuples
* Sets
* Dictoinaries



```python
list = [...]
for i in range(len(list)):
	element = mylist[i]
	print(element)
```
is equivalent to 

```python
list = [...]
for letter in my_list:
	print(letter)
```

###list comprehensions
Can create list in a very concise way.
`my_list = [expression for x in another_list]`  
It will evaluate the expression on each element x in another_list.  

example:

```python
>>> my_numbers = [x for x in range(1, 10)]
[1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> my_numbers = [x for x in range(1, 10) if x % 2 == 0]
>>> my_numbers
[2, 4, 6, 8]
>>> halved = [x/2 for x in my_numbers]
[1.0, 2.0, 3.0, 4.0]
```

## More Data Structures
###Sets
`fruits = {"oragne", "mango", "pineapple"}`  
Sets don't support indexing and item assignment. 

```python
>>> fruits = {"oragne", "mango", "pineapple"}
>>> fruits[1]
error  # cuz set doesn't have any order
>>> fruits[1] = "dfd"
error
```

**.add()**, adding item into set.  
**.remove()**, removing item from the set.  
**Set doesn't allow duplicate, so adding existing item will change nothing.

###Dictionary
Similar to a list, being indexed using type rather than number.  
**Key** is the string before `:`, and followed by a value

example:

```python
>>> my_dict = {}
>>> marks = {"A": 72, "B": 95, "H": 85, "G": 95}
>>> marks
{"A": 72, "B": 95, "H": 85, "G": 95}
>>> marks["A"]
72
>>> marks["H"] = 80 # item can be modified
>>> marks["H"]
80
```

Using with `for` loop:

```python
marks = {"A": 72, "B": 95, "H": 85, "G": 95}
for key in marks.keys():
	print("Key is", key)
	print("Value", marks[key])

=> # out put is not in order
Key is H
Value 85
Key is G
Value 95
Key is A
Value 72
Key is B
Value 95
```

Use dictonary to count object:

```python
fruits = []

choice = ""
while choice != "q":
	choice = input(enter another fruit")
	fruits.append(choice)
	
fruit_quantities = {}
for fruit in fruits:
	if fruit in fruit_quantites:
		fruit_quantities[fruit] += 1
	else:
		fruit_quantities[fruit] = 1

for fruit in fruit_quantities:
	print(fruit, fruit_quantities[fruit])
	
=>
lemon 4
banana 1
mango 1
q 1		# it still taking the "q" input and I don't know why
aaple 3
```

