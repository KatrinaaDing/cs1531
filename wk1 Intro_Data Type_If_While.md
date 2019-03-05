<a id="ct"></a>

# Content Table
* [Python](#p)
* [String and Data Type](#sadt)
* [`if` Statement](#if)
* [`while` Loop](#wl)
* [Data Structure](#ds)
	* [List](#l)
	* [Sets](#s)
	* [Dictionary](#d)



<a id="p"></a>

# Python
Interpret means can directly running using shell(no compilation and linking).  

```python
>>> u = 'df'
>>> u
'df'
>>> _
'df'
>>> h = 3
>>> _
'df'
>>> h
3
>>> _
3
>>> u
'df'
>>> _
'df'
>>> _ = h
>>> _
3
```

<a id="sadt"></a>

>>> z = "a"
>>> j = "b"
>>> z+j
'ab'
>>> print("hello", ",", "World")
Hello , Word
```
(when concatinate python will **automatically put space in-between).   
to use other seperator:

```python
>>> print("hello,", ", ", "World", sep="")
'hello, World'
```

Inside string, **Delimiter escaping using `\`.**, i.e. can use `\` to treat the following symbol as normal char.  
e.g. `'kat don\'t like dun'`. 



**produce reversing string**    

<a id="is"></a>


<a id="wl"></a>

[Return to Content Table](#ct)

<a id="ds"></a>

Four main collection data types:

* List (*ordered, mutable, allows duplicate*)
* Tuples
* Sets
* Dictionaries

<a id="l"></a>

## List
Using `for` loop in list:

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
[1.0, 2.0, 3.0, 4.0]	# divide '\' always return float, can do '\\'
```

`.sorted()` return a list, can do `sorted(list)[index]`. 

some methods:  

[Return to Content Table](#ct)

<a id="s"></a>

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

[Return to Content Table](#ct)

<a id="d"></a>

## Dictionary
Similar to a list, being indexed using type rather than number. Has no order, every time run will have different order.   
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

`.key()` loop all keys in the dictionary. 
 
 
```python
fruits = {'banana': 10, 'apple': 5}
for fruit in fruits.keys():
    ...
    x += fruits[fruit] # dictionary[key] = the value
```
to access both key and value in `for` loop, do:

```python
for fruit,value in fruits.items():
    ...
```
[Return to Content Table](#ct)