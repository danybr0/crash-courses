# Python crash course

## Methods:

int() -> converts a string into an integer \n
str() -> converts an integer into a string \n
type() -> to see what kind of data type is it
upper() -> CAPS ex. my_name.upper()
lower() -> lower ex. my_name.lower()
len() -> length of a string

## Types of variables:

*	List
X = [1, 2, 3]
You can loop through a list with different loops as for, while and do while.

*	Tuple – static list
X = (1, 2,)
Once a tuple is defined you cannot update the values. Basically you cannot change the values after the tuple is defined.
To get both a tuple and a list value you refer to the indexes: ex. x[0]

* Dictionaries / dict – objects
These are key value objects.
X = {“first_name”: “Jorge”, “last_name”: “Escobar”}
To get the value of Jorge’s first name: x[“first”]
You can also do a list of dictionaries. That is something you do a lot when interacting with databases.
Ex.
x = {“first_name”: “Jorge”, “last_name”: “Escobar”}
y = {“first_name”: “Paul”, “last_name”: “Graham”}
cmd: users = [x, y]
cmd: print(users)

## Functions
first of all you need to import datetime (it is a collection of date and time functions and utilities)
import means loading to memory this specific module
