# Content Table
* [Python](#Python)
* [String and Data Type](#String-and-Data-Type)
* [`if` Statement](#\`if\`-Statement)
* [`while` Loop](#`while`-Loop)
* [Data Structure](#Data-Structure)
	* [List](#List)
	* [Sets](#Sets)
	* [Dictionary](#Dictionary)

[Return to README.md](https://github.com/KatrinaaDing/cs1531/blob/master/README.md)


# Python

Python is interpret, dynamically typed language. 
Interpret means can directly running using shell(no compilation and linking).  

don't need files (e.g. .c file)

```python
>>> width = 20
>>> height = 10
>>> width * height
200
>>> print(width * height)
200
```

python can memorize the last value.    

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
[Return to Content Table](#Content-Table)

------

# String and Data Type
```python
>>> a = 9
>>> a = "Hello"
```

can catinate string `print("hello," , ", ", "World") => Hello, World`

```python
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

**{} => placeholder**

```python
>>> print("...is {} and {}.format("a", "b"))
...is a and b
```

**python is strong typed**, which means two type cannot be operated together. `e.g. int cannot + str`, have to convert.

```python
>>> a = 10
>>> b = "10"
>>> a + b
error
>>> a + int(b)
20
>>> str(a) + b
"1010"
```
To find type: `print(type(var))`.   
Inside string, **Delimiter escaping using `\`.**, i.e. can use `\` to treat the following symbol as normal char.  
e.g. `'kat don\'t like dun'`. 


string indexing same as C, **starting from 0**.  
But can do substring as `string[starting : ending (but excluded)]`  

```python
>>> str = "python"
>>> str[0]
'p'
>>> str[0:2]
'py'
>>> str[:2]
'py'
>>> str[3:]
'hon'
```
**can't modify a single char in a defined string**

```python
>>> str = "python"
>>> str[0] = 'j'
error
```

Data comes from console via `input()` **is always str**, better to use `int(input("insert num: ")`  

**produce reversing string**    

```python
word = input('Enter a string: ')
new_word = ""
for i in range(len(word)):
    i = -1-i
    new_word = new_word + word[i]
print(new_word)
```
or  

```python
new_word = word[::-1]
print(new_word)
```
[Return to Content Table](#Content-Table)

--------------------------------

# `if` Statement   

```python
if (condition):
    do somethimg
elif (condition):
    do something
else:
    do something
```

what is **false**:  

- 0
- empty string
- Boolean False  

  
logic operator different from C:  

|C | Python|
|:----:|:-----:|
|&&| and|
| \|\||or|  

[Return to Content Table](#ct)

-----------
<a id="wl"></a>

# `while` Loop  

```python
>>> while (i<n):
...     print(i)
...     i += 1
0
1
2
3
4
5
6
7
8
9
>>> for i in range (1, 10):		# can do range(10)
...      print(i)
0
1
2
3
4
5
6
7
8
9
>>> for i in range (1, 10, -1):
...     print(i)
9
8
7
6
5
4
3
2
1
0
```
[Return to Content Table](#Content-Table)

-------
# Data Structure
Four main collection data types:

* List (*ordered, mutable, allows duplicate*)
* Tuples
* Sets
* Dictionaries

<a id="l"></a>

## List
**list**, can contain different datatype, e.g. `sth = [1, 2, "hello"]`   
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
**.append()** append an item at the end of the list.  
**.pop()** remove the last item from the end of the list.  
**.insert(index, item)** insert item at index(starting from 0)  
`[start : end]` thing can be used for list. 

``` python
odd = [1, 2, 3]
print(odd[1:])
=>[2, 3]
```

[Return to Content Table](#Content-Table)

## Sets
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

[Return to Content Table](#Content-Table)

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
[Return to Content Table](#Content-Table)
