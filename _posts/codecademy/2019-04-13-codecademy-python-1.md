---
layout: post
title: "Codecademy - Python 1"
categories: [python]
tags: [python, codecademy python, codecademy]
comment: 1
date: 2019-05-09
toc: 1
---

{% assign img-url = '/images/posts/codecademy/python-3' %}

This note is created when I started to learn the [Learn Python 3](https://www.codecademy.com/courses/learn-python-3) on Codecademy.

- Multiplines **string**
	~~~ python
	leaves_of_grass = """
	Poets to come! orators, singers, musicians to come!
	Not to-day is to justify me and answer what I am for,
	But you, a new brood, native, athletic, continental, greater than
	  before known,
	Arouse! for you must justify me.
	"""
	~~~
- To pass variables to a **function**, there are 2 ways: *positional arguments* (1st value for the 1st arg,...) and *keyword arguments* (with the keywords)
- We can define a default keyword like this
	~~~ python
	def greet_customer(special_item, grocery_store="Engrossing Grocers"):
	    print("Welcome to "+ grocery_store + ".")
	    print("Our special is " + special_item + ".")
	    print("Have fun shopping!")
	~~~
- Multiple return values
	~~~ python
	def square_point(x_value, y_value):
	  x_2 = x_value * x_value
	  y_2 = y_value * y_value
	  return x_2, y_2
	~~~
- **Try/Except**
	~~~ python
	# raise an error
	def raises_value_error():
	  raise ValueError
	raises_value_error()
	
	# try with try/except
	def raises_value_error():
	  raise ValueError
	try:
	  raises_value_error()
	except ValueError:
	  print("You raised a ValueError!")
	~~~
- An if statement that is always false is called a **contradiction**.
- **zip**: create paired list
- Count an element in a list: `votes.count('Jake')`
- `.sort()` vs `sorted()`: 1st one returns `None` and make the change on the list while the 2nd return a sorted list.
- **List comprehension**:
  ~~~ python
  usernames = [word for word in words if word[0] == '@']
  ~~~
- **Join string**:
  ~~~ python
  my_munequita = ['My', 'Spanish', 'Harlem', 'Mona', 'Lisa']
  ' '.join(my_munequita)
  ~~~
- **Format**
  ~~~ python
  Print("Toi ten la {}".format("Anh Thi")
  Print("Toi ten la {name}, toi den tu {town}.".format(name="Anh Thi", town="Ben Tre")
  ~~~
- Date and time
  ~~~ python
  from datetime import datetime
  datetime.now() # current time
  ~~~
- **Random numbers**
  ~~~ python
  import random
  random.randint(<num1>,<num2>) # give a random integer number between <num1> and <num2> inclusive
  random.choice(<list>) # give a random element in the <list>
  ~~~
- Two different files with the same folder. One can call `from file2 import function_1` to use the `function_1` in file1.

## Virual environment

- **Virtual Environment** -> **Pipnv**
  ~~~ hash
  pip install --user pipenv
  pipenv --three # using python 3
  pipenv install numpy
  pipenv install requests==2.18.1 # specific the version
  ~~~
  - Need to add to the PATH (on Windows, add more path to `path` variable)
  - With this pipenv, we can install different versions of the package we use. Each of them is used via a created file named "Pipfile" and "Pipfile.lock"
  - If we wanna use the different shell with its installed packages, we just `cd` to the folder and use `pipenv shell`
  - Use `exit()` to exit the virtual shell
  - One can send these files (Pipfile*) to other developers so that they can use the same version for packages you need them to use.
- Check the version of some package in **python env**:
  ~~~ python
  import numpy
  print(numpy.__version__)
  ~~~
- Add multiple keys/values to a **dictionary**: `dict.update({key: value, key: value})`
- Create a dictionary from list:
  ~~~ python
  students = {key:value for key, value in zip(names, heights)}
  ~~~
- Using try/except to overcome the KeyError in the using of **dictionary**
  ~~~ python
  key_to_check = "Landmark 81"
  try:
    print(building_heights[key_to_check])
  except KeyError:
    print("That key doesn't exist!")
  ~~~
- We can use method `<dict>.key()` to find a key, if there is not, it returns `None`.
  - `<dict>.get('key', <default value if the key doesn't exist>)`
- We can use `.pop("key", default_value)` to get the value of key and delete it from the dictionary.
- We can use `list(dict)` to get all key of the dictionary or use `for key in dic.keys()`

## Read / Write to files csv, json

- **Read files**
  ~~~ python
  with open('welcome.txt') as text_file:
    text_data = text_file.read()
  print(text_data)
  ~~~
- Print down each line in the file's content
  ~~~ python
  with open("how_many_lines.txt") as lines_doc:
    for line in lines_doc.readlines():
      print(line)

  # each line
  with open('millay_sonnet.txt') as sonnet_doc:
    first_line = sonnet_doc.readline()
    second_line = sonnet_doc.readline()
    print(second_line)
  ~~~
- **Write to file**
  ~~~ python
  with open('generated_file.txt', 'w') as gen_file:
    gen_file.write("What an incredible file!")
  ~~~
- **Appending to a File**
  ~~~ python
  with open('generated_file.txt', 'a') as gen_file:
    gen_file.write("... and it still is")
  ~~~
- **Why `with` and indent**? Why is closing the file so complicated? Well, most other aspects of our code deal with things that Python itself controls. All the variables you create: integers, lists, dictionaries — these are all Python objects, and Python knows how to clean them up when it’s done with them. Since your files exist outside your Python script, we need to tell Python when we’re done with them so that it can close the connection to that file. Leaving a file connection open unnecessarily can affect performance or impact other programs on your computer that might be trying to access that file.
- Use the first line as keys
  ~~~ python
  import csv
  with open("cool_csv.csv", newline="") as cool_csv_file:
    cool_csv_dict = csv.DictReader(cool_csv_file)
    for row in cool_csv_dict:
      print(row["Cool Fact"])
  ~~~
- **Read a csv file**
  ~~~ python
  import csv
  
  with open('addresses.csv', newline='') as addresses_csv:
    address_reader = csv.DictReader(addresses_csv, delimiter=';')
    for row in address_reader:
      print(row['Address'])
  ~~~
- **Write to a csv file**
  ~~~ python
  big_list = [{'name': 'Fredrick Stein', 'userid': 6712359021, 'is_admin': False}, {'name': 'Wiltmore Denis, 'userid': 2525942, 'is_admin': False}, {'name': 'Greely Plonk', 'userid': 15890235, 'is_admin': False}, {'name': 'Dendris Stulo', 'userid': 572189563, 'is_admin': True}] 
  
  import csv
  
  with open('output.csv', 'w') as output_csv:
    fields = ['name', 'userid', 'is_admin']
    output_writer = csv.DictWriter(output_csv, fieldnames=fields)
  
    output_writer.writeheader()
    for item in big_list:
      output_writer.writerow(item)
  ~~~
- Reading a **JSON** file
  ~~~ python
  import json
  
  with open('purchase_14781239.json') as purchase_json:
    purchase_data = json.load(purchase_json)
  
  print(purchase_data['user'])
  # Prints 'ellen_greg'
  ~~~
- **Write to a json file**
  ~~~ python
  turn_to_json = {
    'eventId': 674189,
    'dateTime': '2015-02-12T09:23:17.511Z',
    'chocolate': 'Semi-sweet Dark',
    'isTomatoAFruit': True
  }
  import json
  
  with open('output.json', 'w') as json_file:
    json.dump(turn_to_json, json_file)
  ~~~

## Class

- A **class** **instance** is also called an **object**. 
- The constructor (the function called `__init__`)
- In Python `__main__` means “*this current file that we’re running*” 
- `hasattr(obj, "attr")` check if an object has an attribute or not.
- `getattr(attributeless, "other_fake_attribute", 800)`: check an attribute, if there is not, the default value will be returned.
- It’s possible for an object to have some attributes that are not explicitly defined in an object’s constructor. 
- `dir(<obj>)` to see obj's attributes
- Python automatically adds a number of attributes to all objects that get created
- Create a subclass
  ~~~ python
  class Bin:
  	pass
  class RecyclingBin(Bin):
    pass
  ~~~
- `issubclass()` is a Python built-in function that takes two parameters. `issubclass()` returns **True** if the first argument is a **subclass** of the second argument. `issubclass()` raises a **TypeError** if either argument passed in is not a class.
  ~~~ python
  issubclass(ZeroDivisionError, Exception)
  # Returns True
  ~~~
  ![subclasses]({{img-url}}/python-1-1.jpg)
- Check out the [Buit-in Exceptions hierarchy](https://docs.python.org/3/library/exceptions.html#exception-hierarchy) in Python.
- **Overriding methods**: Below we define an **Admin** class that subclasses **User**. It has all methods, attributes, and functionality that User has. However, if you call `has_permission_for` on an instance of Admin, it won’t check its permissions dictionary. Since this User is also an Admin, we just say they have permission to see everything!
  ~~~ python
  # class "User"
  class User:
    def __init__(self, username, permissions):
      self.username = username
      self.permissions = permissions
  
    def has_permission_for(self, key):
      if self.permissions.get(key):
        return True
      else:
        return False
  
  # class "Admin"
  class Admin(User):
    def has_permission_for(self, key):
      return True
  ~~~
- Sometimes, we need to **add some extra logic to the existing method**, we use `super()`
  ~~~ python
  class Sink:
    def __init__(self, basin, nozzle):
      self.basin = basin
      self.nozzle = nozzle
  
  class KitchenSink(Sink):
    def __init__(self, basin, nozzle, trash_compactor=None):
      super().__init__(basin, nozzle)
      if trash_compactor:
        self.trash_compactor = trash_compactor
  ~~~
- **Interface**: We use the same attributes / methods for 2 different classes so that if we build some function outside these classes and take the input, we don't care about the class this instance belongs to.
  - When two classes have the same method names and attributes, we say they implement **the same interface**.
  - Different objects from different classes can perform the same operation (even if it is implemented differently for each class).
- **Polymorphism** (đa hình) :
  - What’s worth remembering is that we want to implement forms that are familiar in our programs so that usage is expected.
  - Polymorphism is an abstract concept that covers a lot of ground, but defining class hierarchies that all implement the same interface is a way of introducing polymorphism to our code.
- **Dunder Methods** (`__` double underscores)
  - `__iter__`, the iterator, we use the `iter()` function to turn the list `self.user_list` into an iterator so we can use for user in `user_group` syntax.
  - `__len__`, the length method, so when we call `len(user_group)` it will return the length of the underlying `self.user_list` list.
  - `__contains__`, the check for containment, allows us to use user in `user_group` syntax to check if a User exists in the `user_list` we have.
  - Following class acts like the usual list
    ~~~ python
    class UserGroup:
      def __init__(self, users, permissions):
        self.user_list = users
        self.permissions = permissions
    
      def __iter__(self):
        return iter(self.user_list)
    
      def __len__(self):
        return len(self.user_list)
    
      def __contains__(self, user):
        return user in self.user_list
    ~~~
- Check [this project on Codecademy](https://www.codecademy.com/courses/learn-python-3/projects/basta-fazoolin) to review the lesson in practice.

## Function arguments

- `None` is nothing
  - It's `False`
  - We can use `if var is None` to check
  - default return in a function if the function has no return statement
- **Unpacking the function**
  ~~~ python
  def multiple_returns(cool_num1, cool_num2):
    sum_nums = cool_num1 + cool_num2
    div_nums = cool_num1 / cool_num2
    return sum_nums, div_nums
  
  sum, div = sum_and_div(18, 9)
  ~~~
- **Positional Argument Unpacking** (`*arg`): Below we use a single asterisk (*) to indicate we’ll accept any number of positional arguments passed to the function. Our parameter args is a tuple of all of the arguments passed. In this case args has three values inside, but it can have many more (or fewer).
  ~~~ python
  def shout_strings(*args):
    for argument in args:
      print(argument.upper())
  
  shout_strings("hi", "what do we have here", "cool, thanks!")
  # Prints out:
  # "HI"
  # "WHAT DO WE HAVE HERE"
  # "COOL, THANKS!"
  ~~~

  ~~~ python
  def truncate_sentences(length, *sentences):
    for sentence in sentences:
      print(sentence[:length])
  
  truncate_sentences(8, "What's going on here", "Looks like we've been cut off")
  # Prints out:
  # "What's g"
  # "Looks li"
  ~~~
- **Keyword Argument Unpacking** (`**kwarg`)
  ~~~ python
  def arbitrary_keyword_args(**kwargs):
    print(type(kwargs))
    print(kwargs)
  
    # See if there's an "anything_goes" keyword arg and print it
    print(kwargs.get('anything_goes'))
  ~~~

  ~~~ python
  def main(filename, *args, user_list=None, **kwargs):
    if user_list is None:
      user_list = []
  
    if '-a' in args:
      user_list = all_users()
  
    if kwargs.get('active'):
      user_list = [user for user_list if user.active]
  
    with open(filename) as user_file:
      user_file.write(user_list)

  # usage
  main("files/users/userslist.txt", 
     "-d", 
     "-a", 
     save_all_records=True, 
     user_list=current_users)

  # in the main()
  filename == "files/users/userslist.txt"
  args == ('-d', '-a)
  user_list == current_users
  kwargs == {'save_all_records': True}
  ~~~
- We don't need to change the current input to the list to the pass to the function, we can use `*` and `**` right on the call of the parameter like this
  ~~~ python
  def pour_from_sink(temperature="Warm", flow="Medium")
    set_temperature(temperature)
    set_flow(flow)
    open_sink()
  
  # Our function takes two keyword arguments
  # If we make a dictionary with their parameter names...
  sink_open_kwargs = {
    'temperature': 'Hot',
    'flow': "Slight",
  }
  
  # We can destructure them an pass to the function
  pour_from_sink(**sink_open_kwargs)
  # Equivalent to the following:
  # pour_from_sink(temperature="Hot", flow="Slight")
  ~~~