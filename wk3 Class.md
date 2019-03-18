
# Content Table

* [Class](#Class)
	* [Encapsulation](#Encapsulation)
	* [Abstraction and Inheritance](#Abstraction-and-Inheritance)
	* [Print a Class Instance](#Print-a-Class-Instance)
	* [Association Relationship in OOP](#Association-Relationship-in-OOP)

[Return to README.md](https://github.com/KatrinaaDing/cs1531/blob/master/README.md)


# Class
```python
class Person:	# the name of the class, starting with capital letter
	def __init__(self, firstname, lastname):	# constructor, a special method, declare variables inside
		self.first_name = firstname				# is called when create an instance of the class
		self.last_name = lastname				# can be called by using the class's name followed by a bracket
		self.dob = datetime.now()
	
	def walk(self, distance):					# a method
		print(self.first_name, "is walking", distance, "meters")
			
	def calculate_age(self):
		age = (datetime.now() - self.dob) // timedelta(days=365) # '//' to compute int
		return age
			
person1 = Person("John", "Smith")		# calling the class using constructor
person2 = Person("Isaac", "Carr") 

person1.walk(50)		# calling walk method, can only pass in "distance" as person has "self"=="John"
						# equals to person1.walk("John",50)		
age = person2.calculate_age()
```
`__init__()` can also be:

```python
def __init__(firstname, lastname):
	this.first_name = firstname
	this.last_name = lastname
```

[**Reason using double underscore**](http://igorsobreira.com/2010/09/16/difference-between-one-underline-and-two-underlines-in-python.html)

[Content Table](#Content-Table)

## Encapsulation
**encapsulation**, an act that hiding the internal representation or the state of an object from the outside. Like credit card must keep private.  
`print(person1.first_name)` is accessing the attribute for specific instance, breaking encapsulation.  
Put underscore before the attribute to indicate it's private. e.g. `self._first_name = firstname`  

### getter & setter
To expose the private attribute, use **getter** and **setter**. 

getter:

```python
def get_first_name(self):
	return self._first_name
```

setter:

```python
def set_first_name(self, new_name):
self._first_name = new_name
```

Calling getter and setter:

```python
print(person1.get_first_name())		# to get person1's first name
person1.set_first_name("Jon")		# to set person1's new first name (self parameter is passed in by person1)
```

Getter and setter can change the way (i.e. put restriction) that people extract/change the value from the instance.  
example:

```python
def withdraw(self, amount):		# put restriction on withdrawing money
	if amount > self._balance or amount > 2000L
		print("error: can't withdraw, not enough balance.")
```

Using python properties, getter and setter can have same method name, but basically they are different method.  
e.g.

```python
@property					# a getter in python properties syntax
def my_attribute(self):		# the @ symbol is to specify that my attribute is a python property
	print("Calling getter")
	return self._my_attribute
	
@my_attribute.setter		# a setter 
def my_attribute(self, new_attr):
	print("Calling setter")
	self._my_attribute = new_attr

x = Test(5)		# initialise an instance
print(x.my_attribute)	# => Calling getter => 5
x.my_attribute = 10		# => Calling setter
print(x.my_attribute)	# => Calling getter => 10
```
[Content Table](#Content-Table)

## Abstraction and Inheritance
**parent/super class:** have common behavior/attribute.  
**child/sub class:** can overwrite the behavior of parent class.   
**abstract:** an empty method (templet) inside parent class, allowing child classs to implement theirselves. This kind of method is **abstract method**, and the class containing abstract method is **abstract class**.

example:

```python
class Shape:				# an parent + abstract class
	def __init__(self, color):
		self._color = color
	
	def get_area(self):		# an abstract method
		pass
		
	...
	
class Rectangle(Shape):		# Rectangle is subclass of Shape
	def __init__(self, color, width, height):
		self._color = color
		self._width = width
		self._height = height
	
	def get_area(self):		# implement the abstract
		return self._width * self._height
	
	...

class Circle(Shape):
	def __init__(self, color, radius):
		self._color = color
		self._radius = radius
	
	def get_area(self):		# implement t he abstract
		return 3.142 * self._radius  * self._radius
	
	...
```

Abstract class cannot be instantiated.  
Must use subclass to create new instance.  
e.g.

```python
someShape = Shape("red")	# invalid
rectangle1 = Rectangle("red", 10, 20)	# valid
circle1 = Circle("blue", 15)	# valid
```

Computer doesn't know `Shape` is an abstract class, so in the file contain `Shape`, must from `abc` (the abstract library), import `ABC` (the name of the base class for all abstract classes) and `abstractmethod` (the decorator apply to any abstract method).  

example:

```python
from abc import ABC, abstractmethod

class Shape(ABC):		# bracket shows where does it "belong" to 
	def _init_(...):
		...
		
	@abstractmethod		# the decorator
	def get_area(...):
		...
		
	@abstractmethod
	def get_perimeter(...):
		...
	
	...
```

In child class, to call constructor(or method) from parent class, use `super().constructorName(attribute)`.  
e.g.

```python
def __init__(self, colour, radius) {
	super().__init__(colour)  # This use super's __init__ to initiate variable locally
	self.radius = radius
}
```

**Why using `@abstractmethod`?**  
If don't use `@abstractmethod`, when developer forget to overwite the method in child class, python will automatically implement parent's method (and basically do nothing). If implement `@abstractmethod` in parent class, forgeting to overwrite the method will give an error.

[Content Table](#Content-Table)

## Print a Class Instance
Python can auto convert num to string for `print()`, but for class it doesn't know how to do, hence it will print the pointer by default.

So wee need another method to print class in string.  
example:


```python
def __str__(self):
	return self._first_name + " " + self._last_name
```

[Content Table](#Content-Table)

## Association Relationship in OOP
> I assume you know about UML diagrams


**Association:** there is a "has a"/"contains" relation between class A and class B.

In **UML digram**, the little box points to the container.  
e.g. `Cars ◇- Engine`, `Book ◆- *Page`.  

**Composition** is that "class B" cannot exist dependently. e.g. `Book ◆- *Page`, `Page` will be destoryed if `book` is destroyed. [seems like `Page` is just a pointer contained by `Book`]  

```python
class Car:
	def __init__(self, engine, make):
		self._engine = engine
		self._make = make
		
	def drive(self):
		print("Is driving" + self._make)

class Engine:
	def __init(self):
		pass
		
if __name__ == "__main__":
	my_engine = Engine()
	#my_car = Car(my_engine, "bmw")
	#my_car.drive()
	
	# delete above two lines (destroy my_car) won't destroy my_engine
```
**Aggregation/Association** is that "class B" can exist dependently. e.g. `Cars ◇- Engine`.  

```python
class Book:
	def __init__(self):		# book is a list of pages
		self._pages = [Page("page1"), Page("page2"), Page("page3")]	
	
	def read_book(self):
		for page in self._pages:
			print(page)

class Page:
	def __init__(self, page_text):
		self._page_text = page_text

if __name__ == "__main__":
	#my_book = Book()
	#my_book.read_book()
	
	# destroy my_book will also destory those pages
```
[Content Table](#Content-Table)


