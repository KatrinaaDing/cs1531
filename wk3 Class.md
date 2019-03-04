# Class
```python
class Person:	# the name of the class, starting with capital letter
	def _init_(self, firstname, lastname):		# constructor, a special method
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


## encapsulation
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





