<a id="ct"></a>

# Content Table

* [File Input and Output (I/O)](#fial)
* [CSV File](#cf)
* [Pickle](#p)

<a id="fiao"></a>

# File Input and Output (I/O)

`open("filename", FLAG)` returns `file_object`.
File object is a way we can interact with the file.  
e.g.  
`file_object.read()`  
`file_object.write(str)`  
`file_object.close()`  

Very similar to C.

```python
>>> fp = open("examplefile.txt", "r") # only readable
>>> fp.read()
''	# so far nothing inside
>>> fp.write("Hello")
ERROR	# since the file is only readable

>>> fp = open("examplefile.txt", "w") # write mode
>>> fp.write("Hello")
5	# return bytes that successfully written
>>> fp.write("new string")	# this will overwrite original file
10
>>> fp = open("examplefile.txt", "a") # append mode
>>> fp.write("some more text") # this will concatenate new string at the end of the file.
14 
```

For files that have multiple lines, can do:

```python
>>>fp = open("ex2.txt", "r")
>>>while True:
...		x = fp.readline()   # .readling() allow python to read the file line by line, like fgets() in C
... 	if not x: break     # when (x == None) means it's the end of the file, like (fgets() == NULL) 
... 	print(x)
...
line1

line2

line3

line4

line5

>>> with open("ex2.txt", "r") as f: # easier with for loop
... 	for x in f:  # x is the line, f represents the file (defined above)
... 		print(x)
...
line1
 
line2

line3

line4

line5
```

But those read write function cannot handle complex data type file. We can use **CSV file**.

[Content table](#ct)

<a id="cf"></a>

# CSV File
**CSV file** which stands for comma separated values is a file type that **stores table like data with rows and coloumns**, similar to a spreadsheet.  
example:

```
student_id, first_name, last_name, start_year, degree_length, campus
	  1234,     "John",   "Smith",       2014,             4, "UNSW"
      2345,     "Lucy",	  "Brown",       2014,             2, "UNSW"
      1345,    "Edina",     "Lao",       2015,             3, "USYD"
```

Python has a libary that allow us to read and write CSV file using python API (need to import).

```python
import csv    # import first

f = open("ex_csv.csv", "r")    # then treat it as usual
reader = csv.reader(f) 

for row in reader:
	print(row)
```

* `.reader()` read and return each row as a string, and put each row into a **list**.
* `.DictReader()` put each row into a **dictionary**.

To write CSV file:

```python
import csv

f = open("ex_csv.csv", "a")   # append mode

writer = csv.writer(f)
writer.writerow([1580, "Mary", "Green", 2018, 3, "UTS"])  # pass in a list of new info in order of the table
```

[Content table](#ct)

<a id="p"></a>

# Pickle
Pickle is a python library and it's a way of **serializing** and **deserializing** any python object into a `.pickle` file.  

Unlike `.txt` and `.csv`, `.pickle` not human-readable. It stores data in **binary format** and is able to read it later in python file.

First create a `.pickle` file:

```
@in-terminal: touch myfile.pickle`
```
Then in `.py` we have:

```python
import pickle

class TestClass:    # pickle works with any kind of object
	def __init__(self, foo, bar):
		self._foo = foo
		self._bar = bar
	
	def get_foo(self):
		return self._foo

	def get_bar(self):
		return self._bar

my_obj = TestClass("abc", 5)

f = open("myfile.pickle", "wb")    # "w" = write, "wb" = write in binary
pickle.dump(my_obj, f) # 1st arg: any type of python object. 2nd arg: file objects
```

but after executing the `.py` file and `cat` the `.pickle` file:

```
@in-terminal: python3 test.py
@in-terminal: cat myfile.pickle
**CONFUSING SYMBOLS**
**HERE AND THERE**
**AND ANYWHERE**
```
Those confusing sysmbols is **binary representation** of the data stored in `.pickle`.

If want to read the `.pickle` file, continued from example above, do:

```python
#my_obj = TestClass("abc", 5)

#f = open("myfile.pickle", "wb")
#pickle.dump(my_obj, f)

f = open("myfile.pickle", "rb")    # read in binary mode
pickle.load(f)   # only one parameter: the file object

print(my_obj.get_foo(), my_obj.get_bar()) # then can treat as normal
```

Then excute the `.py` file again:

```
@in-terminal: python3 test.py
abc 5
```

[Content Table](#ct)
