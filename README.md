
# Practice with Instance Variables

## Introduction
In this lesson, we will introduce using instance variables, which we use to store information about a particular instance object. We use instance variables as another tool to help us model our object oriented solutions after real-world contexts. So, while we may have a class that is modeled after a School, we have many schools. Things that differentiate schools are the `number_of_students`, `average_class_size`, `city`, etc. These all represent information about a particular school, just as instance variables represent information about a particular instance object.  

## Objectives

* Define instance variables
* Describe how instance variables give objects attributes and properties

## Defining Instance Variables

We have been writing functions and working with variables for a while now. We've talked about the difference between global variables and local variables. However, classes add another level of complexity with instance variables. Remember the *difference between local and global variables is their **scope***. Local varibles have local or function scope, that is that they are only able to be accessed inside the function in which they are defined. Global variables can be accessed from anywhere in the file. Below is an example to jog our memory:  


```python
name = "terrance" # global variable
def example_function():
    name = "jake" # local variable
    last_name = "spalding"
    print(name, last_name)

example_function() # executing fuction with local variable
print(name) # printing global variable
print(last_name) # printing local variable
```

    jake spalding
    terrance
    


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-1-6aed85cdb045> in <module>()
          7 example_function() # executing fuction with local variable
          8 print(name) # printing global variable
    ----> 9 print(last_name) # printing local variable
    

    NameError: name 'last_name' is not defined


Again, our local variable, `last_name` is bound to its local or function scope, so when we try to print its value outside of the function it is undefined. Likewise, when we try to print the `name` variable outside of the function, it refers to the globally defined `name` as opposed to the `name` defined in the `example_function`. This brings us to instance variables. They act similarly in that they are bound to their instance. This means that we define instance variables **on** instance objects. These instance variables are then only accessible through the instance on which they were defined.

The following is an example of adding an instance variable to an instance object and then accessing it later. Don't worry if it is confusing right now, the rest of this lesson will clear things up.


```python
class Person:
    pass

terrance = Person() # instantiating instance object from Person class called 'terrance'
jake = Person() # instantiating instance object from Person class called 'terrance'
terrance.first_name = "terrance" # adding an instance variable, first_name to the instance
```


```python
print(terrance.first_name) # printing instance variable accessed from the instance
```

    terrance
    


```python
print(jake.first_name) # undefined since it is not defined yet on the instance jake
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-4-0eccfe9aaa93> in <module>()
    ----> 1 print(jake.first_name) # undefined since it is not defined yet on the instance jake
    

    AttributeError: 'Person' object has no attribute 'first_name'



```python
print(first_name) # undefined since it is not being accessed from the instance
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-5-6924f43a7ba7> in <module>()
    ----> 1 print(first_name) # undefined since it is not being accessed from the instance
    

    NameError: name 'first_name' is not defined


## Okay, But Why Do We Need Instance Variables?

Let's imagine we have two drivers. We instantiate them as instances of the `ExampleDriver` class and assign them to variables, `driver_one` and `driver_two`. Let's see this:


```python
class ExampleDriver:
    pass
    
driver_one = ExampleDriver()
driver_two = ExampleDriver()
print(driver_one)
print(driver_two)
```

    <__main__.ExampleDriver object at 0x000001B132DE2518>
    <__main__.ExampleDriver object at 0x000001B132D32E48>
    

Notice anything? Pretty hard to tell who is who... How can we fix this? We could probably give them names, right? Well, how do we assign a name to these instances?

That's where instance variables come in. Instance variables can be thought of as an attribute on an object. So, if we want our instance objects to have a `name` attribute, we simply need to add it to the object.


```python
driver_one.name = 'alex'
print(driver_one.name)
```

    alex
    

Great! We have made our first instance variable and we can now start to differentiate our instance objects and make them a bit more interesting. To reiterate, adding an attribute like `name` to an instance object is done by simply using the following syntax: `variable-dot-attribute = value`. Let's add driver_two's name now, let's name them 'julian'.


```python
# add name to driver_two
driver_two.name = 'julian'
print(driver_two.name)
```

    julian
    

Now, we can imagine wanting to add many instance variables to these instance objects which would make them quite complex. We will want a way to look at the instance variables -- similar to how we want to be able to look at the keys in a dictionary. Luckily for us, there is a couple methods that do just that! 

The first, `vars`, is a method that returns a dictionary containing the keys and values that represent the instance variable names and values of an instance object. Let's see it in action:

> **Note:** instance variables and instance methods both can be referred to as `attributes` of an instance object. 


```python
vars(driver_two)
```




    {'name': 'julian'}



The next, `__dict__`, is actually a built-in attribute of all objects in Python, including Classes and instance objects. In fact, it is used every time we access an instance variable. The example below shows how accessing instance variables works behind the scenes.

```python
    driver_one.name # "alex"
    
    driver_one.__dict__["name"] # "alex"
```
Let's see what the output of the `__dict__` method looks like in action:


```python
driver_two.__dict__
```




    {'name': 'julian'}



So, to prove our example above, let's show each step of the process, starting with accessing the `name` variable with the dot (`.`) method.


```python
driver_one.name
```




    'alex'




```python
# creates a dictionary with the key 'name' pointing to the string 'alex'
driver_one.__dict__
```




    {'name': 'alex'}




```python
# creates a dictionary with the key 'name' pointing to the string 'alex'
# then accesses the key 'name' to return the value 'alex'
driver_one.__dict__['name']
```




    'alex'



## Differentiating Instance Methods And Instance Variables

Awesome! As the note above states, instance variables aren't the only attribute. Our instance methods are also attributes and a lot of the time we use them in tandem. Let's see a quick example:


```python
class Person:
    def say_hello(self):
        print("Hi! How are you today? My name is " + self.name.title() + ".")
        
jeff = Person()
jeff.name = "jeff"
```


```python
jeff.say_hello()
```

    Hi! How are you today? My name is Jeff.
    


```python
jeff.name
```




    'jeff'



So, as we can see instance variables and instance methods look very similar syntactically. In fact, the main difference between the two is that instance methods are callable attributes on an instance object and instance variables are not callable. This makes sense since instance methods have a block of code to execute and instance variables do not. 

## Summary
In this lesson we saw how to define instance variables and saw how to use them in order to give our instance objects attributes and added complexity. We then saw how to define instance methods and call them on our instance objects. 
