[Interpreted vs Compiled](https://www.youtube.com/watch?v=e4ax90XmUBc)

#PowerShell from Windows


1. **pwd** = _Print Working Directory_
	* Display path of current working directory
2. **ls** = _list_
	* Shows all the files inside the Working Directory (List directory contents)
3. **cd** = _Change Directory_
	* Change directory to <directory>
4. **.** = _Current directory_
	* Represents the current directory when try to change to another. _i.e: cd .\Desktop_
5. **..** = _Parent Directory_ 
	* Goes back one level when changing directory using __..__
6. **cd \*** = _Change Directory straight to C:\*_ 
	* Goes back straight to the root when changing directories
7. **~** = _Autocompletes absolute path_ 
	* i.e.: ~\Desktop = C:\Users\Marcos\Desktop
8. **mkdir** = _Make directory_ 
	* Creates a folder in actual directory. i.e. _mkdir Fotos_
9. **rm** = Remove File 
	* i.e.: _rm mauro.py_
10. **rm -r -fo** = _Remove Directory: -r for **recursive** (to fully empty the folder and subfolders);
	(-fo for **force** to prevent warnings: "just go and delete it")_
	* i.e.:_rm -r -fo Sondeos_

## Creating a file
1. **echo $null FileNameHere.py**
	* Create a file python UTF 8. _$null_ means "don't put anything in this file"
2. **New-Item -ItemType file name.py**
3. **function touch {New-Item -ItemType File -Name ($args[0])}**
	* _touch NewFile.py_

_Additional Note_
>Python Interpreter is a **REPL**: _Reads, Evaluate, Print, Loop_

>**Data Types**: _Boolean(bool), Integers(int), Strings(str), Floats(floats)._

>**Data Structures**: _Dictionary (dict), Lists(list), Tuples, Sets._

>Dynamic Typing: since variables can change types readly. It allows to have variables change types not just values from a 
number to a number or string to string but the actual type of variable.
C++ is statyc-typed lenguaje. An INT always stays as an INT

>**None** represents the idea of _nothingness_. Is the python version of **Null**

```python
		Name = "Daisy"
		Age = 30
		Child = None
```
----

#Python Introduction

##Escape sequences/characters:

http://python-ds.com/python-3-escape-sequences

_Additional Note:_
>+= operator
	str_one = "ice"
	str_one += " cream"
	print(str_one) -> "ice cream"

----

Variable Interpolation - formatting strings (F- strings)

guess = 8
print (f"your guess of {guess} was incorrect!")
notice F at the begining of the sentence and the {} to escape the int

Just for Udemy = "The {} is {}".format(fruit, ripeness)

----

Converting data types 

random = 12.453
integer = int(random) #12 (chopps off the decimals, not round)
string = str(random) # "12.453"
random1 = 12
float = float(random1) # 12.0
round(random,2) = the thing to round, how many decimlas


.replace()
.strip()

----

Conditional Statements

IF some condition is True
	do something
ELIF some other condition is True
	do something
ELSE
	do something

----

Comparison Operators

https://www.tutorialspoint.com/python3/comparison_operators_example.htm

== equals to
!= is not equal to
> <
>= <=

THEY ARE BULEANS - THEY RETURN EITHER TRUE OR FALSE

evaluate for falsy or truthy

bool(value)
Ej.:
bool([])
	# False

----

is vs. ==

== checks if the values are the same and is (Ej. a is b) checks if the values 
	are stored in the same place in memory

a = [1, 2, 3]
b = [1, 2, 3]
a == b			# True (they point to the same values but differet places in memory)
a is b			# False (they are not stored in the same list in memory)
c = b 			
b is c			# True (they are pointing to the same list in memory)

"IS" is only truthy if the variables references the same item in memory
----

Logical Operators

and

or

not

Ej.: not((age >= 2 and age <= 8) or age >= 65)

----

Truthy and falsy

Truthy = Statements or expressions that resolve to a True value

FALSE elements: zero, None, empty strings, empty objects.
The rest are truthy elements 



----

import random

variable = random.randint(from, to)

OR

from random import randint

variable = randint(from, to)

----

.lower()	-> lower case everything the user types in
.upper()	-> upper case everything the user types in

----

		LOOPS

--for--

we want to do something "for every character, or item, or number on a string, list 
	or whatever" That's why the "for"

for item in iterable_object:
	#do something with item

iterable_object = collection of data 
item = is a new variable
	references the current position of our iterator within the iterable.
	It will run through (iterate over) every item of the collection and then 
	go away when it has visited every item

for i in range(1, 8):
	print(i)
1
2
3
4
5
6
7



--ranges--

simple ways of generating inmutable sequences that are ordered in a particular way


range(7)-----------> asume que el inicio es 0
range(1, 8)--------> va de 1 en 1 hasta el numero 8, pero no lo incluye
range(1, 10, 2)----> va de 2 en 2 hasta 10, pero no lo incluye (1, 3, 5, 7, 9)
range(7, 0, -1)----> cuenta regresiva desde 7 hasta 1

r = range(4)
list(r) # [0, 1, 2, 3]

Ej.:

num_of_iteration = input("how many times do I have to tell you? ")

num_of_iteration = int(num_of_iteration)

for num in range(num_of_iteration):
	print("Clean ur room!")



--while--


Ej.: while im_tired:

	#bring me coffee

im_tired ----> boolean variable set to True or False

the while continues to loop while the variable or expression remains Truthy


Ej.: 

user_response = None

While user_response != "please":
	user_response = input("ah ah ah, you didn't say the magic word: ")


in while loop u generally have to pre-create a variable 
while in For loop you can create a temporary one that only exists on the for loop



Ej.:
num = 1

while num < 11:
	print(num)
	num += 2


--break--

gives us the ability to exit out of while loops whenever we want


----

PEP 8 : Popular style guide for python

***PEP* stands for Python Enhancement Proposal.***

autopep8 --in-place filename.py
or 
autopep8 --in-place --aggressive --aggressive filename.py

**Styles:**

1. Do not use more than 79 characters in a line of code.

2. _Quotes_: you can use either single or double quotes to define strings. Please, choose one that you like the most and consistently use it in your code. Avoid backslashes. 


----

--LIST--

Fundamental data structures for ordered information
it's a collection or grouping of items: anything, string, float, booleans, other lists, integers.
a way of combining data into one variable/one structure. 

LIST = data structure. higher level up of data type, that store other data types inside in a structured way
	like a mini data base, but stored in a python variable
	
	list always start counting from 0
elem =	["a", "b", "c", "d", "e"]
index	  0    1    2    3    4
index	 -5   -4   -3   -2   -1

print(elem[0]) = "a"

print(elem[1]) = "b"

other = elem[1]
print(other) = "b"

Ej.: tasks = ["clean", "swipe", "order", "finish up", 1, 56, True]

list built in function

tasks = list(range(1, 4))
print(tasks) # [1, 2, 3]
----

Length of lists

If you want to loop through the list, you need to know how many elements the list has

tasks = ["clean", "swipe", "order", "finish up", 1, 56, True]
len(tasks) #7

----

Check if value is in list

Ej.: tasks = ["clean", "swipe", "order", "finish up", 1, 56, True]

"clean" in tasks #True

"dirty" in tasks #False

----

replace items in a list

Individually

	people = ["arthur", "mauro", "wanda", "pepe"]

	people[3] = "jose"

Access All values -- FOR LOOP --

people = ["arthur", "mauro", "wanda", "pepe"]

for person in people:
	print(person)
	
		or

numbers = [1, 4, 5, 17, 6, 19]

for num in numbers:
	print(num * num)		

Access all values -- WHILE LOOP --

numbers = [1, 4, 5, 17, 6, 19]
index = 0      #-----> i responde al indice de los elementos de la lista

while index < len(numbers):
	print(f"{index}: numbers[index]")
	index += 1

----

IDE

An IDE, or Integrated Development Environment, enables programmers to consolidate the 
	different aspects of writing a computer program.

IDEs increase programmer productivity by combining common activities of writing software into a single application: editing source code, 		building executables, and debugging.

----

functions vs methods 

a method is a type of a function

functions that starts with a dot "." at the end are specific for lists. Therefore, they are called LIST METHOD

.append()	----> adds an item to the end of the list
	Ej.: 
	first_list = [1, 2, 3, 4]
	first_list.append(5)
	print(first_list) # [1, 2, 3, 4, 5]

	or

	first_list.append([5, 6, 7, 8])
	print(first_list) # [1, 2, 3, 4, [5, 6, 7, 8]]	


.extend()	----> add to the end of a list all values passed to extend whereas with .append you can only add 1 item

Ej.: 
	first_list = [1, 2, 3, 4]
	first_list.extend([5, 6, 7, 8])
	print(first_list) # [1, 2, 3, 4, 5, 6, 7, 8]


.insert()	----> inserts an item at a given position using a numeric index

Ej.: 
	first_list = [1, 2, 3, 4]
	first_list.insert(2, "hi!")
	print(first_list) # [1, 2, "hi!", 3, 4]
	first_list.insert(-1, "The End")
	print(first_list) # [1, 2, "hi!", 3, "The End", 4]


----

Remove items from lists


.clear()	----> remove all of the items from the list, at once

Ej.: 
	first_list = [1, 2, 3, 4]
	first_list.clear()
	print(first_list) # []


.pop()	----> removes a single element; have to pass the index that responds to the item u want to remove
				else, it removes the last item in the list.
				In both cases, it returns the removed item in case u want to capture it

Ej.: 
	first_list = [1, 2, 3, 4]
	first_list.pop(1)
	print(first_list) # [1, 3, 4]

capturing popped item:

	last_item = first_list.pop(1)
	print(last_item) = 2	


.remove()	----> we assign the value that we want to remove; not the index but the exact value
					removes the first item from a list whose value is X meaning
						Throws a ValueError if the item is not found
						it doesn't return the removed item in case u want to capture it

Ej.: 
	first_list = ["hi", "hello", "hola", "ciao", "hallo", "ciao"]
	first_list.remove("ciao")
	print(first_list) # ["hi", "hello", "hola", "hallo", "ciao"]



.index()	----> allows to find the position of a given item inside of a list
					allows to specify an start and an end

	first_list = ["hi", "hello", "hola", "ciao", "hallo", "ciao"]
	first_list.index("hello") # 1
		
	allows to specify an start and an end

	first_list = ["hi", "hello", "hola", "hello", "ciao", "hallo", "ciao"]
					0		1		2		3		 4		 5		  6
	first_list.index("hello") # 1
	first_list.index("hello", 2) ---> find the index of "hello" after the index 2 (inclusive)
		#3
	
	first_list = ["hi", "hello", "hola", "hello", "ciao", "hallo", "ciao"]
					0		1		2		3		 4		 5		  6
	first_list.index("hello") # 1
	first_list.index("hello", 2, 5) ---> find the index of "hello" after the index 2 (inclusive) and before 5


.count()	----> accepts 1 input; counts how many times the input occurs in the list

Ej.:	
	
	first_list = ["hi", "hello", "hola", "ciao", "hallo", "ciao"]
	first_list.count("ciao") #2



.reverse()	-----> reverses the order of a list, in place. 

Ej.:	
	
	first_list = [1, 2, 3, 4]
	first_list.reverse() #[4, 3, 2, 1]

	numbers = [1, 2, 3, 4]
	numbers = [::-1] # [4, 3, 2, 1]

.sort()	----> sort the items of the list, in place. 
	
Ej.:	
	
	first_list = [2, 1, 4, 3]
	first_list.sort() # [1, 2, 3, 4]


.join()	----> string method that takes an iterable argument

	Ej.:

	words = ["Coding", "Is", "Fun"]

	' '.join(words) # "Coding Is Fun" ----> the ' ' means there is a space between each word of whatever we fill it with

	'1'.join(words) # "Coding1Is1Fun"


----
	
slicing	----> built in allow to make copies of entire lists or portions of a list
			Ej.: give me from index 5 to 10 from a list

some_list[start:end:step]
		   1st  2nd	interval
		   cut	cut
	INCLUSIVE	EXCLUSIVE
								NOTE: START POINT IS INCLUSIVE
									  END POINT IS EXCLUSIVE

Ej.: 
						
first_list = [1, 2, 3, 4]
first_list[3:]	# [4]			PAY ATTENTION TO THE : <--- That way python understunds it's slicing method

		if you enter a negative number, it will start the slice that many back from the end BUT HACIA ADELANTE (FORWARD)-|

START PARAMETER

Ej.: 																													 |
																														 |	
	first_list = [1, 2, 3, 4]																							 |
	first_list[-1:] # [4]																								 |		
	first_list[-3:] # [2, 3, 4]		<<<==================================================================================|					
		   INDEX ==>  -3 -2 -1
					  =====>>> FORWARD



END PARAMETER

first_list = [1, 2, 3, 4]
first_list[1:3] #[2, 3]

	if you pass a negative number as the end value, it will end the slice at that many elements from the end of the list

Ej.:

first_list = [1, 2, 3, 4]
			 -4 -3 -2 -1

			 end point = -1 index (exclusive)

first_list[:-1] #[1, 2, 3]


STEP PARAMETER
		With negative parameter, instead of going forward, ---> you go backwards <---

Ej.:
			  0  1  2  3  4  5

first_list = [1, 2, 3, 4, 5, 6]

			 -6 -5 -4 -3 -2 -1


first_list[1::2]	#[2, 4, 6]
first_list[::2]		#[1, 3, 5]
first_list[1::-1]	#[2, 1] 
first_list[:1:-1]	#[6, 5, 4, 3]
first_list[2::-1]	#[3, 2, 1]

----


Tricks with Slices

----Reverse list/strings -----> [::-1]  	

		Ej.: string = "This is fun!"
			 string[::-1] # '!nuf si sihT'

----Modifying portions of lists
		
		Ej.:
			numbers = [1, 2, 3, 4, 5]
			numbers[1:3] = ["a"; "b", "c"]
			print(numbers) # [1, 'a', 'b', 'c', 4, 5] 

		Removes 2, 3 and adds a, b, c


----Swapping values

Ej.:
			names = ["James", "Michelle"]
			names[0], names[1] = names[1], names[0]
			#["Michelle", "James"]





---- List Comprehension ---- 

	It's shorthand syntax that allows us to generate new lists that makes new lists that are direct copies
		of other lists or more often than not are tweaked versions where we could take one list and then
			generate a new one that has, i.e., every number squared or every string reversed.

	SYNTAX


	[   ____    for    ____    in    ____   ]

	   what to   	   where 	   from which
	   	  do**		 to save it 	  list
	   				(placeholder)*

	   					*placeholder variable for
	   						each item in that list			 
	   		
	   		**some way of manipulating 
	   			each item of that list

	Sintesis: We take an existing list and output another list with different values 
					based upon the first list 
		 

	Ej.:
		
		nums = [1, 2, 3]
		[x * 10 for x in nums] ----> for every x in nums, multiply by 10
		[10, 20, 30]




----

List comprehension vs. Loops

Ej.: loop instrad list comprehension

	list = [1, 2, 3, 4, 5]
	new_values = []
													FOR LOOP
	for item in list:
		new_list = item * 2
		new_values.append[new_list]

														VS.

list = [1, 2, 3, 4, 5]
													LIST COMPREHENSION
new_values = [x * 2 for x in list]


Ej.:

	string = "Hello"
1.	[char.upper() for char in string]
		# ["H", "E", "L", "L", "O"]


	friends = ["juan", "pedro", "alberto", "pepito"]
2.	[friend[0].upper()+friend[1:] for friend in friends] or [friend.title() for friend in friends]
		# ["Juan", "Pedro", "Alberto", "Pepito"]

3.	[num * 10 for num in range(1,6)]
		# [10, 20, 30, 40, 50]

4.	numbers = [1, 2, 3, 4, 5]
	[str(num) for num in numbers]
		# ['1', '2', '3', '4', '5']
5. 

```py
suit = ["Clubs", "Diamonds", "Hearts", "Spades"]
value = ["A", "2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K"]
new_list = [f"{v} of {s}" for v in value for s in suit]
print(new_list)
# ['A of Clubs', 'A of Diamonds', 'A of Hearts', 'A of Spades', '2 of Clubs', '2 of Diamonds', '2 of Hearts', '2 of Spades', 
# '3 of Clubs', '3 of Diamonds', '3 of Hearts', '3 of Spades', '4 of Clubs', '4 of Diamonds', '4 of Hearts', '4 of Spades', 
# '5 of Clubs', '5 of Diamonds', '5 of Hearts', '5 of Spades', '6 of Clubs', '6 of Diamonds', '6 of Hearts', '6 of Spades', 
# '7 of Clubs', '7 of Diamonds', '7 of Hearts', '7 of Spades', '8 of Clubs', '8 of Diamonds', '8 of Hearts', '8 of Spades', 
# '9 of Clubs', '9 of Diamonds', '9 of Hearts', '9 of Spades', '10 of Clubs', '10 of Diamonds', '10 of Hearts', '10 of Spades', 
# 'J of Clubs', 'J of Diamonds', 'J of Hearts', 'J of Spades', 'Q of Clubs', 'Q of Diamonds', 'Q of Hearts', 'Q of Spades', 
# 'K of Clubs', 'K of Diamonds', 'K of Hearts', 'K of Spades']
```
----

List comprehension with conditional logic

1. 	IF

 	numbers = [1, 2, 3, 4, 5, 6]
	evens = [num for num in numbers if num % 2 = 0]    -----> attention to the SYNTAX
	odds = [num for num in numbers if % 2 != 0]

2. IF + ELSE
	
	numbers = [1, 2, 3, 4, 5, 6]
	[num * 2  if num % 2  == 0 else num / 2 for num in numbers]  ----> ____ if ____ else ____ for ____ in ____
		# [0.5, 4, 1.5, 8, 2.5, 12]

3. IF - in strings
	
	with_vowels = "This is so much fun"

	####Without the .join(), it would be:
		[char for char in with_vowels if char not in "aeiou"]
		["T", "h", "s", " ", "s", " ", "s", " ", "m", "c", "h", " ", "f", "n"]

	''.join(char for char in with_vowels if char not in "aeiou")
		# 'Ths s s mch fn'	


4.  JUST AN EXAMPLE

		names = ["Elie", "Tim", "Matt"]
		answer = [name[0] for name in names]

		numbers = [1, 2, 3, 4, 5, 6]
		answer2 = [num for num in numbers if num % 2 == 0]

				OR

		answer = [person[0] for person in ["Elie", "Tim", "Matt"]]
		answer2 = [val for val in [1,2,3,4,5,6] if val % 2 == 0]


----

Nested Lists or Multi-dimensional Lists

		Useful for matrices, data structures, game boards, visualizacion de filas y columnas, etc.
	
	Ej.:
		
		nested_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
			or
		nested_list = [["a", "b", "c"], ["d", "e", "f"], ["g", "h", "i"]]
		
		len(nested_list) # 3


----

Access to neste lists		

						 -3				  -2               -1
                    -3   -2   -1     -3   -2   -1     -3   -2   -1	
1.	nested_list = [["a", "b", "c"], ["d", "e", "f"], ["g", "h", "i"]]
	                 0    1    2      0    1    2      0    1    2   
	                 	  0				   1				2


	nested_list[0][1] #"e"
	nested_list[-1][-1] #"i"

----

Printing values in nested lists 

		
		Ej.:
	
1.			nested_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
			
			for l in nested_list:
				for val in l:
					print(val)
			# 1	
			# 2
			# 3
			# 4
			# 5
			# 6
			# 7
			# 8
			# 9

----

Nested list Comprehension

Ej.:
						   l          l          l 
 1.		nested_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
					   valvalval  valvalval  valvalval

		[[print(val) for val in l] for l in nested_list]      <<<<================== ATTENTION
													Interpretación == por cada l en la nested_list, printear
																	cada valor existente en  cada l





2.		board = [[num for num in range(1, 4)] for val in range(1, 4)]
		print(board) # [[1, 2, 3], [1, 2, 3], [1, 2, 3]]



3. IF + ELSE 

		[["X" if num % 2 != 0 else "O" for num in range(1, 4)] for val in range(1, 4)]
			#[['X', 'O', 'X'], ['X', 'O', 'X'], ['X', 'O', 'X']]



## Limitations of lists
They work to store a particular type or set of data where things make sense. Ej.:	_list of users
																					list of names_
list = [True, 1, "hola,", ["a", 3, 4]]  ----> this doesn't really mean or help much; we don't know what it refers to




#Dictionaries
A data structure that consists of key value pairs 
We use keys to describe our data and the values to represent the data
In a list, a the key would be the index of the value. In dictionaries, you control de key and the value. 
_There is no specific ordered guaranteed_, unlike a list where you know we have at index "n" order "x" item.


##Creating a dictionary

Ej.:
```python	
instructor = {
	"name": "Colt",
	"owns_dog": "True",
	"num_courses": 4,
	"favorite_language": "Python",
	"is_hilarious": False,
	44: "My favorite number!"
}
```
or

use **dict** function 

Ej.:
	
	another_dictionary = dict(key = "value")
	another_dictionary # {'key': 'value'}

	Ej.:
		new_dictionary = dict(name = "juan", edad = 34, genero = "Masculino")
		new_dictionary # {'name': 'juan', 'edad': 34, 'genero': 'Masculino'}


##Accessing to a dictionary
###Individual Values	


	instructor = {
		"name": "Colt",
		"owns_dog": "True",
		"num_courses": 4,
		"favorite_language": "Python",
		"is_hilarious": False,
		44: "My favorite number!"
	}

	instructor["name"] # 'Colt'
	instructor["thing"] # KeyError

###All the values
**.values()** ----> prints the values, not the keys
	
	instructor = {
		"name": "Colt",
		"owns_dog": "True",
		"num_courses": 4,
		"favorite_language": "Python",
		"is_hilarious": False,
		44: "My favorite number!"
	}

	for val in instructor.values():
		print(val)
		# Colt
		# True
		# 4
		# Python
		# False
		# My favorite number!

##All the keys

**.keys()**_ ----> prints the keys, not the values
	
	instructor = {
		"name": "Colt",
		"owns_dog": "True",
		"num_courses": 4,
		"favorite_language": "Python",
		"is_hilarious": False,
		44: "My favorite number!"
	}
		

	for key in instructor.keys():
		print(key)
		# name
		# owns_dog
		# num_courses
		# favorite_language
		# is_hilarious
		# 44

##Access both: keys and values

**.items()**

	instructor = {
		"name": "Colt",
		"owns_dog": "True",
		"num_courses": 4,
		"favorite_language": "Python",
		"is_hilarious": False,
		44: "My favorite number!"
	}
		

	for key, value in instructor.items():          ================>>>> SYNTAX ATTENION!!! FOR KEY, VALUE IN ________:
		# print(key, value)
		# name Colt
		# owns_dog True
		# num_courses 4
		# favorite_language Python
		# is_hilarious False
		# 44 My favorite number!

##Test for existance of a key or value

###Keys
	"name" in instructor # True   or    "name" in instructor.key() # True
	"address" in instructor # False
###Values
	"Colt" in instructor.value() # True
	"74" in instructor.value() # False

##Dictionary Methods

**.clear()** 

		Clears all the keys and values in a dictionary

		d = dict(a=1, b=2, c=3)
		d.clear()
		d # {}

**.copy()**
		
		d = dict(a=1, b=2, c=3)
		c = d.copy()
		c # {'a': 1, 'b': 2, 'c': 3}
		c is d = False

**.fromkeys()** 
		Usually it's used to create default dictionaries to assign initial values to properties (keys) 
		Creates key-value pairs from comma separated values (.CSV)
		Call it from an empty dictionary --> {}. or dict.
		What we do is we pass in an iterable collection (otherwise, if its a string it will separate every character and return an iterable collection: 'phone': 'p','h','o','n','e' ) and then a value (Ej.: {}.fromkeys(['email'], 'unknown')
		creates a new dictionary from the given sequence of elements with a value provided by the user.
		dictionary.fromkeys(sequence[, value])
		If we had a bunch of keys that we are trying to set to a default value ej.: "None"

		Ej.: new_user = {}.fromkeys(['name', 'score', 'email', 'gender'], None)
			 		# {'name': None, 'score': None, 'email': None, 'gender': None}

	Ej.:
		keys = {'a', 'e', 'i', 'o', 'u' }
		vowels = dict.fromkeys(keys)
		print(vowels) 
		# {'a': None, 'u': None, 'o': None, 'e': None, 'i': None} 

		{}.fromkeys("a", "b") # {'a', 'b'}
		{}.fromkeys(['email'], 'unknown') # {'email': 'unknown'}

**.get()**
		Retrieves a key in an object and return None instead of a KeyError if the key doesn't exist
		It's a useful method to test for the existance of a value  

	Ej.: 
		d = dict(a=1, b=2, c=3)
		d.['a'] #1
		d.get['a'] #1	

		d.['e'] #KeyError
		d.get['e'] #None

**.pop()**
		Takes a single value corresponding to a key and removes that key-value pair from the dictionary. 
		Returns the value corresponding to the key that was removed. 

	Ej.: 
		d = dict(a=1, b=2, c=3)
		d.pop('a') #1
		d #	{'b':'2', 'c':'3'}
		d.pop('e') #KeyError

**.popitem()**
		Removes a random item


**.update()**
		Update keys and values in a dictionary with another set of key value pairs.
		The update() method updates the dictionary with the elements from the another dictionary object or from an iterable of key/value pairs.
		The update() method adds element(s) to the dictionary if the key is not in the dictionary. If the key is in the dictionary, it updates the key with the new value

		SYNTAX = dict.update([other])

		d = {1: "one", 2: "three"}
		d1 = {2: "two"}

	
		d.update(d1)						# updates the value of key 2
		# {1: 'one', 2: 'two'}

		d1 = {3: "three"}

		d.update(d1)						# adds element with key 3
		# {1: 'one', 2: 'two', 3: 'three'}


##Dictionary Comprehension
	
	By default it will iterate over Keys.
	To iterate over keys and values u can use .items()
	

						SYNTAX


	{   ____  :  ____  for    ____    in    ____   }

	
	numbers = dict(first=1, second=2, third=3)

1.	squared_numbers = {key: value ** 2 for key in numbers.items()}
		#{'first' : 1, 'second': 4, 'third': '9'}


2.	{num: num ** 2 for num in [1,2,3,4,5]}
	{1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

 	
3.	str1 = "ABC"
	str2 = "123"
	{str1[i]: str2[i] for i in range(0, len(str1))}
	#{'A': '1', 'B': '2','C': '3'}

4. 	CONDITIONAL LOGIC 									{ ____  :  ____ if ____  else  ____  for  ____  in  ____ }
	num_list = [1, 2, 3, 4, 5]

	{num:("even" if num % 2 == 0 else "odd") for num in num_list}



#Tuples

Tuples is an ordered collection of items.
A tuple in Python is similar to a list. The difference between the two is that **we cannot change the elements of a tuple once it is assigned** whereas, in a list, elements can be changed.
_**Tuples are inmutable**_ ---> They can never change
A tuple can have any number of items and they may be of different types 
	
	SYNTAX

	numbers = (1, 2, 3, 4)
	3 in numbers #True 												#inmutable
	numbers[3] = "Change me!" #TypeError: 'tuple' object does not support item assignment


Why to use a tuple?
1. Tuples are faster than lists (lighter weight)
2. Can make ur code safer from bugs and that kind of stuff
3. They are useful as validkeys in a dictionary
	
	locations = {
		(35.5925, 39.3834): "Tokyo Office",
		(45.2257, 39.8834): "New York Office"
		(40.5123, 39.8637): "San Francisco Office"
	}


4. Some methods return tuples. Ej.: .items() when working with dictionaries.
	
	instructor = {
		"name": "Colt",
		"owns_dog": "True",
		"num_courses": 4,
		"favorite_language": "Python",
		"is_hilarious": False,
		44: "My favorite number!"
	}
	print(instructor.items())

	# dict_items([('name', 'Colt'), ('owns_dog', 'True'), ('num_courses', 4), ('favorite_language', 'Python'), ('is_hilarious', False), (44, 'My favorite number!')])

##Creating a tuple

Ej.:
	
	alphabet = ('a', 'b', 'c', 'd')

or

use **tuple** function

	 numbers = [1, 2, 3, 4]
	 tuple = tuple(numbers)

##Accessing tuple
	
	tuple = (1, 2, 3, 4, 5)
	tuple[0] #1


##Iterating over tuple

1. FOR
		alphabet = ('a', 'b', 'c', 'd')
		for elements in alphabet:
			print(elements)
		#a
		#b
		#c
		#d

2. WHILE

months = ('Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio', 'Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre')
i = len(months) - 1

while i >= 0:
	print(months[i])
	i -= 1

	#Diciembre
	#Noviembre
	#Octubre
	#Septiembre
	#Agosto
	#Julio
	#Junio
	#Mayo
	#Abril
	#Marzo
	#Febrero
	#Enero

##Tuples Methods

**.count()**
		Returns the number of times a value appears in a tuple

	Ej.: 
		alphabet = ('a', 'b', 'c', 'd')
		alphabet.count('a')
		# 1

**.index()**
		Returns de index at which a value is found in a tuple

	Ej.: 
		alphabet = ('a', 'b', 'c', 'd')
		alphabet.index('a')
		# 0

##You can use slices as well for tuples

#Sets
No duplicate values and no order. 
A set is an unordered collection of items. Every element is unique (no duplicates) and must be immutable (which cannot be changed).
However, the set itself is mutable. We can add or remove items from it.
Sets can be used to perform mathematical set operations like union, intersection, symmetric difference etc.

_They are useful if you need to keep track of a collection of elements but don't care about ordering keys or values or duplicates_

SYNTAX

A set is created by placing all the items (elements) inside curly braces {}, separated by comma or by using the built-in function set().
It can have any number of items and they may be of different types (integer, float, tuple, string etc.). But a set cannot have a mutable element, like list, set or dictionary, as its element.

my_set = {1, 2, 3}

##Create a Set
Empty curly braces {} will make an empty dictionary in Python. 
To make a set without any elements we use the **set()** function without any argument.

	Ej.:
		a = {}
		# check data type of a
		# Output: <class 'dict'>
		print(type(a))

		# initialize a with set()
		a = set()

		or


		my_set = {1, 2, 3}


##Acces to sets
Can't do it by index (because there is no order).

**Test if an element is in the set**

	Ej.:
		my_set = {1, 2, 3, 'a', 'b'}
		1 in my_set #True

###Accessing all values
	
	my_set = {1, 2, 3, 'a', 'b'}
	for elem in my_set:
		print(elem)

##Common use for set
**If you turn a list with duplicates into a set, _it will eliminate duplicates and keep the unique elements_**


##Set methods

**.add()**
We can add single element using the add() method and multiple elements using the update() method. The update() method can take tuples, lists, strings or other sets as its argument.
	
	Ej.:
		my_set = {1, 2, 3, 'a', 'b'}
		my_set.add('c')
		# my_set = {1, 2, 3, 'a', 'b', 'c'}


**.update()**



A particular item can be removed from set using methods, discard() and remove().

The only difference between the two is that, while using discard() if the item does not exist in the set, it remains unchanged. But remove() will raise an error in such condition.

**.discard()**

**.remove()**

	Ej.:
		my_set = {1, 2, 3, 'a', 'b'}
		my_set.remove('b')
		# my_set = {1, 2, 3, 'a'}

**.copy()**
		
	Ej.:
		my_set = {1, 2, 3, 'a'}
		another_set = my_set.copy()
		# another_set = {1, 2, 3, 'a'}

**.clear()**


	Ej.:
		my_set = {1, 2, 3, 'a', 'b'}
		my_set.clear()
		# my_set = {}

##Set Math
1. **intersection**

Intersection of A and B is a set of elements that are common in both sets. Intersection is performed using **&** operator. Same can be accomplished using the method intersection().

	A = {1, 2, 3, 4, 5}
	B = {4, 5, 6, 7, 8}

	A & B

	# use & operator
	
	print(A & B)

	# {4, 5}

2. **symmetric_difference**
3. **union**

The Python set union() method returns a new set with distinct elements from all the sets. Combine, i.e, too sets excluding duplicate items.

	Syntax = A | B

	Ej.:
		A = {1, 2}
		B = {2, 3, 4}
		C = {5}

		Then,
		A|B = B|A = {1, 2, 3, 4}
		A|C = C|A = {1, 2, 5}
		B|C = C|B = {2, 3, 4, 5}

		A|B|C = {1, 2, 3, 4, 5}


##Set Comprehension

	{ ____ for ____ in ____ }

1.	{x ** 2 for x in range(0, 10)}

	# {0, 1, 64, 4, 36, 9, 16, 49, 81, 25} 		----> no order as u see

2. 	string = "hello"
	
	{char for char in string if char in "aeiou") 
	
	#{'e', 'o'}


	len({char for char in string if char in "aeiou"}) == 5   ----> entonces tiene todas las vocales (#True)



#														F U N C T I O N S

**In Python, function is a group of related statements that perform a specific task.** It's a process for executing a

Functions help break our program into smaller and modular chunks. As our program grows larger and larger, functions make it more organized and manageable.

Furthermore, it avoids repetition and makes code reusable.

##	Why to use functions?

1. Code stay DRY (clean) - **DONT REPEAT YOURSELF** != WET -> Write Everything Twice
	Helps clean up code and prevent code duplication
2. Helps _Abstract away_ code for other users.
	Imagine you had to rewrite the "print()" function for every program you wrote.
3. Allows organize the code, logically. 

##	SYNTAX 
	
		def function_name(parameters):
		"""docstring"""
		statement(s)

Above shown is a function definition which consists of following components.

1. Keyword **def** marks the start of function header.
2. A _function name_ to uniquely identify it. Function naming follows the same rules of writing identifiers in Python (snake case).
3. **Parameters** (arguments) through which we pass values to a function. They are optional.
4. A **colon** (:) to mark the end of function header.
5. Optional _documentation string **(docstring)**_ to describe what the function does.
6. **One or more valid python statements that make up the function body.** Statements must have same indentation level (usually 4 spaces).
7. An **optional return** statement to return a value from the function.

	Ej.: 
	def greet(name):
	"""This function greets to
	the person passed in as
	parameter"""
	print("Hello, " + name + ". Good morning!")

						OR

	def sing_happy_birthday(name):
		print("Happy Birthday to you")
		print("Happy Birthday to you")
		print(f"Happy Birthday dear {name}")
		print("Happy Birthday to you")

##The Return Statement
*The return statement is used to exit a function and go back to the place from where it was called.*

1. Exits the function (if you print sthing after the return, it won't print)
2. Outputs whatever value is placed after the return keyward
3. Pops the function off of the call stack

Syntax of return

**return [expression_list]**

This statement can contain expression which gets evaluated and the value is returned. If there is no expression in the statement or the return statement itself is not present inside a function, then the function will return the None object.

For example(s):

1. Not using **return**

```python	
	print(greet("May"))
	Hello, May. Good morning!
	None	
	Here, None is the returned value.
```

2. using **return**

Ej.:
```python
from random import random
from random import randint

def flip_a_coin():
	#generate random between 0-1
	if random() > 0.5:
		return "Cara"
	else:
		return "Seca"
	return

print(flip_a_coin())
```

3. using **1 input as a parameter/argument**

```python
def square(num):
	return num**num
print(square(3))
# 27
```

4. using ***2* parameter/argument**


```python
def multiply(a,b):
	return a*b
print(add(3,4))
# 12
```

## Parameters vs. Arguments

1. **Parameter** = is a variable in a method definition. Is a variable in the declaration of function.
	Ej.:
```python
def multiply(a,b):
	return a*b
```
2. **Arguments** = when a method is called, the arguments are the data you pass _into the method's parameters_. Is the actual value that is passed to the function
	Ej.:
```python
print(add(3,4))
```

##Default parameters - If no argument passed in

What can default parameters be?
1. Functions
2. Lists
3. Dictionaries
4. Strings
5. Booleans
6. Integers/Floats

In this case (below), if there is no argument passed on parameter **b**, then the default value is going to be 2

```python
def multiply(a,b=0):
	return a*b
print(multiply(3))
# 0
```

###Other functions as Default Parameters

```python
def add(a,b):
	return a+b

def subtract(a,b):
	return a-b

def math_operation(a,b, fn=add):
	return fn(a,b)



```


### Keyword Arguments

They allow us to specify **if we know the name of the parameters**

**It's useful when passing a dictionary to a function and unpacking it's value**

```python
def full_name(first, last):
	return f"Your name is {first} {last}"

full_name(first = 'Mauro', last = 'Consolani')

					OR

full_name(last = 'Consolani', first = 'Mauro')						
```

Always the return will be: 
```python
'Your name is Mauro Consolani'
```
**Because I specified which argument responds to each parameter**

##Scope of functions (alcance)

Scope of a variable is the portion of a program where the variable is recognized. Parameters and variables defined inside a function is not visible from outside. Hence, they have a __local scope__. Otherwise, they are __global scope__
_Variables created in functions are scoped in that function_ meaning that they are only available in that function
1. Local Variable = can only be used and invoked inside the function
2. Global Variable = they exist on the global scope; can't be used inside a function if it already exists outside; must be defined inside the function again.


```python
def my_func():							
	x = 10												# x = LOCAL SCOPE
	print("Value inside function:",x)

x = 20
my_func()												# x = GLOBAL SCOPE
print("Value outside function:",x)

Value inside function: 10
Value outside function: 20
```


## Use a global variable in a function

**global**
Allows to use a global variable in a local scope

```python
total = 0 

def increment():
	global total # <------------------------- bring a global variable into a local scope
	total += 1
	return total

increment() # 1

```

**nonlocal**
Lets us modify a parent's variable in a child (aka nested) function

```python
def outer():
	count = 0
	def inner():
		nonlocal count # <----------- means is not global, it's a local variable in the parent function
		count += 1 
		return count
	return inner()
```

##Documenting Functions

Using triple cuotes: """ """

Essential when writing complex functions

```python
def say_hello():
	"""a simple function that returns the string 'hello' """
	return 'hello'

say_hello.__doc__ #'a simple function that returns the string 'hello'' 
```

#Introduction to \*args and **\*\*kwargs in Python**

In Python, we can pass a variable "number of arguments" to a function using special symbols. There are two special symbols:

\*args (Non Keyword Arguments)
\*\*kwargs (Keyword Arguments)

We use \*args and \*\*kwargs as an argument when we are unsure about the number of arguments to pass in the functions.

##\*args

It will gather all the remaining arguments as a *tuple*. \*args is just a parameter, you can name it as you want. 
If we put \*args as a parameter, it will collect any number of additional or extra arguments that have been passed in into a single parameters called \*args or whatever we name it

If we are not sure about the number of arguments that can be passed to a function, Python has \*args which allow us to pass the variable number of non keyword arguments to function. In the function, we should use an asterisk \* before the parameter name to pass variable length arguments.The arguments are passed as a tuple and these passed arguments make tuple inside the function with same name as the parameter excluding asterisk \*.

Ej.:

```python
def sum_all_values(*args):
    total = 0
    for val in args:
        total += val

    return total

sum_all_values(1, 2, 3) # 6

sum_all_values(1, 2, 3, 4, 5) # 15
```

Ej.:
```python
def ensure_correct_info(*args):
    if "Colt" in args and "Steele" in args:
        return "Welcome back Colt!"

    return "Not sure who you are..."

ensure_correct_info() # Not sure who you are...

ensure_correct_info(1, True, "Steele", "Colt")
```


##\*\*kwargs
It's another special operator that we can add as a parameter into functions rather than collecting any addiontal argument what it would do is gather remaining keyword arguments and rather than storing it in a tuple it stores them in a dictionary

Ej.:
```python
def fav_colors(**kwargs):
	for person, color in kwargs.items():
		print(f"{person}'s favorite color is {color}")

fav_colors(colt="purple", ruby="red", ethel="teal")
fav_colors(colt="purple", ruby="red", ethel="teal", ted="blue")
fav_colors(colt="royal deep amazing purple")
```

Ej.:
```python
def special_greeting(**kwargs):
    if "Colt" in kwargs and kwargs["Colt"] == "special":
        return "You get a special greeting Colt!"
    elif "Colt" in kwargs:
        return f"{kwargs["Colt"]} Colt!"

    return "Not sure who this is..."

special_greeting(Colt='Hello') # Hello Colt!
special_greeting(Bob='hello') # Not sure who this is...
special_greeting(Colt='special') # You get a special greeting Colt!
```

Python passes variable length non keyword argument to function using \*args but we cannot use this to pass keyword argument. For this problem Python has got a solution called \*\*kwargs, it allows us to pass the variable length of keyword arguments to the function.
In the function, we use the double asterisk \*\* before the parameter name to denote this type of argument. The arguments are passed as a dictionary and these arguments make a dictionary inside function with name same as the parameter excluding double asterisk \*\*.

```python
def intro(**data):
    print("\nData type of argument:",type(data))

    for key, value in data.items():
        print("{} is {}".format(key,value))

intro(Firstname="John", Lastname="Wood", Email="johnwood@nomail.com", Country="Wakanda", Age=25, Phone=9876543210)

Data type of argument: <class 'dict'>
Firstname is John
Lastname is Wood
Email is johnwood@nomail.com
Country is Wakanda
Age is 25
Phone is 9876543210
```

In the above program, we have a function intro() with \*\*data as a parameter. We passed two dictionaries with variable argument length to the intro() function. We have for loop inside intro() function which works on the data of passed dictionary and prints the value of the dictionary.


##Parameter Ordering

1. parameters
2. \*args
3. default parameters
4. \*\*kwargs

Ej.:

```python
def display_info(a, b, *args, instructor="Colt", **kwargs):
  return [a, b, args, instructor, kwargs]

display_info(1, 2, 3, last_name="Steele", job="Instructor")

[1, 2, (3,), 'Colt', {'job': 'Instructor', 'last_name': 'Steele'}]
```

##Tuple Unpacking

**We can use \* as an argument to a function to "unpack" values from a tuple or a list to function as \*args.**

Ej.:
```python
def sum_all_values(*args):
    # there's a built in sum function - we'll see more later!
    return sum(args)

sum_all_values([1, 2, 3, 4]) # nope...
sum_all_values((1, 2, 3, 4)) # this does not work either...

sum_all_values(*[1, 2, 3, 4]) # 10
sum_all_values(*(1, 2, 3, 4)) # 10
```

##Dictionary Unpacking

**We can use \*\* as an argument to a function to "unpack" dictionary values into keyword.**

```python
def display_names(first, second):
    return f"{first} says hello to {second}"

names = {"first": "Colt", "second": "Rusty"}

display_names(names) # nope..
display_names(**names) "Colt says hello to Rusty"
```


#Lambdas

Normal functions have names but lambdas are **anonymous functions**.
We use lambda functions when we require a nameless function for a short period of time. **It's normally used when you have some code where you need to pass a function into another function as a parameter and that function will never be used again** like in map() or filter() function.  
**It only accepts one expression (one line) and the expression is automatically returned**

From Wikipedia, and about Lambda Calculus:

>Lambda calculus consists of constructing lambda terms and **performing reduction operations** on them
>Se puede considerar al cálculo lambda como el lenguaje universal de programación más pequeño. 
>Consiste en una regla de transformación simple (sustitución de variables) y un esquema simple para definir funciones.
>El cálculo lambda es universal porque cualquier función computable puede ser expresada y evaluada a través de él.

##Syntax

```python
lambda arguments: expression
```
```python
add_values = lambda x, y: x + y
multiply_values = lambda x, y: x * y

add_values(10, 20) # 30
multiply_values(10, 20) # 200
```

##Regular function vs. Lambda function

###Regular Function
```python
def first_function():
    return 'Hello!'

first_function() # 'Hello!'
first_function.__name__ # first_function'
```
###Lambda function
```python
first_lambda = lambda x: x + 5

first_lambda(10) # 15
first_lambda.__name__ # '<lambda>'
```

#Map
A standard function that accepts at least two arguments, a function and an "iterable" [something that can be iterated over (lists, strings, dictionaries, sets, tuples)].
**Runs the lambda for each value in the iterable and returns a map object which can be converted into another data structure**

From _Programiz_

>The **map()** function applies a given function to each item of an iterable (list, tuple etc.) and returns a list of the results.

```python
l = [1, 2, 3, 4]
doubles = list(map(lambda x: x * 2, l))

evens # [2, 4, 6, 8]
```
##Syntax
1. **function** - map() passes each item of the iterable to this function.
2. **iterable** - iterable which is to be mapped. You can pass more than one iterable to the map() function.

```python
names = [
    {'first':'Rusty', 'last': 'Steele'}, 
    {'first':'Colt', 'last': 'Steele', }, 
    {'first':'Blue', 'last': 'Steele', }
]

first_names = list(map(lambda x: x['first'], names))
first_names # ['Rusty', 'Colt', 'Blue']
```

#Filter
In simple words, the filter() method filters the given iterable with the help of a function that tests each element in the iterable to be true or not. Filter object returned can be converted into other iterables. The object contains only the values that return true to the lambda.

##Syntax
```python
filter(function, iterable)
```
1. **function** -  function that tests if elements of an iterable returns true or false. If None, the function defaults to Identity function - which returns false if any elements are false
2. **iterable** - iterable which is to be filtered, could be sets, lists, tuples, or containers of any iterators

```python
l = [1,2,3,4]

evens = list(filter(lambda x: x % 2 == 0, l))
evens # [2,4]
```
More of a complex (and useful) example:

```python
users = [
	{"username": "samuel", "tweets": ["I love cake", "I love pie", "hello world!"]},
	{"username": "katie", "tweets": ["I love my cat"]},
	{"username": "jeff", "tweets": []},
	{"username": "bob123", "tweets": []},
	{"username": "doggo_luvr", "tweets": ["dogs are the best", "I'm hungry"]},
	{"username": "guitar_gal", "tweets": []}
]
#extract inactive users using filter:
inactive_users = list(filter(lambda u: not u['tweets'], users))

#extract inactive users using list comprehension:
inactive_users2= [user for user in users if not user["tweets"]]

# extract usernames of inactive users w/ map and filter:
usernames = list(map(lambda user: user["username"].upper(), 
	filter(lambda u: not u['tweets'], users)))

# extract usernames of inactive users w/ list comprehension
usernames2 = [user["username"].upper() for user in users if not user["tweets"]]
```

##Combining _filter_ and _map_

```python
names = ['Lassie', 'Colt', 'Rusty']
list(map(lambda name: f"Your instructor is {name}", filter(lambda value: len(value) < 5, names)))
		#This binds "Your instructor is" to 'Colt'					#This drops 'Colt'
# ['Your instructor is Colt']
```

##Using list comprehension

```python
names = ['Lassie', 'Colt', 'Rusty']
answer = [f"Your instructor is {name}" for name in names if len(name)<5]
print(answer)
# ['Your instructor is Colt']
```

#Built-in Functions

## All()
Return True if **all** elements in the _iterable_ are truthy or if the iterable is empty

###Syntax
```python
all(iterable)
```
1. **iterable** - any iterable (list, tuple, dictionary, etc.) which contains the elements

Ej.:

```python
all([0,1,2,3,4]) # False

all([char for char in 'eio' if char in 'aeiou']) # True

names = ['Cristian', 'Carlos', 'Catalina', 'Carmen', 'Cataldo']
all([name[0].lower() for name in names if name[0] == name[0].upper()]) # True
```

## Any()
Return True if **any** elements in the _iterable_ are truthy. If the iterable is empty, it returns False

###Syntax
```python
any(iterable)
```
1. **iterable** - any iterable (list, tuple, dictionary, etc.) which contains the elements

Ej.:

```python
any([0,1,2,3,4]) # True

any([val for val in [1,2,3] if val > 2]) # True

any([val for val in [1,2,3] if val > 5]) # False
```

###_Aditional Note_: **Generator expressions** are like lists but lighter (save memory). They come in handy when there is no need for creating a new list. Basically, use the generator expression if what you are doing is iterating once. If you want to store and use the generated result, you are probably better off with a list comprehension.
 Ej.:

```python
names = ['Cristian', 'Carlos', 'Catalina', 'Carmen', 'Cataldo']
all(name[0] == "C" for name in names) #True 
(name[0] == "C" for name in names) # <generator object <genexpr> at 0x005F2FB0>
```
instead of 

```python
names = ['Cristian', 'Carlos', 'Catalina', 'Carmen', 'Cataldo']
[name[0] == "C" for name in names] # [True, True, True, True, True] # <class 'list'>
```
####Memory Usage Difference - Generator Expre. vs List Compre.

```python
import sys
# A simple comparison of size (in Bytes)
list_comp = sys.getsizeof([x * 10 for x in range(1000)])
gen_exp = sys.getsizeof(x * 10 for x in range(1000))

print("To do the same thing, it takes...") # To do the same thing, it takes...
print(f"List Comprehension: {list_comp} bytes") # List Comprehension: 4516 bytes 
print(f"Generator Expression: {gen_exp} bytes") # Generator Expression: 64 bytes
```

##Sorted()
Returns a **new sorted list** (it doesn't modify the original, it's a new one) from the items in iterable following specific order (either ascending or descending).

###Syntax
```python
sorted(iterable, key=None, reverse=False)
```
sorted() can take a maximum of three parameters:

1. **iterable** - A sequence (string, tuple, list) or collection (set, dictionary, frozen set) or any other iterator.
2. **key** (Optional) - A function that serves as a key for the sort comparison. Defaults to None.
	* **From Programiz:**
		If you want your own implementation for sorting, sorted() also accepts a *key* function as an optional parameter.
		Based on the results of the *key* function, you can sort the given iterable.
```
		sorted(iterable, key=len)
```
		Here, len() is Python's in-built function to count the length of an object.
		The list is sorted based on the length of the element, from the lowest count to highest.
3. **reverse** (Optional) - If True, the sorted list is reversed (or sorted in descending order). Defaults to False if not provided.

```python
# sorted (works on anything that is iterable)
more_numbers = [6,1,8,2]
sorted(more_numbers) # [1, 2, 6, 8]
print(more_numbers) # [6, 1, 8, 2]
```
_Aditional Note:_ 
>A list also has the sort() method which performs the same way as sorted(). The only difference being, the sort() method doesn't return any value and changes the original list.


####Using ***key*** parameter
```python
users = [
	{"username": "samuel", "tweets": ["I love cake", "I love pie", "hello world!"]},
	{"username": "katie", "tweets": ["I love my cat"]},
	{"username": "jeff", "tweets": [], "color": "purple"},
	{"username": "bob123", "tweets": [], "num": 10, "color": "teal"},
	{"username": "doggo_luvr", "tweets": ["dogs are the best", "I'm hungry"]},
	{"username": "guitar_gal", "tweets": []}
]

# To sort users by their username
sorted(users,key=lambda user: user['username'])

# Finding our most active users...
# Sort users by number of tweets, descending
sorted(users,key=lambda user: len(user["tweets"]), reverse=True)

# ANOTHER EXAMPLE DATA SET==================================
songs = [
	{"title": "happy birthday", "playcount": 1},
	{"title": "Survive", "playcount": 6},
	{"title": "YMCA", "playcount": 99},
	{"title": "Toxic", "playcount": 31}
]
# To sort songs by playcount
sorted(songs, key=lambda s: s['playcount']) 
```



##Max()
Return the largest item in an iterable or the largest of two or more arguments.

```python
# max (strings, dicts with same keys)
max([3,4,1,2]) # 4
max((1,2,3,4)) # 4
max('awesome') # 'w'
max({1:'a', 3:'c', 2:'b'}) # 3
```

###Syntax

```
max(iterable, *iterables, key, default)
```
####Parameters
1. **Iterable** - an iterable such as list, tuple, set, dictionary, etc.
2. **\*iterables** (optional) - any number of iterables; can be more than one
3. **key** (optional) - key function where the iterables are passed and comparison is performed based on its return value
4. **default** (optional) - default value if the given iterable is empty

If the items in an iterable are strings, the largest item (ordered alphabetically) is returned.
In the case of dictionaries, max() returns the largest key.

#### Max() for longest element in a list using key parameter

This returns the longest element in the list
```python
alpha = ['AAA', 'BBBB', 'CCCCC', 'AAAAAA']

longest = max(alpha, key = lambda x: len(x))
print(longest) # 'AAAAAA'
```

This returns the length of longest element in a list
```python
alpha = ['AAA', 'BBBB', 'CCCCC', 'AAAAAA']

longest = max(len(element) for element in alpha)
print(longest) # 6
```

#### Max() with dictionaries
```python
square = {2: 4, -3: 9, -1: 1, -2: 4}

# the largest key
key1 = max(square)
print("The largest key:", key1)    # 2

# the key whose value is the largest
key2 = max(square, key = lambda k: square[k])

print("The key with the largest value:", key2)    # -3

# getting the largest value
print("The largest value:", square[key2])    # 9

The largest key: 2
The key with the largest value: -3
The largest value: 9
```



##Min()
Return the smallest item in an iterable or the smallest of two or more arguments.

```python
# min (strings, dicts with same keys)

min([3,4,1,2]) # 1
min((1,2,3,4)) # 1
min('awesome') # 'a'
min({1:'a', 3:'c', 2:'b'}) # 1
```
###Syntax

```
min(iterable, *iterables, key, default)
```
####Parameters
1. **Iterable** - an iterable such as list, tuple, set, dictionary, etc.
2. **\*iterables** (optional) - any number of iterables; can be more than one
3. **key** (optional) - key function where the iterables are passed and comparison is performed based on its return value
4. **default** (optional) - default value if the given iterable is empty

#### Min() for shortest element in a list using key parameter

This returns the shortest element in the list
```python
alpha = ['AAA', 'BBBB', 'CCCCC', 'AAAAAA']

shortest = min(alpha, key = lambda x: len(x))
print(shortest) # 'AAA'
```

This returns the length of shortest element in a list
```python
alpha = ['AAA', 'BBBB', 'CCCCC', 'AAAAAA']

shortest = min(len(element) for element in alpha)
print(shortest) # 3
```



##len()
Return the length (the number of items) of an object. The argument may be a sequence (such as a string, tuple, list, or range) or a collection (such as a dictionary, set)

```python
len('awesome') # 7
len((1,2,3,4)) # 4
len([1,2,3,4]) # 4
len(range(0,10) # 10

len({1,2,3,4}) # 4
len({'a':1, 'b':2, 'c':2} # 3
```

###Syntax

```
len(s)
```
####Parameters
1. **s** - a sequence (string, bytes, tuple, list, or range) or a collection (dictionary, set or frozen set)

###Return value
The len() function returns the number of items of an object. Failing to pass an argument or passing an invalid argument will raise a ```TypeError``` exception.

###Behind the scenes
This is how the len() built in method works:

```python
len('hello')
#is equivalent to:
'hello'.__len__()
```


##abs()
Return the absolute value of a number. The argument may be an integer or a floating point number.

```python
abs(-5) # 5
abs(5)  # 5
```

###Syntax
```
abs(num)
```
####Parameters
1. **num** - number whose absolute value is to be returned. The number can be:
	* integer
	* floating numbers
	* complex number



##sum()
The sum() function adds the items of an iterable and returns the sum.
Takes an iterable and an optional start.
Returns the sum of start and the items of an iterable from left to right and returns the total.
_Start_ defaults to 0

```python
sum([1,2,3,4], -10) # 0
```

###Syntax
```
sum(iterable, start)
```
####Parameters
1. **iterable** - iterable (list, tuple, dict, etc). The items of the iterable should be numbers.
2. **start** (optional) - this value is added to the sum of items of the iterable. The default value of start is 0 (if omitted)

```python
numbers = [2.5, 3, 4, -5]

# start parameter = 10
numbers_sum = sum(numbers, 10)
print(numbers_sum)
#14.5
```



##round()
Return _number_ rounded to _ndigits_ precision after the decimal point. If _ndigits_ is omitted or is None, it returns the nearest integer to its input.

```python
round(10.2) # 10
round(1.212121, 2) # 1.21
```

###Syntax
```
round(number, ndigits)
```
####Parameters
1. **number** - the number to be rounded
2. **ndigits** (optional) - number up to which the given number is rounded; defaults to 0



##reversed()
The reversed() function returns the reversed iterator of the given sequence.

```python
# for string
seq_string = 'Python'
print(reversed(seq_string))
# <reversed object at 0x0024F7D0>
print(list(reversed(seq_string)))
# ['n', 'o', 'h', 't', 'y', 'P']
```
reversed() to iterate backwards
```python
print([x for x in reversed(range(0,10))])
# [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```
or using range() parameters better (or even slice method for lists)

```python
print([x for x in range(9,-1,-1)])
```

###Syntax
```
reversed(seq)
```
####Parameters
1. **seq** - the sequence to be reversed
	* A sequence is an object that supports sequence protocols: \_\_len\_\_() and \_\_getitem\_\_() methods. For example, tuple, string, list, range, etc.


##zip()
*Python zip() is an inbuilt function that returns the zip object, which is the iterator of tuples where the first item in each passed iterator is paired together, and then the second item in each passed iterator are paired together.*
It makes an iterator that aggregates elements from each of the iterables. 
Returns an iterator of tuples, where the i-th tuple contains the i-th element from each of the argument sequences or iterables.
The iterator stops when the shortest input iterable is exhausted.


```python
first_zip = zip([1,2,3], [4,5,6])

list(first_zip) # [(1, 4), (2, 5), (3, 6)]

dict(first_zip) # {1: 4, 2: 5, 3: 6}
```
_Additional Note:_
>We can use the star operator (\*) to unpack iterators that will serve as an input for zip()

```python
five_by_two = [(0, 1), (1, 2), (2, 3), (3, 4), (4, 5)]

list(zip(*five_by_two))

[(0, 1, 2, 3, 4), (1, 2, 3, 4, 5)]
```

###Syntax
```
zip(*iterables)
```
####Parameters
1. **iterables**

###Return value
The zip()function returns an iterator of tuples based on the iterable objects:

* If we do not pass any parameter, zip() returns an empty iterator

* If a single iterable is passed, zip() returns an iterator of tuples with each tuple having only one element.

* If multiple iterables are passed, zip() returns an iterator of tuples with each tuple having elements from all the iterables.

* Suppose, two iterables are passed to zip(); one iterable containing three and other containing five elements. Then, the returned iterator will contain three tuples. It's because iterator stops when the shortest iterable is exhausted.

```python
midterms = [80,91,78]
finals = [98,89,53]
students = ['dan', 'ang', 'kate']


# returns dict with {student:highest score} USING DICT COMP
# {'dan': 98, 'ang': 91, 'kate': 78}
final_grades = {t[0]:max(t[1], t[2]) for t in zip(students, midterms, finals)}


# returns dict with {student:highest score} (same thing as above) USING MAP+LAMBDA
# {'dan': 98, 'ang': 91, 'kate': 78}
final_grades = dict(
	zip(
		students,
		map(
			lambda pair: max(pair),
			zip(midterms, finals)
		)
	)
)

# returns dict with student:average score
# {'dan': 89.0, 'ang': 90.0, 'kate': 65.5}
avg_grades = dict(
	zip(
		students,
		map(
			lambda pair: ((pair[0]+pair[1])/2),
			zip(midterms, finals)
		)
	)
)

```

----

#Debugging

##Common Errors

1. **SyntaxError**: Occurs when Python encounters _incorrect syntax_ (something it doesn't parse (_analizar gramaticalmente_)). Usually due to typos or not knowing Python well enough
```python
def first: # SyntaxError
None = 1 # SyntaxError
return # SyntaxError
```

2. **NameError**: This occurs when a _variable is not defined_, i.e. it hasn't been assigned
```python
test
# NameError: name 'test' is not defined
```

3. **TypeError**: 
	* Occurs when an operation or function is applied to the wrong type
	* Occurs when Python cannot interpret an operation on two data types
```python
len(5)  
# TypeError: object of type 'int' has no len()

"awesome" + []  
# TypeError: cannot concatenate 'str' and 'list' objects
```

4. **IndexError**: Occurs when you try to access an element in a list using an invalid index (i.e. one that is outside the range of the list or string):

```python
list = ["hello"]
list[2]
# IndexError: list index out of range
```

5. **ValueError**: This occurs when a built-in operation or function receives an argument that has the right type but an inappropriate value

```python
int("foo")
# ValueError: invalid literal for int() with base 10: 'foo'
```

6. **KeyError**: This occurs when a dictionary does not have a specific key

```python
d = {}
d["foo"]
# KeyError: 'foo'
```

7. **AttributeError**: This occurs when a variable does not have an attribute

```python
"awesome".foo
# AttributeError: 'str' object has no attribute 'foo'
```
_Additional Note:_ for more excepctions chech here https://www.programiz.com/python-programming/exceptions


##Raising own exceptions
In python we can also throw errors using the _raise_ keyword. This is helpful when creating your own kinds of exception and error messages.

```python
def colorize(text, color):
	colors = ("cyan", "yellow", "blue", "green", "magenta")
	if type(text) is not str:
		raise TypeError("text must be instance of str")
	if color not in colors:
		raise ValueError("color is invalid color")
	print(f"Printed {text} in {color}")

colorize([], 'cyan')
# TypeError: text must be instance of str
```

##Handling errors
In Python, exceptions can be handled using a _try_ statement. A critical operation which can raise exception is placed inside the try clause and the code that handles exception is written in except clause.
In Python, it is **strongly** encouraged to use _try_/_except_ blocks, to catch exceptions when we can do something about them. 


```python
try: 
    foobar
except NameError as err:
    print(err)
```

###Why not catching every error?

```python
try: 
    colt
except:
    print("You tried to use a variable that was never declared!")
```
What we are doing here is catching every error, which means we are not able to correctly identify "what" went wrong. It is highly discouraged to do this. If you can't identify the error, you can't fix the non-identified error. **It's necesary to be specific about the error handled**

```python
try: 
    colt
except NameError:
    print("You tried to use a variable that was never declared!")
```


###Basic Syntax
```python
try:
	# tasks
except:
	# what to do if an error raises
else:	# Optional
	# else will run when except doesnt run 
finally:	# Optional
	# This clause is executed no matter what, and is generally used to release external resources.	
```
_Additional Note_ 
>About **finally** clause: 

>The normal use of **finally** is when one uses resources that are bound not by python, but by libraries (ex. databases, image, tk, ml, etc). Those are notorious to generate memory leaks if the resources are not freed by use of their internal destructors. **For example, we may be connected to a remote data center through the network or working with a file or working with a Graphical User Interface (GUI). In all these circumstances, we must clean up the resource once used, whether it was successful or not. These actions (closing a file, GUI or disconnecting from network) are performed in the finally clause to guarantee execution.**
Here is an example of file operations to illustrate this.
```python
try:
   f = open("test.txt",encoding = 'utf-8')
   # perform file operations
finally:
   f.close()
```

When you use try/except, make sure that a specific type of exception is being handled.
​If you want to except a handful of exceptions, you can pass a tuple of errors into the except block as well:

```python
try: 
    colt.hello
except (TypeError, AttributeError):
    print("That doesn't work with this thing.")
```

```python

def get(d,key):
	try:
		return d[key]
	except KeyError:
		return None
d = {"name": "Ricky"}
print(get(d, "city"))
d["city"]
```

Useful pattern when dealing with **user input**

```python
while True:
	try:
		num = int(input("please enter a number: "))
	except ValueError:
		print("That's not a number!")
	else:
		print("Good job, you entered a number!")
		break
	finally:
		print("RUNS NO MATTER WHAT!")
print("REST OF GAME LOGIC RUNS!")

# try:
# 	num = int(input("please enter a number: "))
# except:
# 	print("That's not a number!")
# else:
# 	print("I'M IN THE ELSE!")
# finally:
# 	print("RUNS NO MATTER WHAT!")

```

_Additional Note:_
>The following code will print the actual error raised by Python. 

```python
except (ZeroDivisionError, TypeError) as err:
print(err)
```


```python
def divide(a,b):
	try:
		result = a/b
	except (ZeroDivisionError, TypeError) as err:
		print("Something went wrong!")
		print(err)
	else:
		print(f"{a} divided by {b} is {result}")



# print(divide(1,2))
print(divide(1,'a'))
print(divide(1,0))
```

## **_pdb_** — The Python Debugger**
###_\*\* pdb has been replaced by built in **breakpoint()** in Python 3.7_
https://realpython.com/python37-new-features/#the-breakpoint-built-in

Useful when we encounter to an unexpected error. 
To set breakpoints in our code we can use pdb by inserting this line. ```import pdb; pdb.set_trace()```

```python
import pdb; pdb.set_trace() # PAY ATTENTION TO SEMI COLON ";"
```
**We must set ```pdb.set_trace()``` method a few lines before where the error raises**

Inside of the debugger we can press **c** to continue and **q** to quit. Certain characters have meaning in pdb so be careful with naming variables

```python
def add_then_multiply(num1, num2):
    sum = num1 + num2
    import pdb; pdb.set_trace()

    product = sum * num1 * num2

    return product

```


```python
# FIRST EXAMPLE:
# import pdb
# first = "First"
# second = "Second"
# pdb.set_trace()
# result = first + second
# third = "Third"
# result += third
# print(result)


# Be careful with variable names!
def add_numbers(a, b, c, d):
    import pdb; pdb.set_trace() 

    return a + b + c + d
add_numbers(1,2,3,4)

```

If you use variable names that match the pdb commands (a,c,etc.) you could mess up the debugging problem

```python
import pdb
pdb.set_trace()

Also commonly on one line:
import pdb; pdb.set_trace()
```
Common PDB Commands:
l (list)
n (next line)
p (print)
c (continue - finishes debugging)

##Breakpoint() 
https://realpython.com/python37-new-features/#the-breakpoint-built-in

https://realpython.com/python-debugging-pdb/


A breakpoint is a signal inside your code that execution should temporarily stop, so that you can look around at the current state of the program.

```python
def divide(e, f):
    breakpoint()
    return f / e
```
The script will break when it reaches **breakpoint()** and drop you into a PDB debugging session. You can type **c** and hit **Enter** to continue the script.
Now, say that you think you’ve fixed the bug. You would like to run the script again but without stopping in the debugger. You could, of course, comment out the **breakpoint()** line, but another option is to use the **PYTHONBREAKPOINT** environment variable. This variable controls the behavior of **breakpoint()**, and setting **PYTHONBREAKPOINT=0** means that any call to **breakpoint()** is ignored:

```
$ PYTHONBREAKPOINT=0 python3.7 bugs.py
ZeroDivisionError: division by zero
```

#Print Vs. Return

```print``` simply displays values inside our console in a human readable format, basically as a string. That printing itself cannot further be used by the program (computer).

On the other hand, ```return```  is a how a function gives back a value (outputs a value after finishing execution). This value can't be seen by us (unless we print it or directly execute it inside the Python shell/console which is set up to automatically show returned values), but it can be used by the program - e.g. we can set a variable to equal a function call, and that variable will be set to whatever the function returns.

Also, print  won't affect the execution flow of the function. We use it to print values to the console, check if a value is what we expect, etc. return  will stop the function and return a value from it. If there is no return statement in the function, it will return ```None```  after executing.

```print(speak(animal="cat")) ```

For example, the line above will print the returned value from the ```speak()``` function.

If you did:
```
cat_sound = speak(animal="cat")
```
It would set the ```cat_sound ```variable to whatever ```speak()``` returns.

Without the return statement in the speak function, we would get only ```None```  if we tried the same examples from above.


#Modules
Modules refer to a file containing Python statements and definitions (those are methods that correspond to that module). A file containing Python code, for e.g.: ```example.py```, is called a module and its module name would be ```example```.

Modules allow us to:

* Break down large programs into small manageable and organized files - keep Python files small

* Reuse code across multiple files by importing it

* We can define our most used functions in a module and import it, instead of copying their definitions into different programs.

## Types of modules
1. **Built-in Modules - Python Default**: [Python Standard Module Index](https://docs.python.org/3/py-modindex.html)
2. **Custom Modules**: Those we create as a Python file and import on other files. 
3. **External Modules**: Those built by the Python community that can be installed through pip and then imported


**Python Module Example**
_Create this function and save it as **example.py**_
```python
# Python Module example

def add(a, b):
   """This program adds two
   numbers and return the result"""

   result = a + b
   return result
```
_Import the module **example** and call the function **add** which is defined inside module **example.py**_

```python
import example
print(example.add(4,5))
# 9
```

##Built-in Modules

There are various ways to import modules:

1. Import a module using ```import``` statement and access the definitions inside it using the dot operator
```python
# import statement example
# to import standard module math

import math
print("The value of pi is", math.pi)
```
2. _From...import:_ We can import specific names from a module without importing the module as a whole
```python
# import only specifics methods from the module

from random import choice, shuffle, randint
print(randint(0,100))
```
3. _Import all names:_ We can import all names(definitions) from a module using the following construct
```python
# import all names from the standard module math

from math import *
print("The value of pi is", pi)
```
Importing everything with the asterisk (\*) symbol is not a good programming practice.

4. _Import with renaming:_ We can import a module by renaming it
```python
# import module by renaming it

import math as m
print("The value of pi is", m.pi)
```

5. _From...import + method alias:_ We can import a specific name from a module and use an alias for the method
```python
# import only specifics methods from the module and use alias for the method

from random import randint as rnit
print(rnit(0,100))
```

##Custom Modules
* You can import from your own code too
* The syntax is the same as before
* import from the name of the Python file

**file1**
```python
def fn():
    return "do some stuff"

def other_fn():
    return "do some other stuff"
```

**file2**
```python
import file1

file1.fn() # 'do some stuff'

file2.fn() # 'do some other stuff'
```

##External Modules
External modules are downloaded from the internet [(click here for Pypi.org)](https://pypi.org/). You can download external modules using pip

###_pip_
Is a package management system for Python. 

###### Syntax
```
python3 -m pip install NAME_OF_PACKAGE
```
###External Modules Examples

* ***termcolor***  - Adds colors to output in a Python shell
>To make the ANSI colors used in termcolor work within Windows Powershell, you'll need to also import/init [colorama](https://pypi.python.org/pypi/colorama)

```python
from colorama import init
from termcolor import colored
 
# use Colorama to make Termcolor work on Windows too
init()
 
# then use Termcolor for all colored text output
print(colored('Hello, World!', 'green', 'on_red'))
```

* ***pyfiglet*** - ASCII art creator!


##AutoPEP-8 Module - Clean up code
Cleans up code following PEP-8 guide. It mostly hits on whitespaces.
######Most common commands

Do this in console:

1. ```autopep8 --in-place somecode.py```

2. ```autopep8 --in-place -a somecode.py``` # This is a little bit more agressive on whitespaces

3. ```autopep8 --in-place -a -a somecode.py``` # This is very agressive on whitespaces


##*\_\_name\_\_* variable

When run, every Python file has a **\_\_name\_\_** variable. If the file is the **main file** being run, its value is "__main__"
Otherwise, its value is the file name.

```import``` __Revisited__:

*When you use import, Python...:*

1. Tries to find the module (if it fails, it throws an error),
2. Runs the code inside of the module being imported,
3. Creates variables in the namespace of the file with the import statement.

**Preventing code from being run**:

```python
if __name__ == '__main__':
	run_code()
	# this code will only run
	# if the file is the main file
```

_Additional Note:_
>For further information check this [link](https://www.freecodecamp.org/news/whats-in-a-python-s-name-506262fe61e8/) or this [other one](https://www.udemy.com/course/the-modern-python3-bootcamp/learn/lecture/7991096#questions/4578236)


#Making HTTP Requests with Python

**_HTTP_**: _Hypertext Transfer Protocol_

####Process URL into URL BAR:

######What goes on:

1. _DNS lookup_: takes the url (i.e. _google.com_) and finds the correct address (IP) to send a request to.
	* _DNS SERVER it's like a phonebook for the internet:_ takes a domain name (i.e.: _google.com_) and turns it into an IP addres
2. _Computer Request_: computer makes a **HTTP** request to a server looking for the actual URL
3. _Server receives requests_: the servers receives the request
4. _Server issues a response_: compiles the page searched, and send it to the client

###### 2,3 and 4 make the _Request/Response cycle_

client -> _get_ request -> IP 172.217.9.142 -> Server receives -> Search in server -> Server HTTP Response with status code -> Response body (HTML)

####*HTTP Headers* 

They are meta data about the request. They are sent with both, request and response. Permiten al cliente y al servidor enviar información adicional junto a una petición o respuesta.

__Header Examples__

_Request headers:_

* **Accept**: Acceptable content-types for response (e.g. html, json, xml)
* **Cache-Control**: Specify caching behavior
* **User-Agent**: Information about the software used to make the request

_Response headers_

* **Access-Control-Allow-Origin**: specify domains that can make requests
* **Allowed**: HTTP verbs that are allowed in requests


***Response Status Code***

Every request, receives a response, which can be diverse. 

* **2xx**: Success
* **3xx**: Redirect
* **4xx**: Client Error (your fault!)
* **5xx**: Server Error (not your fault!)


####*HTTP Verbs*

***GET*** vs. ***POST***

**GET**

1. Useful for retrieving (getting) data
2. Data passed in query string
3. **Should have no "side-effects"**
4. Can be cached
5. Can be bookmarked

**POST**

1. Useful for writing (submitting1) data
2. Data passed in request body
3. **Can have "side-effects"**
4. Not cached
5. Can't be bookmarked

####*API*

***API***: _Application Programming Interface_

An API is a software intermediary that allows two applications to talk to each other. In other words, an API is the messenger that delivers your request to the provider that you're requesting it from and then delivers the response back to you.

* Allows you to get data from another application without needing to understand how the application works
* Can often send data back in different formats. i.e.: (_JSON - JavaScript Object Notation_)
* Examples of companies with APIs: GitHub, Spotify, Google

####*Requests* - [documentation here](https://requests.readthedocs.io/en/master/user/advanced/)

* Lets us make HTTP requests from our Python code!
* Installed using pip
* Useful for web scraping/crawling, grabbing data from other APIs, etc.

```py
from requests import get

get("https://news.ycombinator.com/")

```
_Requests Headers_ - [all about HTTP headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages)

```py
import requests

response = requests.get(
    "http://www.example.com",
    headers={
        "header1": "value1",
        "header2": "value2"
    }
)
```

_Additional Note:_

>This retrieves a plain text: ```response = requests.get(url, headers={"Accept": "text/plain"})```

>This retrieves a JSON: ```response = requests.get(url, headers={"Accept": "application/json"})```.
>The format retrieved looks very similar to Python but is JSON

>This converts JSON to Python Dictionary: ```response.json()```.
>It _tells Python turn it into actual Python_.

Example: _retrieving a JSON_

```py
import requests
url = "https://icanhazdadjoke.com/"

response = requests.get(url, headers={"Accept": "application/json"})
# Response = requests.get(url, headers={"Accept": "text/plain"})
	#This throws up plain text. Not every web site has an API that response well to that Accept command.
	
data = response.json()

print(data["joke"])
print(f"status: {data['status']}")
```


####What's a Query String?

* *A way to pass data to the server as part of a GET request to give more information about what we want to get*
* Looks like this: ```http://www.example.com/?key1=value1&key2=value2```
* Browsers enforce a maximum size on length of the query string


**option 1**

```py
import requests

response = requests.get(
    "http://www.example.com?key1=value1&key2=value2"
)
```
**option 2 - preferable!**

```py
import requests

response = requests.get(
    "http://www.example.com",
    params={
        "key1": "value1",
        "key2": "value2"
    }
)
```

###### Using params in requests

```py
import requests
url = "https://icanhazdadjoke.com/search"

response = requests.get(
	url, 
	headers={"Accept": "application/json"},
	params={"term": "cat", "limit": 1}
)

data = response.json()
print(data["results"])
```
_Additional Note_:
>To figure out what ```params``` or ```headers``` to use when requesting to an API, is necesary to check the API documentation.

>Ej.: [I can haz dad joke API's documentation](https://icanhazdadjoke.com/api)

>Also, ```"https://icanhazdadjoke.com/search?term=cat&limit=1"``` is the same as 
```py
response = requests.get(
	url, 
	headers={"Accept": "application/json"},
	params={"term": "cat", "limit": 1}
```
but using actual Python code.


######A Note on APIs

* Some APIs require a key in order for you to use them
* Especially true of APIs that allow you to send data, rather than just getting data
* Typically sent as part of URL
* API keys allow for greater control of how users interact with the API
* Instructions for obtaining a key vary by API


#Object Oriented Programming (OOP)

***Object oriented programming** is a method of programming that attempts to __model some process or thing in the world__ using classes or objects. Python is not the only Object oriented programming; there are thers too!*

One of the popular approach to solve a programming problem is by **creating objects**. This is known as _Object-Oriented Programming (OOP)._

_It's a new way of thinking about how writing code_


An **object** has two characteristics:

* **attributes**
* **behavior**

Let's take an example:

_Parrot is an **object**_

* _name, age, color are **attributes**_
* _singing, dancing are **behavior**_

The concept of _OOP_ in Python **focuses on creating reusable code**. This concept is also known as **DRY** (_Don't Repeat Yourself_). _OOP_ follows some basic principles:

1. ***Inheritance***: _A process of using details from a new class without modifying existing class._
2. ***Encapsulation***: _Hiding the private details of a class from other objects._
3. ***Polymorphism***: _A concept of using common operation in different ways for different data input._

##Why OOP?

With ***object oriented programming***, the goal is to encapsulate your code into logical, hierarchical groupings using classes so that you can reason about your code at a higher level.

____

_Example_:

_Say we want to model a game of poker in our program. Each entity could be its own class in our program!_

* Game
* Player
* Card
* Deck
* Hand
* Chip
* Bet

_Card Deck Possible Implementation (**Pseudocode**)_

```
Deck {class}

_cards         {private list attribute}
_max_cards     {private int attribute}
shuffle        {public method}
deal_card      {public method}
deal_hand      {public method}
count          {public method}
```

____

##_Class_

A **class** _is a blueprint (proyecto original - cianotipo) for the object_. Classes _can contain **methods** (functions) and **attributes** (similar to keys in a dict)._ Classes define what every single instance of that class should contain. 

We can _think of class as an sketch of a parrot with labels_. Here, we use ```class``` keyword to define an empty class ```Parrot```. From class, we construct instances. _An **instance** is a specific **object created from a particular class**_.

We name classes in singular and camel case (convention), and first letter is capital: ```PockerDeck``` rather than ```Pocker_deck```

```py
class Parrot:
    pass
```

##_Object_ or _Instance_

An **object** (instance) _is an instantiation of a class_. **When a class is defined, only the description for the object is defined**. _Therefore, no memory or storage is allocated_.

Objects are constructed from a class blueprint that contain their class's methods and properties.
____

Now, we are going to show how to build the class and objects of **parrot**.

```py
class Parrot:

    # class attribute
    species = "bird"

    # instance attribute
    def __init__(self, name, age):
        self.name = name
        self.age = age

# instantiate the Parrot class
blu = Parrot("Blu", 10)

# access the class attributes
print("Blu is a {}".format(blu.__class__.species)) # Blu is a bird

# access the instance attributes
print("{} is {} years old".format( blu.name, blu.age)) # Blu is 10 years old
```

##_Methods_

**Methods** _are functions defined inside the body of a class_. They **are used to define the behaviors of an object**.

```py
class Parrot:
    
    # instance attributes
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    # instance method
    def sing(self, song):
        return "{} sings {}".format(self.name, song)

    def dance(self):
        return "{} is now dancing".format(self.name)

# instantiate the object
blu = Parrot("Blu", 10)

# call our instance methods
print(blu.sing("'Happy'")) 	# Blu sings 'Happy'
print(blu.dance())			# Blu is now dancing
```

##_Encapsulation_

Is the grouping of public and private attributes and methods into a programmatic class, **making abstraction possible**.

____

_Example_:

Designing the Deck class, I make ```cards``` a private attribute (a list)
I decide that the length of the cards should be accessed via a public method called ```count()``` -- i.e. ```Deck.count()```

____


Using OOP in Python, we can restrict access to methods and variables. This prevent data from direct modification which is called encapsulation. In Python, we denote private attribute using underscore as prefix i.e single “ \_ “ or double “ \_\_“.


```py
class Computer:

    def __init__(self):
        self.__maxprice = 900

    def sell(self):
        print("Selling Price: {}".format(self.__maxprice))

    def setMaxPrice(self, price):
        self.__maxprice = price

c = Computer()
c.sell() # 900

# change the price
c.__maxprice = 1000
c.sell() # 900

# using setter function
c.setMaxPrice(1000)
c.sell() # 1000
```
We tried to modify the price. However, we can’t change it because **Python treats the \_\_maxprice as private attributes**. To change the value, we used a setter function i.e setMaxPrice() which takes price as parameter.

######Abstraction

Means exposing only "relevant" data in a class interface, hiding private attributes and methods (aka the "inner workings") from users

____

_Example:_

As a user of the ```Deck``` class, I never call ```len(Deck.cards)```, only ```Deck.count()``` because ```Deck.cards``` is "abstracted away" for me.

____


#### Encapsulation vs. Abstraction

* _**Encapsulation** means that the internal representation of an object is generally hidden from view outside of the object’s definition._

* _**Abstraction** is a mechanism which represents the essential features without including implementation details._

>**Encapsulation:** — _Information hiding._ Things that don't actually need to be exposed to the "outside world" or the programming outside world. Ej.: list of cards of a deck. Is not something we need to access directly. 

>**Abstraction:** — _Implementation hiding._ Data is safe and secure with data abstraction.


#### Self

[Clear explanation on _self_ concept](https://www.youtube.com/watch?v=M1BAlDufqao)

[More about _self_](https://medium.com/quick-code/understanding-self-in-python-a3704319e5f0)

[Some more about it](https://pythontips.com/2013/08/07/the-self-variable-in-python-explained/)

[Guido Van Rossum explains why not to eliminate 'self'](http://neopythonic.blogspot.com/2008/10/why-explicit-self-has-to-stay.html)

In Python, when you write a class, there's no implicit reference to the current instance of the class. Instead, the first argument to each of its methods is a reference to the instance itself. Itself. That's why the first argument of a method is called self by convention (you could use any other variable name, though that's advised against as it affects readability). This self-reference is what we use to set and get the instance's attributes and to access its other methods, from within a method.

_From Programiz:_

```py
class MyClass:

	def func(self):
		print('Hello')

ob = MyClass()
ob.func()
```

>This is because, whenever an object calls its method, the object itself is passed as the first argument. So, ```ob.func()``` translates into ```MyClass.func(ob)```.


####Creating a Class

Classes in Python can have a special ```__init__``` method, which gets called every time you create an instance of the class (instantiate).

```__init__``` is a reserved method in Python classes. It is **known as a constructor in object-oriented programming concepts**.

_There are **very rare cases in which a class doesn't contain the**_ ```__init__``` _**method**_

```py
class Vehicle:

    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year
```

####Instantiating a Class

Creating an object that is an instance of a class is called **instantiating** a class.

```py
v = Vehicle("Honda", "Civic", 2017)
```

In this case, **v** becomes a Honda Civic, a new instance of Vehicle

```py
v
<__main__.Vehicle at 0x10472f5c0>
v.make
'Honda'
v.model
'Civic'
v.year
2017
```

###### Self (_following Colton Steele_)

[Colt explaining ```__init__```, ```self```, and why ```self.attribute = attribute```](https://www.udemy.com/course/the-modern-python3-bootcamp/learn/lecture/8975736#questions)

>The ```self``` keyword refers to the current class instance.
```self``` must always be the first parameter to ```__init__``` and any methods and properties on class instances.
You never have to pass it directly when calling instance methods, including ```__init__```.


```py
class Vehicle:

    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year
```

####Instance Attributes and Methods


```py
# A User class with both instance attributes and instance methods
class User:
	def __init__(self, first, last, age):
		self.first = first
		self.last = last
		self.age = age

	def full_name(self):
		return f"{self.first} {self.last}"

	def initials(self):
		return f"{self.first[0]}.{self.last[0]}."

	def likes(self, thing):
		return f"{self.first} likes {thing}"

	def is_senior(self):
		return self.age >= 65

	def birthday(self):
		self.age += 1
		return f"Happy {self.age}th, {self.first}"


user1 = User("Joe", "Smith", 68)
user2 = User("Blanca", "Lopez", 41)

print(user1.likes("Ice Cream"))
print(user2.likes("Chips"))

print(user2.initials())
print(user1.initials())

print(user2.is_senior())
print(user1.age) #Print age before we update it
print(user1.birthday()) #updates age
print(user1.age) #Print new value of age

```

**To access specific attributes on an instance, we run:**

```py
instance.attribute_name
```


```py
class Person():

    def __init__(self, first_name, last_name):
        self.first_name = first_name
        self.last_name = last_name

    def full_name(self):
        return f"My name is {self.first_name} {self.last_name}"

    def likes(self, thing):
        return f"{self.first_name} likes {thing}!" 

p = Person("Colt", "Steele")
p.full_name()
# Colt Steele
p.likes("Python")
# Colt likes Python!
```

#### Class Attributes

Class attributes live on the class itself

We can also define attributes directly on a class that are shared by all instances of a class and the class itself.

```py
# A User class with both a class attribute
class User:

	active_users = 0

	def __init__(self, first, last, age):
		self.first = first
		self.last = last
		self.age = age
		User.active_users += 1  # Adds one every time a user initializes

	def logout(self):
		User.active_users -= 1	# Subtract one every time a user logs out
		return f"{self.first} has logged out"

	def full_name(self):
		return f"{self.first} {self.last}"

	def initials(self):
		return f"{self.first[0]}.{self.last[0]}."

	def likes(self, thing):
		return f"{self.first} likes {thing}"

	def is_senior(self):
		return self.age >= 65

	def birthday(self):
		self.age += 1
		return f"Happy {self.age}th, {self.first}"

print(User.active_users)
user1 = User("Joe", "Smith", 68)
user2 = User("Blanca", "Lopez", 41)
print(User.active_users)
print(user2.logout())
print(User.active_users)
```

**Another class with a class attribute, used for validation purposes**

```py
# Another class with a class attribute, used for validation purposes
class Pet:
	allowed = ['cat', 'dog', 'fish', 'rat']

	def __init__(self, name, species):
		if species not in Pet.allowed:
			raise ValueError(f"You can't have a {species} pet!")
		self.name = name
		self.species = species

	def set_species(self,species):
		if species not in Pet.allowed:
			raise ValueError(f"You can't have a {species} pet!")
		self.species = species

cat = Pet("Blue", "cat")
dog = Pet("Wyatt", "dog")

id(cat.allowed)
# 4315448904
id(dog.allowed) 	# They all point to the same space in memory. They refer to the same thing
# 4315448904
id(Pet.allowed)
# 4315448904

```

#### Class Methods

Class methods are methods (with the ```@classmethod``` decorator) that are not concerned with instances, but the class itself.
Commonly use to validate, count or create a new instance of a class. Class methods are used when the method does not need to know about the specific instance; instance methods are the opposite. 

```py
class Person():
    # ...

    @classmethod
    def from_csv(cls, filename):
        return cls(*params) # this is the same as calling Person(*params)

Person.from_csv(my_csv)
```	

The first argument is ```cls``` (for class) instead of ```self```. Like ```self```, it does not need to be passed in explicitly.

**Class methods are available on the class itself and any instances of the class**, and **are mostly used for building new instances of classes.**

**A User class with both instance attributes and instance methods** + **_multiple variable assignment_**

```py
class User:
	active_users = 0

	@classmethod
	def display_active_users(cls):
		return f"There are currently {cls.active_users} active users"

	@classmethod
	def from_string(cls, data_str):
		first,last,age = data_str.split(",") ##This splits up a CSV string ("Tom,Jones,69") and save each peace to 3 variables:
		return cls(first, last, int(age))	# (first, last, age), Then it creates a new User

	def __init__(self, first, last, age):
		self.first = first
		self.last = last
		self.age = age
		User.active_users += 1

	def logout(self):
		User.active_users -= 1
		return f"{self.first} has logged out"

	def full_name(self):
		return f"{self.first} {self.last}"

	def initials(self):
		return f"{self.first[0]}.{self.last[0]}."

	def likes(self, thing):
		return f"{self.first} likes {thing}"

	def is_senior(self):
		return self.age >= 65

	def birthday(self):
		self.age += 1
		return f"Happy {self.age}th, {self.first}"


tom = User.from_string("Tom,Jones,89")
print(tom.first)
print(tom.full_name())
print(tom.birthday())
```

____

###### _Asignación Multiple de Variables_

[Multiple Variable Assignment - 1](https://stackoverflow.com/questions/8725673/multiple-assignment-and-evaluation-order-in-python)

[**Multiple Variable Assignment - 2**](https://crystal-lang.org/reference/syntax_and_semantics/multiple_assignment.html)

[Multiple Variable Assignment - 3](https://www.youtube.com/watch?v=1W228rb267o)

____

_Additional Note:_

>***In a return statement, only an expression can come after the "return".***

```py
return_stmt ::=  "return" [expression_list]
```

>An **assignment is a statement**. You can't put a statement after "return", because a statement isn't an expression.

>Thus, the following is wrong:

```py
def deposit(self, depo):
	return self.balance += depo
```

>**But this is right**:

```py
def deposit(self, depo):
	self.balance += depo
    return self.balance
```

____

_Additional Note:_

>[Explanation of why this can happen](https://www.udemy.com/course/the-modern-python3-bootcamp/learn/lecture/9160504#questions/8257078):
```py
class BankAccount:
 
    def __init__(self, name):
        self.name = name
        self.balance = 0.0  #----> The attribute is not passed as an argument
```
____


#### Underscores: Dunder Methods, Name Mangling, and More!

* ```_name```
Convention that means: _it's a private property or method, please don't modify it! It's intended for internal use_

However, you could access from outside the class. 

```py
class Person:
	def __init__(self, name):
		self.name = "Tony"
		self._secret = "Password"

```

* ```__name``` 
**It makes a method or an atribute particular of that class.**

What happens here is called **Name Mangling**. Python will _mangle_ (change) the name of that attribute. If you print ```dir(p)``` that attribute is going to look something like ```'_Person__msg'```. In that case, you can access using that _new name_. i.e.: ```print(p._Person__msg)``` # 'something private'

```py
class Person:
	def __init__(self, name):
		self.name = "Tony"
		self.__msg = "something private"

p = Person()
print(p.__msg)
# 'Person' object has no attribute '__msg'
dir(p)
# ['_Person__msg' ---- ETCETERA]

print(p._Person__msg)
# 'something private'

```

* ```__name__``` *python specific methods* 

____

#### String Representation ```__repr__```

The most common use-case for special methods is to make classes "look pretty" in strings.

By default, our classes look ugly:

```py
class Human:
    pass

colt = Human()
print(colt)  # <__main__.Human at 0x1062b8400>

```
We can use special methods to make it look way better!

*The ```__repr__``` method is one of several ways to provide a nicer string representation:*

```py
class Human:

    def __init__(self, name="somebody"):
        self.name = name

    def __repr__(self):
        return self.name
        
dude = Human()
print(dude)  # "somebody"

```
**You don't have to call the method; it works behinds the scene**


There are also several other dunders to return classes in string formats (notably ```__str__``` and ```__format__```), and choosing one is [a bit complicated!](https://stackoverflow.com/questions/1436703/difference-between-str-and-repr)

* ```__str__``` : retrieves something easy to read; meant for human consumption

* ```__repr__``` : it's unambiguous; the goal is to be as explicit as possible; meant for internal use; makes it easy to debug for developers but not meant for users. It's recomended to always put a ```__repr__``` on every class. 

____


##_Inheritance_

A **key feature of OOP is the ability to define a class which inherits functionalities from another class** (a "base" or "parent" class). Inheritance is a way of creating new class for using details of existing class without modifying it. The newly formed class is a derived class (or child class). Similarly, the existing class is a base class (or parent class).

###### Inhertiance Syntax
```py
class BaseClass:
  Body of base class
class DerivedClass(BaseClass):
  Body of derived class
```
Derived class inherits features from the base class, adding new features to it. ***This results into re-usability of code.***
If an attribute is not found in the class, search continues to the base class. This repeats recursively, if the base class is itself derived from other classes.

____

``` py
# parent class
class Bird:
    
    def __init__(self):
        print("Bird is ready")

    def whoisThis(self):
        print("Bird")

    def swim(self):
        print("Swim faster")

# child class
class Penguin(Bird):

    def __init__(self):
        # call super() function
        super().__init__()
        print("Penguin is ready")

    def whoisThis(self):
        print("Penguin")

    def run(self):
        print("Run faster")

peggy = Penguin()
peggy.whoisThis() 
peggy.swim()
peggy.run()
```

In Python, inheritance works by passing the parent class as an argument to the definition of a child class:

```py
class Animal:
    def make_sound(self, sound):
        print(sound)

    cool = True

class Cat(Animal):
    pass

gandalf = Cat()
gandalf.make_sound("meow")  # meow
gandalf.cool  # True
```

____

#### ```isinstance()```

To check which objects belong to which class.

***Syntax:*** 
```py
isinstance(obj, class)
```

***Parameters:***
1. ***obj:*** The object that need to be checked as a part of class or not.
2. ***class:*** class/type/tuple of class or type, against which object is needed to be checked.

***Returns:*** 
```True``` if object belongs to the given class/type if single class is passed or any of the class/type if tuple of class/type is passed, else returns ```False```. Raises a ```TypeError``` if anything other than mentioned valid class type.

____



## @property, getters and setters


[@property, getters and setters - well explained](https://www.youtube.com/watch?v=jCzT9XFZ5bw)


1. **Getters:** These are the methods used in Object-Oriented Programming (OOPS) which helps to access the private attributes from a class.
2. **Setters:** These are the methods used in OOPS feature which helps to set the value to private attributes in a class.

```py
class SampleClass:

    def __init__(self, a):
        ## private varibale or property in Python
        self.__a = a

    ## getter method to get the properties using an object
    def get_a(self):
        return self.__a

    ## setter method to change the value 'a' using an object
    def set_a(self, a):
        self.__a = a

## creating an object
obj = SampleClass(10)

## getting the value of 'a' using get_a() method
print(obj.get_a())
#10
## setting a new value to the 'a' using set_a() method
obj.set_a(45)

print(obj.get_a())
#45
```        
**What's the better to use?**
This depends on our need. _If you want private attributes and methods you can implement the class using setters, getters methods otherwise you will implement using the normal way._


1. **Property**

**interface to interact directly with private attributes or methods**

----

Esta mas aputando a los efectos a nivel "interface" con el usuario que a la funcionalidad en si. 
A un atributo privado tipo ```_age```, lo puedo modificar:

* rompiendo la convencion: ``` object._age = xxxx```

* con un metodo setter: ```object.set_age(xxxx)```

* otorgandole @property al metodo y luego llamandolo como si fuese un atributo:

```object.age = xxxx```
Este es mas parecido a cuando modifico el atributo de forma directa (pero este es un atributo privado). Y ademas, si despues cambio el codigo y lo actualizo, el cliente siempre va a llamar la función de la misma forma, es decir:
```object.age = xxxx```


```py
@property
def age(self):
	return self._age

@age.setter
def age(self, value):
	return self._age = value

	## You can add some logic here to. Validation, etc. 
```

######TODO LO QUE PONGA DEBAJO DE @property, VA A SER EL NOMBRE DE ESA PROPIEDA.
```py
@property
def age(self):				#LA PROPIEDAD AQUI ES age
	return self._age
```

___


Now, what if you want to have some conditions to set the value of an attribute in the SampleClass. Let's say if the value we passed is even and positive then we can set it to the attribute, otherwise set the value to 2.

Let's implement this by changing the ```set_a()``` method in the SampleClass.

```py 
class SampleClass1:

    def __init__(self, a):
        ## calling the set_a() method to set the value 'a' by checking certain conditions
        self.set_a(a)

    ## getter method to get the properties using an object
    def get_a(self):
        return self.__a

    ## setter method to change the value 'a' using an object
    def set_a(self, a):

        ## condition to check whether 'a' is suitable or not
        if a > 0 and a % 2 == 0:
            self.__a = a
        else:
            self.__a = 2

# Let's check the class by creating an object.

## creating an object for the class 'SampleClass1'
obj = SampleClass1(16)

print(obj.get_a())
16
```

Let's see how to implement the above class using the ```@property``` decorator.


```py
class Property:

    def __init__(self, var):
        ## initializing the attribute
        self.a = var

    @property
    def a(self):
        return self.__a

    ## the attribute name and the method name must be same which is used to set the value for the attribute
    @a.setter
    def a(self, var):
        if var > 0 and var % 2 == 0:
            self.__a = var
        else:
            self.__a = 2
```            
@property is used to get the value of a private attribute without using any getter methods. We have to put a line @property in front of the method where we return the private variable.

To set the value of the private variable, we use @method_name.setter in front of the method. We have to use it as a setter.

Let's test the class Property to check whether the decorators is working properly or not.

```py
## creating an object for the class 'Property'
obj = Property(23)

print(obj.a)
2
```

```@a.setter``` will set the value of a by checking the conditions we have mentioned in the method. 

Another way to use the property is...

```py
class AnotherWay:

    def __init__(self, var):
        ## calling the set_a() method to set the value 'a' by checking certain conditions
        self.set_a(var)

    ## getter method to get the properties using an object
    def get_a(self):
        return self.__a

    ## setter method to change the value 'a' using an object
    def set_a
    (self, var):

        ## condition to check whether var is suitable or not
        if var > 0 and var % 2 == 0:
            self.__a = var
        else:
            self.__a = 2

    a = property(get_a, set_a)

## creating an object for the 'AnotherWay' class
obj = AnotherWay(28)

print(obj.a)
28
```

Pass all the getter and setter methods to the property and assign it to the variable which you have to use as a class attribute.

----

Colt — Instructor - Respuesta - hace 2 años
**Hi Nemo,**

_You got it! It's just so that it appears that you are retrieving/changing the value of a property rather than calling a method.  So instead of ```jane.set_age(4)```  you could just do ```jane.age = 4```  but still add in some logic in the ```setter``` method.  Personally, I think it's a lot of work for little payoff, but I figured it was good to mention in the course._

**Colt**

----

Diego Siebra - hace 10 meses

Not using the parenthesis could be VERY useful. Imagine that a version of your code with the line "jane.age = 45" is being used. Assume that there are no restrictions for the values of the attribute age. If you want to put restrictions on the range of possible values, you would need a method for that (with the parenthesis and new name) or a property. With the property, other users of your class wouldn't need to change all their code to get the new functionality. They could just keep using jane.age = number instead of having to change all their code to somehing like jane.set_age(number).


----

[To reinforce hate for getters and setters, click here](https://eli.thegreenplace.net/2009/02/06/getters-and-setters-in-python/)

**Python decorators add functionality to functions and methods at definition time, they are not used to add functionality at run time.**

One simple use case will be to ```set``` **a read only instance attribute** , as you know leading a variable name with one underscore ```_x``` in python usually mean it's private (internal use) but **sometimes we want to be able to read the instance attribute and not to write it so we can use property for this**:

```py
class C(object):
	def __init__(self, x):
		self._x = x

	@property
    def x(self):
    	return self._x

c = C(1)
c.x
# 1
c.x = 2

AttributeError: "can't set attribute"
```


[From StackOverFlow - Properties, Getters and Setters](https://stackoverflow.com/questions/6304040/real-world-example-about-how-to-use-property-feature-in-python)

```py
class C(object):
    def __init__(self):
        self._x = None

    @property
    def x(self):
        """I'm the 'x' property."""
        return self._x

    @x.setter
    def x(self, value):
        self._x = value

    @x.deleter
    def x(self):
        del self._x
```

The property will work exactly the same as simply having an instance variable 'x'.

This is the best thing about **Python properties**: 
* _**From the outside, they work exactly like instance variables, which allows you to use instance variables from outside the class.**_

**This means your first example could actually use an instance variable. If things changed, and then you decide to change your implementation and a property is useful, the interface to the property would still be the same from code outside the class. A change from instance variable to property has no impact on code outside the class.**

>From **Programiz** [this example makes it clearer](https://www.programiz.com/python-programming/property)

Many other languages and programming courses will instruct that a programmer should never expose instance variables, and instead use 'getters' and 'setters' for any value to be accessed from outside the class, even the simple case as quoted in the question.

Code outside the class with many languages (e.g. Java) use

```py
object.get_i()
    #and
object.set_i(value)

#in place of (with python)
object.i
    #and 
object.i = value
``` 
**And when implementing the class there are many 'getters' and 'setters' that do exactly as your first example: replicate a simply instance variable. These getters and setters are required because if the class implementation changes, all the code outside the class will need to change. But python properties allow code outside the class to be the same as with instance variables. So code outside the class does not need to be changed if you add a property, or have a simple instance variable**. So unlike most Object Oriented languages, for your simple example you can use the instance variable instead of 'getters' and 'setters' that are really not needed, secure in the knowledge that if you change to a property in the future, the code using your class need not change.

_This means you only need create properties if there is complex behaviour, and for the very common simple case where, as described in the question, a simple instance variable is all that is needed, you can just use the instance variable._

____


####```super```

The super() keyword allows us to call the ```__init__``` function of a parent class

In the example below, we initialize the child with both its own ```__init__``` method and its parent's ```__init__``` method:

```py
class Animal:
    def __init__(self, species):
        self.species = species

class Dog(Animal):   # This means that Dog inherits from Animal
    def __init__(self, name):
        super().__init__("canine")
        self.name = name
    
bro = Dog("Bro")
bro.name  # Bro
bro.species  # canine
```
Other example

```py
# Inheritance Example Using Super()
class Animal:
	def __init__(self, name, species):
		self.name = name
		self.species = species

	def __repr__(self):
		return f"{self.name} is a {self.species}"

	def make_sound(self, sound):
		print(f"this animal says {sound}")


class Cat(Animal):			# This means that Cat inherits from Animal
	def __init__(self, name, breed, toy):
		super().__init__(name, species="Cat") # Call init on parent class
		self.breed = breed
		self.toy = toy

	def play(self):
		print(f"{self.name} plays with {self.toy}")

blue = Cat("Blue","Scottish Fold", "String")
blue.play()
```

If we don't define the ```__init__``` method inside the child class, then it will automatically inherit and call the ```__init__``` method of the parent class. The same behavior happens for the ```__repr__``` method, too.
However, if you redefine the ```__init__``` method inside the child class, then it will call that method directly and not the parent
```__init__``` method. To use the parent ```__init__``` method for the child class, you need to specifically call it inside the child class ```__init__```, where we use super() for that purpose. This allows us to use the parent ```__init__```, and also add our own child class modifications.

So yes, if a child class has its own ```__init__``` then that's the method that gets called when you create new child class instances.


```py
# A User class with both a class attribute
class User:

	active_users = 0

	def __init__(self, first, last, age):
		self.first = first
		self.last = last
		self.age = age
		User.active_users += 1  # Adds one every time a user initializes

	def logout(self):
		User.active_users -= 1	# Subtract one every time a user logs out
		return f"{self.first} has logged out"

	def full_name(self):
		return f"{self.first} {self.last}"

	def initials(self):
		return f"{self.first[0]}.{self.last[0]}."

	def likes(self, thing):
		return f"{self.first} likes {thing}"

	def is_senior(self):
		return self.age >= 65

	def birthday(self):
		self.age += 1
		return f"Happy {self.age}th, {self.first}"

class Moderators(User):
	
	total_mods = 0

	def __init__ (self, first, last, age, community):
		super().__init__(first, last, age)		
		self.community = community						#User.active_users += 1 is included when calling super()
		Moderators.total_mods += 1

	def remove_post(self):
		return f"{self.full_name()} removed a post from {self.community} community"

	@classmethod
	def display_active_mods(cls):
		return f"There are {cls.total_mods} active Moderators"


```


#### Multiple Inheritance

Python also allows classes to inherit from more than one parent class.

```py
class Aquatic:
  def __init__(self,name):
    self.name = name

  def swim(self):
    return f"{self.name} is swimming"

  def greet(self):
    return f"I am {self.name} of the sea!"

class Ambulatory:
  def __init__(self,name):
    self.name = name

  def walk(self):
    return f"{self.name} is walking"

  def greet(self):
    return f"I am {self.name} of the land!"

class Penguin(Aquatic, Ambulatory):
  def __init__(self,name):
    super().__init__(name=name)

jaws = Aquatic("Jaws")
lassie = Ambulatory("Lassie")
captain_cook = Penguin("Captain Cook")
jaws.swim() # 'Jaws is swimming'
jaws.walk() # AttributeError: 'Aquatic' object has no attribute 'walk'
jaws.greet() # 'I am Jaws of the sea!'

lassie.swim() # AttributeError: 'Ambulatory' object has no attribute 'swim'
lassie.walk() # 'Lassie is walking'
lassie.greet() # 'I am Lassie of the land!'

captain_cook.swim() # 'Captain Cook is swimming'
captain_cook.walk() # 'Captain Cook is walking'
captain_cook.greet() # 'I am Captain Cook of the sea!'   ---> THIS IS BECAUSE AQUATIC ES INHERITED FIRST, THEN AMBULATORY. SO IT INHERITS 														AQUATICS GREETS METHODS INSTEAD OF AMBULATORY GREETS METHOD
```

```Penguin``` inherits from both ```Aquatic``` and ```Ambulatory```, therefore instances of Penguin can call both the walk and swim methods.

#### Method Resolution Order _(MRO)_

Whenever you create a class, Python sets a **Method Resolution Order**, or MRO, for that class, which _is the order in which Python will look for methods on instances of that class_. (Jerarquiza)

You can programmatically reference the MRO three ways:

```__mro__``` attribute on the class
use the ```mro()``` method on the class
use the builtin ```help(cls)``` method

```py
Penguin.__mro__ 

# (<class 'multiple.Penguin'>, <class 'multiple.Aquatic'>, 
#  <class 'multiple.Ambulatory'>, <class 'object'>)

Penguin.mro() 

# [__main__.Penguin, __main__.Aquatic, __main__.Ambulatory, object]

help(Penguin) # best for HUMAN readability -> gives us a detailed chain 

```



##_Polymorphism_

Polymorphism **is an ability (in OOP) to use common interface for multiple form (data types)**.

Suppose, we need to color a shape, there are multiple shape option (rectangle, square, circle). However we could use same method to color any shape. This concept is called Polymorphism.

A key principle in OOP is the idea of polymorphism - an object can take on many (poly) forms (morph).

While a formal definition of polymorphism is more difficult, here are two important practical applications:


1. The same class method works in a similar way for different classes

```py
Cat.speak()  # meow
Dog.speak()  # woof
Human.speak()  # yo
```

2. The same operation works for different kinds of objects

```py
sample_list = [1,2,3]
sample_tuple = (1,2,3)
sample_string = "awesome"

len(sample_list)
len(sample_tuple)
len(sample_string)
```

#### Polymorphism & Inheritance

1. The same class method works in a similar way for different classes (having one method working in multiple ways depending in what class they are defined)

A common implementation of this is to have a method in a base (or parent) class that is overridden by a subclass. This is called **method overriding.**

* Each subclass will have a different implementation of the method.

* If the method is not implemented in the subclass, the version in the parent class is called instead.

```py

class Animal():
    def speak(self):
        raise NotImplementedError("Subclass needs to implement this method")

class Dog(Animal):
    def speak(self):
        return "woof"

class Cat(Animal):
    def speak(self):
        return "meow"
```

2. (Polymorphism) The same operation works for different kinds of objects. 

How does the following work in Python?

```py
8 + 2  # 10
"8" + "2"  # 82
```
The ```+``` operator is shorthand for a special method called ```__add__()``` that gets called on the first operand. If the first (left) operand is an instance of ```int```, ```__add__()``` does mathematical addition. *If it's a string, it does string concatenation.*

The answer is "**special methods**"!

Python classes have special (also known as "**magic**") methods, that are **dunders** (i.e. double underscore-named). **These are methods with special names that give instructions to Python for how to deal with objects.**

######Special Methods Applied

[Special Dunder Methods](https://docs.python.org/3/reference/datamodel.html)

Therefore, you can declare special methods on your own classes to mimic the behavior of builtin objects, like so using ```__len__```:

```py
from copy import copy
class Human:
	def __init__(self, first, last, age):
		self.first = first
		self.last = last
		self.age = age
		
	def __repr__(self):
		return f"Human named {self.first} {self.last} aged {self.age}"

	def __len__(self):
		return self.age

	def __add__(self, other):
		# When you add two humans together...you get a newborn baby Human!
		if isinstance(other, Human):
			return Human(first='Newborn', last=self.last, age=0)
		return "You can't add that!"

	def __mul__(self, other):
		# When you multiply a Human by an int, you get clones of that Human!
		if isinstance(other, int):
			return [copy(self) for i in range(other)] # THE COPY METHOD CREATES THREE OBJECTS ALLOCATED IN DIF. SPACES OF MEMORY
		return "CANT MULTIPLY!"
	


j = Human("Jenny", "Larsen", 47)
k = Human("Kevin", "Jones", 49)
# print(j)
# print(len(j))
# triplets = j * 3

# kevin and jessica have triplets!
triplets = (k + j) * 3
print(triplets)

```

_Additinal Note:_
>```copy``` method from ```copy``` module makes a copy of an object allocating it in a different place in memory, even though the object _looks_ the same


**Other example**

```py
class GrumpyDict(dict): #we don't need to define our own __init__(). We instead use the existing dict__init__()
	def __repr__(self):
		print("NONE OF YOUR BUSINESS")
		return super().__repr__()

	def __missing__(self, key):
		print(f"YOU WANT {key}?  WELL IT AINT HERE!")

	def __setitem__(self, key, value):
		print("YOU WANT TO CHANGE THE DICTIONARY?")
		print("OK FINE...")
		super().__setitem__(key, value)

	def __contains__(self, item):
		print("NO IT AINT IN HERE!")
		return False

data = GrumpyDict({"first": "Tom", "animal": "cat"})
print(data)
data['city'] = 'Tokyo'
print(data)
'city' in data

# NONE OF YOUR BUSINESS
# {'first': 'Tom', 'animal': 'cat'}
# YOU WANT TO CHANGE THE DICTIONARY?
# OK FINE...
# NONE OF YOUR BUSINESS
# {'first': 'Tom', 'animal': 'cat', 'city': 'Tokyo'}
# NO IT AINT IN HERE!

```



######String Representation

**For ```__repr__``` method go to line 3567**

____
