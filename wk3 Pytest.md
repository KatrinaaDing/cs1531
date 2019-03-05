# Pytest

To install:

```
@in-terminal: pip3 install pytest
```
To check if it's installed:

```python
@in-terminal: python3
>>> import pytest
>>>        # no error occurs means it's installed correctly
```

To run pytest:

```
@in-terminal: python3 -m pytest test_example.py # name of the test file
```

## Writing Pytest
Firstly, import the file that we want to test and the function inside the file,  
i.e.

```python
from file_want_to_test import func_want_to_test
```
Each function runs as a **separate test**, and it will indicate which passed and which failed.

To write test, simply use `assert()`.

```python
from file_want_to_test import func_want_to_test

def test_simple():
	ans = func_want_to_test(arg1, arg2)
	assert(ans == 5)
```

When there is complex data structure like `class` in the file we want to test, use **setup_method()** to avoid initialise the data structure for each test.

example (to test classes):

```python
from library import Libaray, Staff, Book	# those three are the names of the classes

class TestLibrary():	# create class inside test file
	def setup_method(self):   # initialise instances so don't need to initialis every time running the test
		book1 = Book(...)
		book2 = Book(...)
		...
		books = [book1, book2....]
		
		staff1  = Staff(...)
		...
		my_staff = [staff1, ...]
		
		self.my_library = Library(my_staff, books)
		
	def test_find_book(self):  # this is inside the class
		result = self.my_library.find_book("aaa") # reutrn a book
		assert(result.get_title() == "aaa") # the function comes from Book

```
