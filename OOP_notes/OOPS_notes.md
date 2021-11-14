## Definitons

### What is OOP? Why was OOP created 

* OOP was created to reduce dependencies.
* Programmers wanted to created a way to section of certain areas of code and to work and manipulate them without affecting the rest of the code.
* Helps us to think in a more abstract fasion about the code currently written.
* It was created to keep the code `DRY` (Don't Repeat Yourself). That is it helps in preventing duplication of the code.
* We are able to build application at a faster pace due to large code reusability from  pre-written code.
* Easier to manage the complexity of the software.
* Easier to conceptualize objects as real life objects.

### Classes and Objects

#### Classes

Classes are basic oulines of what an object is made of. Classes define the attributes and the behaviours of its objects. Common behaviours are grouped within a class. A class can have many objects

```ruby
class Person
	def initialize(name)
    @name = name
  end
end
```

#### Objects

Objects are instances of a class and they *encapsulate* the state of the object. Objects are **instantiated** by calling the `::new` class method on the class.

```ruby
class Person
  def initialize(name)
    @name = name
  end
end

riaz = Person.new("Riaz")
#=> riaz is the object created by calling the ::new class method on the Person class
#=> riaz has a state @name = 'riaz'
```

#### Object Instantiation

A object/instance is instantiated by calling the `::new` class method on the class. This triggers the constructor method `initialize`. The Object may or may not take arguments. And if they do then the arguments are passed in while creating a new object is assigned to the parameter available to the constructor class.

```ruby
class Person
  def initialize(name)
    @name = name
  end
end
```

#### Instance Variables

These are variables which start with the `@` (example: *@instance_variable*) and are scoped at the object level. They are available throughout the instance of the object. The objects encapsulate the state of the object. The state  of an object is the colllection of all of its instance variables and the values it references. Instance methods are used to access the value referenced by the instance variables. Instance variables exists as long as the object exists. Once the Object is destroyed then the instance variable perishes along with it.

#### Uninitialized Instance Variables

In Ruby uninitialized instance variables always returns `nil`  when we try to access them through the getter method. When we try to access an uninitialised local variable  it will raise an error.

#### Instance Methods

Instance methods are the behaviours or functionality available to the objects or the instance of the class. They are defined within the classes from which the objects are derived from. Instance variables can be accessed and exposed by the instance methods. Instance variables exists as long as the instance of the class exists and it perishes if the object perishes.

note :- Generally it is a good practice in Ruby to reassign the instance variables using the setter method. This is because the getter/setter methods are much easier to reference if we ever need to retrieve or modify the state of the object as we can make changes in just one place.

```ruby
def instance_methods(data) # defining an instance method
  data * 2
end
```

#### Class Methods

Class methods are methods which are called on the class itself. They *scoped at the class level* and are not available to any instances of the class. They cannot access instance variables. They are used when we need behaviours/methods that are not related to any objects

```ruby
class Person
  def self.class_method
    "I am from within the class method"
  end
end

Person.class_method # invoking the class method
```

#### Class variables

Class variables are accessible from within the instance methods and class methods. Class variable are defined at the class level and is available to all the instances of the class . Just one copy of the class variable exists for the Class and all of its instances. Hence reassigning the class variable at any point in the class hierarchy will change the value referenced by the class variable for the rest of the program irreversibly. This means that if a subclass changes the class variable then the value referenced would have changed to the new value when we try to access the class variable through a superclass. Due to this reason utilizing class variables can cause unexpected behaviour and due to this Rubyists tend to stay away from it.

#### Instance methods vs class methods

Instance methods are called on the instances of the class. Instance methods are the behaviours or functionality available to the objects. They are encapsulated in the Classes from which the objects are derived from. Instance variables can be accessed by the instance methods.They are defined as follows

```ruby
class Person
  def	instance_method
    "From the instance method"
  end
end

p Person.new.instance_method
# => "From the instance method"
```

Class methods are methods which are called on the class itself. They scoped at the class level and are not available to any instances of the class. They cannot access instance variables. While defining the class methods we chain the method name to the `self` keyword as shown in the example below.

```ruby
class Person
  def self.class_method
    "I am from within the class method"
  end
end

Person.class_method # invoking the class method
```

#### Setter and Getter methods

##### Getter methods

Getter methods are read-only methods which are used to access the value referenced by the instance variable.

```ruby
class Person
  def initialize(name)
    @name = name
  end

  # getter method
  def	name
    @name
  end
end

riaz = Person.new("Riaz")
p riaz.name
```

##### Setter Method

Setter methods are write-only methods which are used to set or update the value referenced by the instance variable.

```ruby
class Person
  def initialize(name)
    @name = name
  end

  # getter method
  def	name
    @name
  end

  # setter method
  def name=(input)
    @name = input
  end
end

riaz = Person.new("Riaz")
p riaz.name # => "Riaz"

riaz.name = "Another name"
p riaz.name # => "Another name"
```

Note:- generally it is a good practice in Ruby to reassign the instance variables using the setter method. This is because the getter/setter methods are much easier to reference if we ever need to retrieve or modify the state of the object as we can make changes in just one place. If you try to access an uninitialized instance variable it always returns `nil`.

##### Getter method for privacy

It is safer to invoke a setter method than to explicitly call an instance variable because we can expose sensitve data or might accidentaly modify the value it references.

```ruby
class Student

  def initialize(name, score)
    @name = name
    @score = score
  end

  def get_grades
    puts "#{name} has the grade #{finding_rank}"
  end

  private
  attr_reader :name, :score

  def finding_rank
    answer = case score
              when 85..100 then "Merit"
              when 80..84 then "Distinction"
              when 59..79 then "Pass"
              else
                "Fail"
             end
    answer            
  end

end

bob = Student.new("Bob", 85)
bob.get_grades
```

here we are encapsulating the `score` attained by the student and instead we are just showing the desired output

#### Using attr_*

The accessor methods are used to access and set the state of the object to read, set and update the values referenced by the instance variables.

The accessor methods takes symbols as arguments which it uses to create getter and setter methods.

**attr_reader** are getter methods which are read-only which is used to access and expose the value referenced by the instance variables.

**attr_writer** methods are used to define setter methods without having to define a setter method. These are write only methods used to set or update the state of the object.

**attr_accessor** methods are used as a short-hand to write both the getter and the setter methods. They are used to access and set the state of the object to read, set and update the values referenced by the instance variables.

#### Fake Operators

Many operators in Ruby are actually methods inherited from another class. Due to this we can override these methods and have our own implementation within the inheriting sub classes. As a general rule of thumb the methods in this case the fake operators should behave in a way simillar to the original methods in order to avoid unexpected/undesired results.

### Method access Control

In Ruby the method access control is implemented by the use of public, private and the protected access modifiers.

##### public methods:

 By default all the instance methods within the class are public methods apart from the constructor method `initialize` which is a private method. Public methods can be accessed from within the class and also from outside of the class. If one knows the class name or the object name then we can access these methods.

##### private methods

Private methods are methods that are accessible within the class but is not available outside of the class to the rest of the program. They are available to one instance of the class at any given time.

```ruby
class Person
  def money_available
    "You have £#{account_balance} in your account"
  end

  private

  def account_balance
    5000
  end
end

Person.new.money_available
```

##### protected methods

The protected methods are available within the class and all of its subclasses. They act as public methods when called within the class and as private methods outside of the class hiearchy. They can be used to compare two objects.

```ruby
class Student
  def initialize(grade)
    @grade = grade
  end

  def >(other)
    grade > other.grade
  end

  protected

  attr_reader :grade
end

bob = Student.new(80)
john = Student.new(90)

p bob > john # => false
p john > bob # => true
```

### Inheritance - [Class and Modules](#example-26)

##### Class Inheritance

Inheritance reduces dependencies and increases code resusability. We can use inheritance to extract common behaviours to a superclass. This helps us to keep the logic in one place. All the methods inherited from a superclass is available to its subclass. This is a great way to model concepts that are **naturally hiearchical**.

when to use class vs interface inheritance.

* If we need multiple inheritance then we use Interface inheritance as subclasses inherit from only one superclass.
* Modules cannot inherit and also modules cannot create objects. Hence inorder to create objects we need to use class inheritance
* modules have a `has-a` relationship hence they are used for namespacing and grouping commom behaviours to be shared.
* Classes have a `is-a` relationship hence it is useful for creating objects.

A subclass inherits the behaviours from a superclass. The subclass is the derived class and the super class is the base class. The superclass has a larger reusability and the subclass has an extended or refined implementation. This reduces complexity of the code and makes it reusable. Class Inheritance displays `Is - A` relationship.

```ruby
class Mammal # superclass
end

class Dog < Mammal # subclass
end
```

##### Interface Inheritance - modules

In Ruby multiple inheritance is acheived by mixin modules. The inheritance achieved through mixing in modules are known as ***Interface Inheritance***. We mix in a behaviour from a module  using the `include` method and passing in the name of the module as an argument to it. Modules are used as containers for grouping common methods and `namespacing`. Grouping simillar or related classes within a module is known as `namespacing`.  Interface inheritance have a `has - a` relationship. Eg. The Dog has a behaviour(.i.e, a method). Hence modules are useful for grouping common methods from classes that are not related hierarchially.

```ruby
module Swimmable
  def swim
    "I can swim!!!"
  end
end

class Human
  include Swimmable
end

class Dog
  include Swimmable
end

puts Human.new.swim
puts Dog.new.swim
```

### Method Lookup Path

The **order** in which Ruby inspects different classes and modules when a method is invoked is known as the `method lookup path`. Ruby looks for the method in the inheritance hierarchy up untill it finds the first instance of the method and then invokes it. If no method is found then it will raise a `NoMethodError`. This can be determined by calling the `::ancestors` class method on the class under question.

```ruby
module Speakable
  def speak(sound)
    "I am a #{self.class} and I can say #{sound}!!"
  end
end

class Animal
  include Speakable
end

class Human < Animal
end

puts Human.new.speak("Hello")
# => "I am a Human and I can say Hello!!"
p Human.ancestors
# => [Human, Animal, Speakable, Object, Kernel, BasicObject] ---> "method lookup path"
```

##### Super

Super is a keyword used by Ruby to invoke a method with the same name within the method lookup path. When we invoke a method which has a super keyword, Ruby looks in the method lookup path to find another method with the same name. Ruby invokes the method when it finds it.

The super keywords can also take arguments. But by default it will pass all the arguments passed into the calling method to the other method with the same name. In order to avoid this we can call the super keyword with a parenthesis such as `super()`.

##### Self

The `self` keyword is an explicit caller. The `self` keyword represents the `class` or the `object` of a class depending upon the scope where it is used.  

In `line xxx - xxx` we are using the `self` keyword while defining a ***method***. In line xxx the `self` in the expression `self.xxxx` represents the class `Person`. Hence this is a ***class method***. Within the class method the `self` keyword also represents the class `xxxx`.

In `line xxx - xxx` the self keyword is used within the setter instance method `xxxx`. Within an instance method the `self` keyword is the **calling object** and hence in `line xxx`  it represents the object `xxx`, which is an instance of the `xxx` class.

### Constants

How can we access constants from outside of the class?

​		In order to access the constants from outside of the class where it is defined we will have to use the `namespace resolution operator`. This is in the format `Class::CONSTANT`. The namespace resolution operator is used between the class name and the constant.

#### Lexical scope

​		When Ruby looks for a constant it first looks for the constant in the class which references it and then looks up the inheritance hierarchy when it cannot find it. This is because the constants in Ruby have a `lexical scope`.

### Polymorphism

`Polymorphism` occurs when `objects` of different types respond to the method invocation with the same name. It helps in reducing dependencies.

Polymorphism are broadly classed into two types

* Polymorphism through inheritance
* Polymorphism through Duck Typing

When the subclass inherits behaviour from one of its superclass because it could not find the method in the subclass then polymorphism occurs. This type of polymorphism is known as `Polymorphism through Inheritance` as we are inhering the behaviours. Since method overriding is also a type of inheritance this is also  `Polymorphism through Inheritance` .

When object of unrelated classes respond to the invocation of the instance method with the same name then this is known as `Polymorphism through Duck Typing`.

### Encapsulation

Ruby creates objects and exposes the interfaces to interact with those objects. Due to this it is possible that the data could be unintentionally modified. Also this can also increase the dependencies between different objects. Ruby enables us to hide the behaviour and its implementation by making it not visible to the rest of the code  in order to reduce dependencies and to prevent the data from being exposed to unwanted parts of the code. This is known as `Encapsulation` and this is acheived through the use of `Method Access Control` or access modifiers which determines if the methods are `public, private or protected`. In ruby all the instance methods are public by default unless we implement method access control. The exception being the constructor method `initialize` which is always private. All instance variables are encapsulated by default and we use the instance method to expose them.

## Worked Examples

### Example 1

\# What is output and why? What does this demonstrate about instance variables that differentiates them from local variables?

```ruby
class Person
  attr_reader :name

  def set_name
    @name = 'Bob'
  end
end

bob = Person.new
p bob.name
```

In line 9 a new object `bob` is instantiated by calling the `::new` class method on the class `Person`. Within the method we have a getter method `name` initialized by the method accessor `attr_reader ` and an instance method `set_name`. There are no instance variables defined within `Person`. Hence line 10 outputs `nil` when we invoke the setter method `name`  on the object `bob`. This is because we are trying to access an uninitialized instance variable. Uninitialized instance variables always returns `nil` when we try to access them through a getter method while an uninitialized local variable would raise an error. The **state** of the object is encapsulated by the instance variables. The state  of an object is the colllection of all of its instance variables and the values it references. Instance methods can access instance variables. Instance variables exists as long as the object exists. Once the Object is destroyed then the instance variable perishes along with it.

### Example 2

\# What is output and why? What does this demonstrate about instance variables?

```ruby
module Swimmable
  def enable_swimming
    @can_swim = true
  end
end

class Dog
  include Swimmable

  def swim
    "swimming!" if @can_swim
  end
end

teddy = Dog.new
p teddy.swim
```

In Ruby uninitialized instance variables always returns `nil`  when we try to access them through the getter method. When we try to access an uninitialised local variable  it will raise an error.

In line 15 a local variable `teddy` is instantiated to a new object by calling the `::new` class method on the class `Dog`. On line 16 the `swim` instance method is invoked on the object `teddy` which outputs `nil`. Within the `swim` method the expression `@can_swim` evaluates to `false` because the @can_swim instance method is never initialized when `teddy` is instantiated. Therefore on line 11 `"swimming!" if @can_swim` is the last evaluated expression within the method `swim`, nothing is evalutated and hence the `swim` method returns `nil`.

### Example 3 - constant scope

\# What is output and why? What does this demonstrate about constant scope? What does `self` refer to in each of the 3 methods above?

```ruby
module Describable
  def describe_shape
    "I am a #{self.class} and have #{self.class::SIDES} sides."
  end
end

class Shape
  include Describable

  def self.sides
    self::SIDES
  end

  def sides
    self.class::SIDES
  end
end

class Quadrilateral < Shape
  SIDES = 4
end

class Square < Quadrilateral; end

p Square.sides # 4
p Square.new.sides # 4
p Square.new.describe_shape # 4
```

When Ruby looks for a constant it first looks for the constant in the class which references it and then looks up the inheritance hierarchy when it cannot find it. This is because the constants in Ruby have a `lexical scope`.

On line 25 we are invoking the class method `sides` on the class `Square` this will print the integer `4`. This is because Ruby looks for the class method in the method lookup path of the `Square` class and finds it in the `Shape` class and then resolves the expression `self::SIDES` which is the same as `Square::SIDES`. Ruby looks for `SIDES` in the *method lookup path* and finds it in the `Quadilateral` class.

On line 26 the `sides` instance method is called on the new instance of the `Square` class this will output the Integer `4`. This is because Ruby looks for the method in the method lookup path and finds  `sides` instance method in the `Shape` class.  The last expression within the method is `self.class::SIDES` which equates to `Square.new.class::SIDES`. As before the value referenced by `SIDES` is `4`.

On `line 27`, we invoke the `describe_shape` instance method on a `Square` object. Since the `SIDES` constant is referenced within this method without a qualifying namespace, Ruby checks the enclosing module - the `Describable` module, to see if it defines the constant. Since it doesn't find it, Ruby raises a `NameError` error. Within the `describe_shape` method, `self` refers to the `Square` object.

### Example 4 - personalize

\# What is output? Is this what we would expect when using `AnimalClass#+`? If not, how could we adjust the implementation of `AnimalClass#+` to be more in line with what we'd expect the method to return?

```ruby
class AnimalClass
  attr_accessor :name, :animals

  def initialize(name)
    @name = name
    @animals = []
  end

  def <<(animal)
    animals << animal
  end

  def +(other_class)
    animals + other_class.animals
  end
end

class Animal
  attr_reader :name

  def initialize(name)
    @name = name
  end
end

mammals = AnimalClass.new('Mammals')
mammals << Animal.new('Human')
mammals << Animal.new('Dog')
mammals << Animal.new('Cat')

birds = AnimalClass.new('Birds')
birds << Animal.new('Eagle')
birds << Animal.new('Blue Jay')
birds << Animal.new('Penguin')

some_animal_classes = mammals + birds

p some_animal_classes
```

This code outputs an Array of animal objects which is not what is expected when we add two objects of the same class `AnimalsClass` using the `AnimalClass#+` method.

When we add two object of the same class as a rule of thumb it should evaluate an object of the same class. This is done to predict their behaviour. In the given code adding two `AnimalClass` objects evaluates to an `Array` object instead of an `AnimalClass` object.

Inorder to fix this we can modify the `AnimalClass#+` method to return an AnimalClass object as follows

```ruby
def +(other_class)
	my_own = AnimalClass.new("My animals")
  my_own.animals = animals + my_own.animals
  my_own
end
```

within the method definition we are initilializing a local variable `my_own` to the return value of initantiating an instance of the `AnimalClass`. We are invoking the `AnimalClass#animal=(name)` setter method on the object to the set the value of `@animals` instance variable to the return value of the expression `animals + my_own.animals` . Since `my_own`  is the last evaluated expression within the method, the object referenced by `my_own` is returned when the `AnimalClass#+` method is invoked.

### Example 5

\# We expect the code above to output `”Spartacus weighs 45 lbs and is 24 inches tall.”` Why does our `change_info` method not work as expected?

```ruby
class GoodDog
  attr_accessor :name, :height, :weight

  def initialize(n, h, w)
    @name = n
    @height = h
    @weight = w
  end

  def change_info(n, h, w)
    name = n
    height = h
    weight = w
  end

  def info
    "#{name} weighs #{weight} and is #{height} tall."
  end
end


sparky = GoodDog.new('Spartacus', '12 inches', '10 lbs')
sparky.change_info('Spartacus', '24 inches', '45 lbs')
puts sparky.info
# => Spartacus weighs 10 lbs and is 12 inches tall.
```

Within the `change_info` method definition we are not calling the setter methods `name, height and weight` instead we are initializing the local variables `name, age and height` and setting them to the arguments passed in during the `change_info` method invocation. Hence the value referenced by the instance variables are not reassigned. Inorder to fix the issue we will have to call the setter method on the `self` keyword which represents the current object. This is done as follows.

```ruby
def change_info(n, h, w)
  self.name = n
  self.height = h
  self.weight = w
end
```

Here the `self` keyword references the calling object. Hence the setter methods are invoked with the required parameters are passed in as arguments. Line 24 now outputs `"Spartacus weighs 45 lbs and is 24 inches tall."`

### Example 6

\# In the code above, we hope to output `'BOB'` on `line 16`. Instead, we raise an error. Why? How could we adjust this code to output `'BOB'`?

```ruby
class Person
  attr_accessor :name

  def initialize(name)
    @name = name
  end

  def change_name
    name = name.upcase
  end
end

bob = Person.new('Bob')
p bob.name
bob.change_name
p bob.name
```

In line 16 we are invoking the instance method `name` on the instance of the class `Person`. This raises an error. This is because within the method `change_name` have the experssion `name = name.upcase` where we are initialializing a new local variable `name` instead of calling the setter method `name`. In order to fix this code we have to call the setter method `name=(argument)` by invoking the setter method on  the `self` keyword as `self.name = name.upcase`. This reassign the instance variable @`name` to `"BOB"`.

```ruby
def change_name
  self.name = name.upcase
end
```

After the above modification the line 16 will output `"BOB"`.

### Example 7

 What does the code above output, and why? What does this demonstrate about class variables, and why we should avoid using class variables when working with inheritance?

```ruby
class Vehicle
  @@wheels = 4

  def self.wheels
    @@wheels
  end
end

p Vehicle.wheels                             

class Motorcycle < Vehicle
  @@wheels = 2
end

p Motorcycle.wheels                           
p Vehicle.wheels                              

class Car < Vehicle; end

p Vehicle.wheels
p Motorcycle.wheels                           
p Car.wheels  
```

Class variables are accessible from within the instance methods. Class variable are defined at the class level and is available to all the instances of the class . Just one copy of the class variable exists for the Class and all of its instances. Hence reassigning the class variable at any point in the class hierarchy will change the value referenced by the class variable for the rest of the program irreversibly. Due to this reason utilizing class variables can cause unexpected behaviour and due to this Rubyists tend to stay away from it.

Hence we get the following output

`line 9` will output the integer `4` because in `line 2` the class variable `@@wheels` is intialized to the integer `4`

`line 15` will output the integer `2` because in line 12 the class variable `@@wheels` is reassigned to the integer `2`

the same copy of the class variables remains for the rest of the program hence `lines 15, 16, 20, 21, 22` all output the integer `2`

### Example 8

\# What is output and why? What does this demonstrate about `super`?

```ruby
class Animal
  attr_accessor :name

  def initialize(name)
    @name = name
  end
end

class GoodDog < Animal
  def initialize(color)
    super
    @color = color
  end
end

bruno = GoodDog.new("brown")       
p bruno
```

`line 17` outputs the object referenced by the local variable `bruno` which is an instance of the `GoodDog` class instantiated on `line 16`.  The state of the object has two instance variables `@name and @color`. This is because within the constructor method `initialize` within the `GoodDog` class we have the `super` keyword which looks for the first occurance of the method with the same in the superclasses and invokes it. In this case it invokes the `initialize` method from the `Animal` class and passes all the arguments passed in to the constructor method in the `GoodDog` class. Thereby two instance variables `@name = brown` and `@color = brown`  are initialized.

This example demponstrates the following about the `super` keyword

Super is a keyword used by Ruby to invoke a method with the same name within the method lookup path. When we invoke a method which has a super keyword, Ruby looks in the method lookup path to find another method with the same name. Ruby invokes the method when it finds it.

The super keywords can also take arguments. But by default it will pass all the arguments passed into the calling method to the other method with the same name. In order to avoid this we can call the super keyword with a parenthesis such as `super()`.

### Example 9

\# What is output and why? What does this demonstrate about `super`?

```ruby
class Animal
  def initialize
  end
end

class Bear < Animal
  def initialize(color)
    super
    @color = color
  end
end

bear = Bear.new("black")  
```

`Line 13` raises an `ArgumentError` this is because during the instantiation of a new instance of the class `Bear` we are passing in an argument `"black"`. Within the constructor method in the `Bear` class we have a `super` keyword at `line 8`. Super keyword looks for a method with the same name in the method lookup path and then invokes it. When `super` keyword is used without parentheses it will pass all the arguments passed to the enclosing method to the method it was looking for. Here the `super`  keyword finds a similar method in the `Animal` class which does not take any arguments. Hence when `super` passes an argument to it an `ArgumentError` is raised. This can be fixed by calling the super keyword with a parantheses as follows.

```ruby
class Animal
  def initialize
  end
end

class Bear < Animal
  def initialize(color)
    super()
    @color = color
  end
end

bear = Bear.new("black")  
```

Now the code executes without any error

### Example 10

\# What is the method lookup path used when invoking `#walk` on `good_dog`?

```ruby
module Walkable
  def walk
    "I'm walking."
  end
end

module Swimmable
  def swim
    "I'm swimming."
  end
end

module Climbable
  def climb
    "I'm climbing."
  end
end

module Danceable
  def dance
    "I'm dancing."
  end
end

class Animal
  include Walkable

  def speak
    "I'm an animal, and I speak!"
  end
end

module GoodAnimals
  include Climbable

  class GoodDog < Animal
    include Swimmable
    include Danceable
  end

  class GoodCat < Animal; end
end

good_dog = GoodAnimals::GoodDog.new
p good_dog.walk
```

The method lookup path used when invoking `walk` on `GoodDog` class is [`GoodAnimals::GoodDog, Animal, Walkable]`.

### Example 11

\# What is output and why? How does this code demonstrate polymorphism?

```ruby
class Animal
  def eat
    puts "I eat."
  end
end

class Fish < Animal
  def eat
    puts "I eat plankton."
  end
end

class Dog < Animal
  def eat
     puts "I eat kibble."
  end
end

def feed_animal(animal)
  animal.eat
end

array_of_animals = [Animal.new, Fish.new, Dog.new]
array_of_animals.each do |animal|
  feed_animal(animal)
end
```

explaination from Oscar

This code outputs, `"I eat"`, `"I eat plankton."`, and `"I eat kibble."`

This is an example of polymporhism through inheritance in which objects of different types can respond to the same method invocation simply by overriding a method from the superclass.

In this example we define a `Animal` class with a `eat` method.  We also define a `Fish` class and `Dog` class that both subclass from `Animal` where they override the `eat` method that they inherit, and implement their own specialized verson of this method.

Even though every object in the `array_of_animals` array is a different object type, each with their own implementation of the `eat` method, the client code only cares that the objects can respond to the same `eat` method invocation.

### Example 12

\# We raise an error in the code above. Why? What do `kitty` and `bud` represent in relation to our `Person` object?

```ruby
class Person
  attr_accessor :name, :pets

  def initialize(name)
    @name = name
    @pets = []
  end
end

class Pet
  def jump
    puts "I'm jumping!"
  end
end

class Cat < Pet; end

class Bulldog < Pet; end

bob = Person.new("Robert")

kitty = Cat.new
bud = Bulldog.new

bob.pets << kitty
bob.pets << bud                     

bob.pets.jump
```

`line 28` the `pets` getter method returns an `Array` object with elements as the objects of the `Cat and Bulldog` class. Since `Array` class does not have a `jump` instance method defined we get an error when we call the `jump` method on the return value of the `pets` getter method been called on the object referenced by `bob`. In order to fix this issue we will have to call the `jump` instance method on each if the elements of the array as follows

```ruby
bob.pets.each(&:jump)
```

now the code executes properly and outputs `"I'm jumping!"` and `"I'm jumping!"` on two seperate lines.

### Example 13

\# What is output and why?

```ruby
class Animal
  def initialize(name)
    @name = name
  end
end

class Dog < Animal
  def initialize(name); end

  def dog_name
    "bark! bark! #{@name} bark! bark!"
  end
end

teddy = Dog.new("Teddy")
puts teddy.dog_name
```

Uninitialized instance variables always returns `nil` when we try to access them through a getter method.

In the above example within the `Dog` class there is a constructor method `initialize` which overrides the constructor method from the `Animal` class. Within the method definiton of the `initialize` method in line 8 there no instance variabled defined. Uninitialized instance variables always returns `nil` when we try to access them. In `line 16` the `dog_name` instance method is called on the object referenced by the local variable `teddy`. Within the method definition of `dog_name` from `line 10 - 13` we are trying to interpolate an uninitialised instance variable `@name` this will evaluate to an empty string `""` as `nil` evaluates to an empty string when interpolated. Due to this the expression in `line 16` outputs `"bark! bark!  bark! bark!"`

### Example 14

\# In the code above, we want to compare whether the two objects have the same name. `Line 11` currently returns `false`. How could we return `true` on `line 11`?
\# Further, since `al.name == alex.name` returns `true`, does this mean the `String` objects referenced by `al` and `alex`'s `@name` instance variables are the same object? How could we prove our case?

```ruby
class Person
  attr_reader :name

  def initialize(name)
    @name = name
  end
end

al = Person.new('Alexander')
alex = Person.new('Alexander')
p al == alex # => true
```

The `line 11` currently outputs `false` because it is comparing two objects of the same class. Each objects are unique though they may have the same state.

In order to make line 11 output `true` we can modify the code as follows by providing a custom `#==` instance method as follows

```ruby
class Person
  attr_reader :name

  def initialize(name)
    @name = name
  end

  def ==(other)
    name == other.name
  end
end

al = Person.new('Alexander')
alex = Person.new('Alexander')
p al == alex # => true
```

Now in `line 15` we are comparing the states of the two objects which have the same value and hence it returns `true`.

since `al.name == alex.name` returns `true`,  This does not mean the `String` objects referenced by `al` and `alex`'s `@name` instance variables are the same object. Though they are objects of the same class they are two different objects in memory space. This can be proved by calling the `object_id` method on them as follows

```ruby
p al.name.object_id
p alex.name.object_id
```

we notice that they both have different object id's.

### Example 15

\# What is output on `lines 14, 15, and 16` and why?

```ruby
class Person
  attr_reader :name

  def initialize(name)
    @name = name
  end

  def to_s
    "My name is #{name.upcase!}."
  end
end

bob = Person.new('Bob')
puts bob.name
puts bob
puts bob.name
```

On `line 13` a local variable `bob` is initialized to the instance of the `Person` object by calling the `new` class method on it. The `::new` method takes an argument String `"Bob"`. This is then assigned to the instance variable `@name`.On `line 8 - 10` a custom `to_s` instance method is defined and within the method definition we have an expression `name.upcase!`. Here we are invoking the getter method `name` and calling a destructive method `upcase!` on it which will permanently modify the object referenced by `@name`. Also `puts` method invocation by default invokes the `to_s` method on the arguments passed to it. Hence on `line 15` the `to_s` custom instance method is invoked and it prints out `"My name is BOB."`. Now the value refereneced by `@name` is modified permanently. Hence l`ine 16` prints `"BOB"`. If we dont want this behaviour then we can call a non destructive method as follows

```ruby
def to_s
  "My name is #{name.upcase}."
end
```

### Example 16

\# Why is it generally safer to invoke a setter method (if available) vs. referencing the instance variable directly when trying to set an instance variable within the class? Give an example.

```ruby
class Student
  def initialize(name, grade)
    @name = name
    @grade = grade
  end

  def >(other)
    grade > other.grade
  end

  protected

  attr_reader :grade
end

bob = Student.new("Bob", 80)
riaz = Student.new("Riaz", 90)
p riaz > bob # => true
p riaz.grade # => NoMethodError
```

explain why -------

### Example 17 - custom setter method

Give an example of when it would make sense to manually write a custom getter method vs. using `attr_reader`.            

```ruby
class Student
  def initialize(name)
    @name = name
  end

  def name
    puts "Hi my name is #{@name.capitalize}"
  end
end

Student.new("riaz").name
```

Creating a getter method using the `attr_reader` can be an easier way of defining setter methods. How ever if you want to manipulate the return value of the getter method or influence what it does then we will have to define a custom getter method. This will give us the added flexibility required. In the above example calling the getter method `name` will output `"Hi my name is Riaz"`.

### Example 18

\# What can executing `Triangle.sides` return? What can executing `Triangle.new.sides` return? What does this demonstrate about class variables

```ruby
class Shape
  @@sides = nil

  def self.sides
    @@sides
  end

  def sides
    @@sides
  end
end

class Triangle < Shape
  def initialize
    @@sides = 3
  end
end

class Quadrilateral < Shape
  def initialize
    @@sides = 4
  end
end

Triangle.sides
Triangle.new.sides
```

line 25 returns `nil` and `line 26`  returns the integer `3`.

On line 25 when we invoke the `sides` class method on the object `Triangle` Ruby looks in the method lookup path for any class method with the name `sides`. It finds it in the `Shape` class. At this point the value referenced by the class variable `@@sides` within the `Shape` class is `nil`. Hence Ruby resolves `@@sides` to be `nil`. Hence line 25 returns `nil`

On line 26 the `sides` instance method is called on the object of the `Triangle` class. Within the object the `@@sides` instance variable is referencing the integer `3`. Hence when Ruby looks for another method within the method lookup path it finds `sides` in the `Shape` class and returns integer `3`

### Example 19 - attr_* for every instance variable

\# What is the `attr_accessor` method, and why wouldn’t we want to just add `attr_accessor` methods for every instance variable in our class? Give an example.

The accessor methods are used to access and set the state of the object to read, set and update the values referenced by the instance variables.

The accessor methods takes symbols as arguments which it uses to create getter and setter methods.

**attr_reader** are getter methods which are read-only which is used to access and expose the value referenced by the instance variables.

**attr_writer** methods are used to define setter methods without having to define a setter method. These are write only methods used to set or update the state of the object.

Adding the `attr_accessor` method to every instance variable in the class will make the data referenced by the instance variable to be accessed from outside of the class. Hence we will be able to acess the value referenced by the instance variables and also and modify  them permanently

```ruby
class Student
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end
end

student = Student.new("Bob", 30)
p student.name # "Bob"
p student.age  # 30

student.name = "Mike"
student.age = 50

p student.name # "Mike"
p student.age  # 50
```

In the above example we able to access and change the state of the object from outside of the class.

### Example 20 - states and behaviour

\# What is the difference between states and behaviors?

Objects encapsulate the state and classes define the attributes of the behaviour of the objects. The instance variables track the state of the object. The state of the Object is unique to the object. The behaviours or the methods are what the objects can do. The instance methods can access the instance variable

Classes are basic oulines of what an object is made of. Classes define the attributes and the behaviours of its objects. Common behaviours are grouped within a class.

```ruby
class Person
  def initialize(name)
    @name = name
  end

  def name
    @name
  end
end

bob = Person.name("Bob")
bob.name
```

In the above example the object refenced by `bob` encapsulates the state `@name = "Bob"`

the state of the object is exposed by the instance method/behaviour `name` when it is called on the object in `line 12`.

### Example 21 - class  vs instance method

\# What is the difference between instance methods and class methods?

Instance methods are called on the instances of the class. Instance methods are the behaviours or functionality available to the objects. They are encapsulated in the Classes from which the objects are derived from. Instance variables can be accessed by the instance methods.They are defined as follows

```ruby
class Person
  def	instance_method
    "From the instance method"
  end
end

p Person.new.instance_method
# => "From the instance method"
```

Class methods are methods which are called on the class itself. They scoped at the class level and are not available to any instances of the class. They cannot access instance variables. While defining the class methods we chain the method name to the `self` keyword as shown in the example below.

```ruby
class Person
  def self.class_method
    "I am from within the class method"
  end
end

Person.class_method # invoking the class method
```

####

### Example 22 - Collabotator objects

What are collaborator objects, and what is the purpose of using them in OOP? Give an example of how we would work with one.

Collaborator objects are usually custom objects that are assigned to the state of another object. This way we can form associations between the two objects. Thereby making the methods of the collaborator object available to the other object

Collaborator objects are objects that are stored as state within another object.

The following is an example of using collaborator objects .

```ruby
class Person
  attr_reader :name, :pets

  def initialize(name)
    @name = name
    @pets = []
  end

  def add_pet(obj)
    pets << obj
  end

  def display_owner_with_pets
    puts "#{name} pets are:"
    puts pets
  end
end

class Pet
  attr_reader :name

  def initialize(name)
    @name = name
  end

  def to_s
    name
  end
end

bob = Person.new("Bob")
kitty = Pet.new("Kitty")
doggy = Pet.new("Doggy")

# p bob

bob.add_pet(kitty)
bob.add_pet(doggy)

# p bob

puts bob.display_owner_with_pets
```

##### Resources:

https://launchschool.com/lessons/dfff5f6b/assignments/4228f149

Objects that are stored as state within another object are also called "collaborator objects". We call such objects collaborators because they work in conjunction (or in collaboration) with the class they are associated with. For instance, bob has a collaborator object stored in the @pet variable. When we need that BullDog object to perform some action (i.e. we want to access some behavior of @pet), then we can go through bob and call the method on the object stored in @pet, such as speak or fetch.

When we work with collaborator objects, they are usually custom objects (e.g. defined by the programmer and not inherited from the Ruby core library); @pet is an example of a custom object. Yet, collaborator objects aren't strictly custom objects. Even the string object stored in @name within bob in the code above is technically a collaborator object.

Collaborator objects play an important role in object oriented design, since they also represent the connections between various actors in your program.

When working on an object oriented program be sure to consider what collaborators your classes will have and if those associations make sense, both from a technical standpoint and in terms of modeling the problem your program aims to solve.

### Example 23 - Fake Operators

How and why would we implement a fake operator in a custom class? Give an example.

```ruby
class Person
  attr_reader :name
  def initialize(name)
    @name = name
  end

  def ==(other)
    name == other.name
  end
end

oscar = Person.new("Oscar")
riaz = Person.new("Riaz")

p oscar == riaz # => false
```

why would you use a Fake Operator?

Many operators in Ruby are originally methods. Because of Ruby's syntactical sugar we are able to read them in a more natural way. Since these are methods we can override their implementation in our custom class. In the above example defining the `==` intance method  in the custom class `Person` overriddes the implementation of the method `==` given by Ruby. This makes it a `fake operator`. Hence in `line 15`  we are comparing the value referenced by the instance variable `@name` in the objects `oscar` and `riaz`. Line 15 can also be re-written as `oscar.==(riaz)`. This will return and print `false`.

### Example 24 - self  (with example)

\# What are the use cases for `self` in Ruby, and how does `self` change based on the scope it is used in? Provide examples.

```ruby
class Person
  attr_reader :name

  def initialize(name)
    @name = name
  end

  def self.name
    self
  end

  def change_name=(new_name)
    self.name = new_name
  end
end

bob = Person.new("Bob")
p Person.name # => "Person"
p bob.name # => "Bob"

bob.change_name("Bobby")
p bob.name # => "Bobby"
```

The `self` keyword is an explicit caller. The `self` keyword represents the `class` or the `object` of a class depending upon where it is used.  

In `line 8 - 10` we are using the `self` keyword while defining a ***method***. In line 8 the `self` in the expression `self.name` represents the class `Person`. Hence this is a ***class method***. Within the class method the `self` keyword also represents the class `Person`.

In `line 12 - 14` the self keyword is used within the setter instance method `change_name=(new_name)`. Within an instance method the `self` keyword is the **calling object** and hence in `line 13`  it represents the object `bob`, which is an instance of the `Person` class.

### Example 25 - Instance variable scope

 \# What does the above code demonstrate about how instance variables are scoped?

```ruby
class Person
  def initialize(n)
    @name = n
  end

  def get_name
    @name
  end
end

bob = Person.new('bob')
joe = Person.new('joe')

puts bob.inspect # => #<Person:0x000055e79be5dea8 @name="bob">
puts joe.inspect # => #<Person:0x000055e79be5de58 @name="joe">

p bob.get_name # => "bob"
```

Instance variables are variables which start with the `@` (example: *@instance_variable*) and are scoped at the **object level**. The instance variables keep track of the **state** of the object. The state  of an object is the collection of all of its instance variables and the values it references. Instance methods can access instance variables, that is it exposes the value referenced by the instance variable. Instance variables exists as long as the object exists. Once the Object is destroyed then the instance variable perishes along with it.

On line 14 the object `bob` has a state `@name = 'bob'` and on line 15 the object `joe` has the state `@name = "joe"`. This shows that though both the objects are created from the same class `Person` their states are unique to the respective objects.

### Example 26

####  Class inheritance vs Interface inheritance (mixins)

 How do class inheritance and mixing in modules affect instance variable scope? Give an example.

A typical `class inheritance` is where a **subclass** inherits its behaviours from a **superclass**. The subclass is the **derived class** and the superclass is the **base class.** The superclass has a **larger reusability** and the subclass has an **extended or refined implementation**. This reduces complexity of the code and makes it reusable. Class inheritance exhibits an `"Is - A"` relationship. Eg. The Dog *is a* mammal.

```ruby
class Mammal # superclass
end

class Dog < Mammal # subclass
end
```

##### Interface Inheritance

In Ruby *multiple inheritance* is acheived by `mixin` in modules. The inheritance achieved through mixing in modules are known as ***Interface Inheritance***. The behaviours from one or more modules are mixed in using the `include` method and passing in the name of the module as an argument to it. The modules group common methods and classes within them. This is known as `namespacing`. Interface inheritance exhibit a `"has - a"` relationship. Eg. The Dog *has a* behaviour(.i.e, a method).

```ruby
module Swimmable
  def swim
    "I can swim!!!"
  end
end

class Human
  include Swimmable
end

class Dog
  include Swimmable
end

puts Human.new.swim
puts Dog.new.swim
```

### Example 27 - Encapsulation

\# How does encapsulation relate to the public interface of a class?

Ruby creates objects and exposes the interfaces to interact with those objects. Due to this it is possible that the data could be unintentionally modified. Also this can also increase the dependencies between different objects. Ruby enables us to hide the behaviour and its implementation by making it not visible to the rest of the code  in order to reduce dependencies and to prevent the data from being exposed to unwanted parts of the code. This is known as `Encapsulation` and this is acheived through the use of `Method Access Control` or access modifiers which determines if the methods are `public, private or protected`. I ruby all the instance methods are public by default unless we implement method access control. The exception being the constructor method `initialize` which is always private.

Example

```ruby
class Student
  attr_reader :name

  def initialize(name, age)
    @name = name
    @age = age
  end

  def student_age
    age
  end

  private

  attr_reader :age
end

bob = Student.new("Bob", 19)

p bob.name         # => "Bob"
p bob.student_age  # => 19
p bob.age          # => NoMethodError
```

The above example we have hidden the implementation details of the instance method `age` from being accessed from outside of the class. This was acheive by the use of the `private` method which is an access modifier. Hence the instance method `age` can only accessed from the within the `Student` class.

### Example 28 - to_s

\# What is output and why? How could we output a message of our choice instead?

```ruby
class GoodDog
  DOG_YEARS = 7

  attr_accessor :name, :age

  def initialize(n, a)
    self.name = n
    self.age  = a * DOG_YEARS
  end
end

sparky = GoodDog.new("Sparky", 4)
puts sparky
```

Line 13 outputs the object referenced by the local variable `sparky` initialized in line 12. The object output consists of the object encoding id and the class name. This is output because when the object is  passed as an argument to the `puts` method it automatically calls the default `to_s` instance method on the argument and prints it. In order to override the default output we can define our own custom implementation of the `to_s` method as shown below.

```ruby
class GoodDog
  DOG_YEARS = 7

  attr_accessor :name, :age

  def initialize(n, a)
    self.name = n
    self.age  = a * DOG_YEARS
  end

  def to_s
    "I am #{name} and I am #{age} years old."
  end
end

sparky = GoodDog.new("Sparky", 4)
puts sparky
```

Now `line 17` outputs `"I am Sparky and I am 28 years old."`

\# How is the output above different than the output of the code below, and why?

```ruby
class GoodDog
  DOG_YEARS = 7

  attr_accessor :name, :age

  def initialize(n, a)
    @name = n
    @age  = a * DOG_YEARS
  end
end

sparky = GoodDog.new("Sparky", 4)
p sparky
```

In this code the instance variables `@name and @age` are initialized within the constructor method `initialize` . Whereas previously the `attr_accessor` methods initialized them. The values referenced by the instance variables `@name` and `@age` are set directly to them. Whereas before they are assigned to the instance variabled using the getter methods `name` and `age`.

### Example 29 - Accidental method overriding

\# When does accidental method overriding occur, and why? Give an example.

In Ruby all the custom class inherit from the class `Object`. This class has many built in methods as part of the Ruby language. Hence all the methods that are available to the class `Object` are available to all the custom classes as they subclass from the `Object` class. All subclasses can create it own custom implementation for any of the methods provided by the `Object` class through `method overriding by inheritance`. As a general rule of thumb the return value of these fake instance methods should behave in a simillar way to the original instance methods. When we accidentally define an instance method in our custom class  with the same name as that of the methods in the `Object` class `accidental method overriding` occurs.

Example

```ruby
class WhoAmI
  def is_a?(object)
    object
  end
end

identify = WhoAmI.new
answer = identify.is_a?(Integer) ? "true" : "false"
puts answer # => true
```

In the above example within the `WhoAmI` class we have a custom implementation for the `is_a?` instance method returns the object that was passed in as an argument  durring the method invocation. In  `line 8` the expression `identify.is_a?(Integer)` evaluates to `true` . This is because the `is_a?` instance method from the `WhoAmI` class overrides the default `is_a?` in the `Object` class. Due to this `line 9` outputs `true`.

### Example 30 - Method Access Control

\# How is Method Access Control implemented in Ruby? Provide examples of when we would use public, protected, and private access modifiers.

In Ruby the method access control is implemented by the use of public, private and the protected access modifiers. In Ruby `encapsulation` is acheived by using the `method access modifiers`.

##### public methods:

 By default all the instance methods within the class are public methods, apart from the constructor method `initialize` which is a private method. Public methods can be accessed from within the class and also from outside of the class. If one knows the object name and the getter method name then we can access these methods.

```ruby
class Person
  def say_hello
    puts "Hello!"
  end
end

Person.new.say_hello # => "Hello!"
```

In the above example the  instance method `say_hello` is defined within the class `Person`. Since this is a public method it can be visible from outside of the class. Therefore line 7 prints `"Hello!"` .

##### private methods

Private methods are methods that are accessible within the class but is not available outside of the class to the rest of the program. They are available to one instance of the class at any given time.  Private methods are used to hide the implementation details of methods thereby facilitating `encapsulation`.  

```ruby
class Person
  def money_available
    puts "You have £#{account_balance} in your account"
  end

  private

  def account_balance
    5000
  end
end

bob = Person.new
bob.money_available # => "You have £5000 in your account"
bob.account_balance # => NoMethodError
```

The instance method `account_balance` is made private by calling the `private` method in `line 6` . Unless otherwise stated anything that comes after this line within the class is a private method. `Line 15` raises an error because the private instance method `account_balance` is not available outside of the class `Person`.

##### protected methods

The protected methods are available within the class and all of its subclasses. They act as public methods when called within the class and as private methods outside of the class hiearchy. They can be used to compare two objects.

```ruby
class Student
  def initialize(grade)
    @grade = grade
  end

  def >(other)
    grade > other.grade
  end

  protected

  attr_reader :grade
end

bob = Student.new(80)
john = Student.new(90)

p bob > john # => false
p john > bob # => true
```

In the above example the protected method `grade` acts as a private method outside of the class hierarchy and acts as a public method. Due to this they are available to multiple instance of the same class

### Example 31 - Modules and classes

\# Describe the distinction between modules and classes.

`Classes` are basic oulines of what an object is made of. Classes define the attributes and the behaviours of its objects. Common behaviours are grouped within a class. All classes are part of a namespace in Ruby. Objects are created from a class.

```ruby
class Person
	def initialize(name)
    @name = name
  end

  def speak
    puts "Hi! How are you?"
  end
end

bob = Person.new("Bob")
bob.speak #=> "Hi! How are you?"
```

A subclass inherits the behaviours from a superclass. The subclass is the derived class and the super class is the base class. The superclass has a larger reusability and the subclass has an extended or refined implementation. This reduces complexity of the code and makes it reusable. Inheritance displays `Is - A` relationship.

```ruby
class Mammal # superclass
end

class Dog < Mammal # subclass
end
```

`Modules` are used as containers for housing methods that may be relevant to multiple classes. The collection of the methods within the module can be used in other classes through `mixins`. Unlike `classes` modules do not have any instances. Modules cannot inherit unlike the classes.

In Ruby multiple inheritance is acheived by mixin modules. The inheritance achieved through mixing in modules are known as ***Interface Inheritance***. The behaviour from a module is mixed in using the `include` method and passing in the name of the module as an argument to it. The modules group common methods, constants and classes within. This is known as `namespacing`. Interface inheritance have a `has - a` relationship. Eg. The Dog has a behaviour(.i.e, a method).

```ruby
module Swimmable
  def swim
    puts "I can swim!!!"
  end
end

class Human
  include Swimmable
end

class Dog
  include Swimmable
end

Human.new.swim
Dog.new.swim
```

### Example 32 - Polymorphism

What is polymorphism and how can we implement polymorphism in Ruby? Provide examples.

`Polymorphism` occurs when `objects` of different types respond to the method invocation with the same name. It helps in reducing dependencies.

Polymorphism are broadly classed into two types

* Polymorphism through inheritance
* Polymorphism through Duck Typing

When the subclass inherits behaviour from one of its superclass because it could not find the method in the subclass then polymorphism occurs. This type of polymorphism is known as `Polymorphism through Inheritance` as we are inhering the behaviours.

```ruby
class Vehicle
  def accelerate
    puts "Increase speed by 5 miles an hour!"
  end
end

class Car < Vehicle
end

class Motorbike < Vehicle
  def accelerate
    puts "Increase speed by 10 miles an hour!"
  end
end

car = Car.new
car.accelerate # Polymorphism through inheritance from the superclass

bike = Motorbike.new
bike.accelerate # Polymorphism through inheritance due to method overriding
```

In the above example we can see that the classes `Car` and `Motorbike` both inherit from the class `Vehicle`.  In `line 16 and 20` we are instantiating two objects from their respective classes referenced by the local variable `car` and `bike`. In line 16  the `accelerate` instance method is invoke on the object referenced by `car`. This outputs `"Increase speed by 5 miles an hour!"`. This is because Ruby looks for the method with the same name in the method lookup path and it finds it in the `Vehicle` class and invokes it.

 In `line 20` the `accelerate` instance method is invoke on the object referenced by `bike`. This outputs `"Increase speed by 10 miles an hour!"`.  The `accelerate` method in the `Motorbike` class overrides the one in the `Vehicle` class. Since method overriding is a form of inheritance this phenomenon is also known as `Polymorphism by inheritance`.

When object of unrelated classes respond to the invocation of the instance method with the same name then this is known as `Polymorphism through Duck Typing`.

```ruby
class Car
  def accelerate
    puts "Increase speed by 5 miles an hour!"
  end
end

class Motorbike
  def accelerate
    puts "Increase speed by 10 miles an hour!"
  end
end

vehicle = [Car.new, Motorbike.new]
vehicle.each { |object| object.accelerate }
# Output
# => Increase speed by 5 miles an hour!
# => Increase speed by 10 miles an hour!
```

In the above example the `Car` and `Motorbike` are two unrelated classes. Both of them have their own implementation of the instance method `accelerate`. Hence in line 14 when the objects created from both the classes are passed in as arguments to the `each` method invocation. They both respond to the `accelerate` instance method invocation with their own implementation. This is an example of `Polymorphism through Duck Typing`.

### Example 33 - Encapsulation

What is encapsulation and why is it important in Ruby? Give an example

Ruby creates objects and exposes the interfaces to interact with those objects. Due to this it is possible that the data could be unintentionally modified. Also this can also increase the dependencies between different objects. Ruby enables us to hide the behaviour and its implementation by making it not visible to the rest of the code  in order to reduce dependencies and to prevent the data from being exposed to unwanted parts of the code. This is known as `Encapsulation` and this is acheived through the use of `Method Access Control` or access modifiers which determines if the methods are `public, private or protected`. All public instance methods are accessible from outside of the class if the method name is known. In ruby all the instance methods are public by default unless we implement method access control. The exception being the constructor method `initialize` which is always private.

**note**: All the attributes within the class are encapsulated by default. In order to overcome this the getter methods are defined to access them.

Example

```ruby
class Student
  attr_reader :name

  def initialize(name, age)
    @name = name
    @age = age
  end

  def student_age
    age
  end

  private

  attr_reader :age
end

bob = Student.new("Bob", 19)

p bob.name         # => "Bob"
p bob.student_age  # => 19
p bob.age          # => NoMethodError
```

The above example we have hidden the implementation details of the instance method `age` from being accessed from outside of the class. This was acheived by the use of the `private` method which is an access modifier. Hence the instance method `age` can only accessed from the within the `Student` class.

### Example 34 - Mixing vs Inheritance - code exp

\# What is returned/output in the code? Why did it make more sense to use a module as a mixin vs. defining a parent class and using class inheritance?

```ruby
module Walkable
  def walk
    "#{name} #{gait} forward"
  end
end

class Person
  include Walkable

  attr_reader :name

  def initialize(name)
    @name = name
  end

  private

  def gait
    "strolls"
  end
end

class Cat
  include Walkable

  attr_reader :name

  def initialize(name)
    @name = name
  end

  private

  def gait
    "saunters"
  end
end

mike = Person.new("Mike")
p mike.walk

kitty = Cat.new("Kitty")
p kitty.walk
```

On `line 40` the `walk` instance method is invoked on the local variable `mike` referencing the instance of the class `Person` it ouputs and returns `"Mike strolls forward"`

On `line 43` the `walk` instance method is invoked on the local variable `kitty` referencing the instance of the class `Cat` it ouputs and returns `"Kitty saunters forward"`.

It makes sense to use a module `Walkable` to mixin the instance method `walk` in the both the classes. This is because both the classes have their own unique state with the `@name` instance variable referencing different values and they also have their own implementation of the private instance method `gait` which is interpolated in the string within the `walk` instance method. If we were to inherit `walk` from the superclass then we will not be able to manipulate the instance method in a simillar fashion.

### Example 35

#### OOP ?

\# What is Object Oriented Programming, and why was it created? What are the benefits of OOP, and examples of problems it solves?

* OOP was created to reduce dependencies.
* Programmers wanted to created a way to section of certain areas of code and to work and manipulate them without affecting the rest of the code.
* Helps us to think in a more abstract fasion about the code currently written.
* It was created to keep the code `DRY` (Don't Repeat Yourself). That is it helps in preventing duplication of the code.
* We are able to build application at a faster pace due to large code reusability from  pre-written code.
* Easier to manage the complexity of the software.
* Easier to conceptualize objects as real life objects.

### Example 36 - relation between class and objects

\# What is the relationship between classes and objects in Ruby?

#### Classes

Classes are basic oulines of what an object is made of. Classes define the attributes and the behaviours of its objects. Common behaviours are grouped within a class. A class can have many objects

```ruby
class Person
	def initialize(name)
    @name = name
  end
end
```

#### Objects

Objects are instances of a class and they *encapsulate* the state of the object. Objects are **instantiated** by calling the `::new` class method on the class.

```ruby
class Person
  def initialize(name)
    @name = name
  end
end

riaz = Person.new("Riaz")
```

In line 7 we are instantiating a new object of the `Person` class and it encapsulates the state  `@name = "Riaz"`

### Example 37

\# When should we use class inheritance vs. interface inheritance?

* If we need multiple inheritance then we use Interface inheritance as subclasses inherit from only one superclass.
* Modules cannot inherit and also modules cannot create objects. Hence inorder to create objects we need to use class inheritance
* modules have a `has-a` relationship hence they are used for namespacing and grouping commom behaviours to be shared.
* Classes have a `is-a` relationship hence it is useful for cerating objects.

A subclass inherits the behaviours from a superclass. The subclass is the derived class and the super class is the base class. The superclass has a larger reusability and the subclass has an extended or refined implementation. This reduces complexity of the code and makes it reusable. Class Inheritance displays `Is - A` relationship.

```ruby
class Mammal # superclass
end

class Dog < Mammal # subclass
end
```

##### Interface Inheritance - modules

In Ruby multiple inheritance is acheived by mixin modules. The inheritance achieved through mixing in modules are known as ***Interface Inheritance***. The behaviour from a module is mixed in using the `include` method and passing in the name of the module as an argument to it. The modules group common methods and classes within. This is known as `namespacing`. Interface inheritance have a `has - a` relationship. Eg. The Dog has a behaviour(.i.e, a method).

```ruby
module Swimmable
  def swim
    "I can swim!!!"
  end
end

class Human
  include Swimmable
end

class Dog
  include Swimmable
end

puts Human.new.swim
puts Dog.new.swim
```

### Example 38

\# If we use `==` to compare the individual `Cat` objects in the code above, will the return value be `true`? Why or why not? What does this demonstrate about classes and objects in Ruby, as well as the `==` method?

```ruby
class Cat
end

whiskers = Cat.new
ginger = Cat.new
paws = Cat.new

p whiskers == ginger
p paws == ginger
```

Line 8 and 9 will return and output `false` because in each line we are comparing two objects from the same class which are unique and they have their own encoding id. This shows that in Ruby all the objects are unique and they have their own state even if they are created from the same class. Also we can infer from this that the `==` method compares the value and when the values are the same then it evaluates to `true` else it will return `false`.

### Example 39

\# Describe the inheritance structure in the code, and identify all the superclasses.

```ruby
class Thing
end

class AnotherThing < Thing
end

class SomethingElse < AnotherThing
end
```

This is an example of `class inheritance` where the subclasses inherit from the superclass. The subclass `SomethingElse` inherits from the superclass `AnotherThing`. `AnotherThing` subclass inherits from the superclass `Thing`. `Thing` does not have any explicit superclass.

### Example 40

What is the method lookup path that Ruby will use as a result of the call to the `fly` method? Explain how we can verify this.

```ruby
module Flight
  def fly; end
end

module Aquatic
  def swim; end
end

module Migratory
  def migrate; end
end

class Animal
end

class Bird < Animal
end

class Penguin < Bird
  include Aquatic
  include Migratory
end

pingu = Penguin.new
pingu.fly
```

The **order** in which Ruby inspects different classes when a method is invoked is known as the `method lookup path`. This can be determined by calling the `#ancestors` method on the class under question.

On `line 25` the instance method `fly` is invoked on the object referenced by `pingu` which is created from the `Penguin` class. Now Ruby will look for `fly` within the method lookup path of the class `Penguin` if it cannot find it within the `Penguin` class. It will first look in the mixed in modules in an ascending order i.e in `Migration` and then followed by `Aquatic`. Since it cant find `fly` in either of them and there are no more modules mixin taking place Ruby with look in the class inheritance hierarchy. Since `Penguin` inherits from the superclass `Bird` it will look inside of it and doesnt find it. Hence `line 25` will raise a `NoMethodError`.

This can be verified by calling the `ancestors` mehtod on the object's class to get the method lookup path.

```ruby
p pingu.class.ancestors
# => [Penguin, Migratory, Aquatic, Bird, Animal, Object, PP::ObjectMixin, Kernel, BasicObject]
```

### Example 41

\# What does this code output and why?

```ruby
class Animal
  def initialize(name)
    @name = name
  end

  def speak
    puts sound
  end

  def sound
    "#{@name} says "
  end
end

class Cow < Animal
  def sound
    super + "moooooooooooo!"
  end
end

daisy = Cow.new("Daisy")
daisy.speak
```

In line 22 the `speak` instance method is invoked on the object of the `Cow` class.  This outputs `"Daisy says moooooooooooo!"`. Ruby looks in the method lookup path of the `Cow` class and finds `speak` in the `Animal` class. Within the method definition of `speak` we have the expression `puts sound`. Now Ruby looks for the `sound` instance method within the method lookup path of the `Cow` class and finds it. Within the method definition of `sound` we have the `super` keyword in line 17. `super` is a keyword used by Ruby to invoke a method with the same name within the method lookup path. When we invoke a method which has a super keyword, Ruby looks in the method lookup path to find another method with the same name. Ruby invokes the method when it finds it. Hence the expression `super + "moooooooooooo!"` resolves as `"#{@name} says " + "moooooooooooo!"` after the `super` finds `sound` in `line 10 - 13` from the `Animal` class.

The super keywords can also take arguments. But by default it will pass all the arguments passed into the calling method to the other method with the same name. In order to avoid this we can call the super keyword with a parenthesis such as `super()`.

### Example 42

\# Do `molly` and `max` have the same states and behaviors in the code below? Explain why or why not, and what this demonstrates about objects in Ruby.

```ruby
class Cat
  def initialize(name, coloring)
    @name = name
    @coloring = coloring
  end

  def purr; end

  def jump; end

  def sleep; end

  def eat; end
end

max = Cat.new("Max", "tabby")
molly = Cat.new("Molly", "gray")
```

`max` has the state `@name="Max", @coloring="tabby"` and `molly` has the state `@name="Molly", @coloring="gray"`. Therefore we can see that both `molly` and `max` which are instances of the same object have different states. This is because in Ruby the objects ,which are created from the class, encapsulate the state and the behaviours are defined by the classes. The objects are unique and their states are specific to them. However both the objects have the same behaviour as they are defined in the class they are created from.

### Example 43

```ruby
class Student
  attr_accessor :name, :grade

  def initialize(name)
    @name = name
    @grade = nil
  end

  def change_grade(new_grade)
    grade = new_grade
  end
end

priya = Student.new("Priya")
priya.change_grade('A')
priya.grade
```

\# In the above code snippet, we want to return `”A”`. What is actually returned and why? How could we adjust the code to produce the desired result?

On line 16 when the instance method `grade` is invoked on the object referenced by  `priya` it returns `nil`. This is because the argument `A` passed in to the setter method `change_grade` invocation in `line 15` does not reassign the value referenced by the `@grade` instance variable in `line 10`. Instead in `line 10` Ruby is initializing a local variable `grade` to the string `A`. Hence `@grade` is never reassigned and is always `nil`. In order to fix this we have to call the `grade` getter method on the `self` keyword in line 10 as follows

```ruby
def change_grade(new_grade)
  self.grade = new_grade
end
```

Now when `priya.grade ` executes in `line 16` string `"A"` is returned.

### Example 44

\# What does each `self` refer to in the above code snippet?

```ruby
class MeMyselfAndI
  self

  def self.me
    self
  end

  def myself
    self
  end
end

i = MeMyselfAndI.new
```

The `self` keyword is an explicit caller. The `self` keyword represents the `class` or the `object` of a class depending upon the scope where it is used.  

In line 2 `self` represents the class `MeMyselfAndI` as it is defined in the scope of the class. In line 4 `self` is used while defining a class method `me`.  Here `self` represents the class `MeMyselfAndI`. There for line 4 - 5 can also be written as

```ruby
def MeMyselfAndI.me
  self
end
```

within the scope of the class methods `self` always represents the class.

In line 8 - 10 `self` is used within the method definition if the instance method `myself`. Hence within the instance method `self` always represents the calling object `i`  of the class `MeMyselfAndI`.

### Example 45

\# Running the following code will not produce the output shown on the last line. Why not? What would we need to change, and what does this demonstrate about instance variables?

```ruby
class Student
  attr_accessor :grade

  def initialize(name, grade=nil)
    @name = name
  end
end

ade = Student.new('Adewale')
p ade # => #<Student:0x00000002a88ef8 @grade=nil, @name="Adewale">
```

This is because within the constructor method `initialize` we have not defined the instance variable `@grade`. Therefore it is not included in the state during instantiation of the instance `ade`. In order to fix the code we will have to initialize the instance variable `@grade` as follows

```ruby
class Student
  attr_accessor :grade

  def initialize(name, grade=nil)
    @grade = grade
    @name = name
  end
end

ade = Student.new('Adewale')
p ade # => #<Student:0x00000002a88ef8 @grade=nil, @name="Adewale">
```

Now line 11 will return the desired output. This demonstrates that the instance variables tracks the state of the object.

### Example 46

\# What is output and returned, and why? What would we need to change so that the last line outputs `”Sir Gallant is speaking.”`?

```ruby
class Character
  attr_accessor :name

  def initialize(name)
    @name = name
  end

  def speak
    "#{@name} is speaking."
  end
end

class Knight < Character
  def name
    "Sir " + super
  end
end

sir_gallant = Knight.new("Gallant")
p sir_gallant.name
p sir_gallant.speak
```

Line 20 when the `name` is invoked on the `sir_gallant` object it   outputs `"Sir Gallant"`. Line 21 when the `speak` is invoked on the `sir_gallant` object it   outputs `"Gallant is speaking"`. This is because we are using the instance variable `@name` . If we change this to the getter method `name` then the last line outputs `"Sir Gallant is speaking."`.

### Example 47

\# What is output and why?

```ruby
class FarmAnimal
  def speak
    "#{self} says "
  end
end

class Sheep < FarmAnimal
  def speak
    super + "baa!"
  end
end

class Lamb < Sheep
  def speak
    super + "baaaaaaa!"
  end
end

class Cow < FarmAnimal
  def speak
    super + "mooooooo!"
  end
end

p Sheep.new.speak
p Lamb.new.speak
p Cow.new.speak
```

Line 25, 26, and 27 when the `speak` instance method is invoked on the instance of the class `Sheep, Lamb and Cow` it outputs a string with the object interpolated instead of the class name on seperate lines. This is because with the body of the instance method `speak` within the `FarmAnimal` class we have the expression `"#{self} says "`. Here `self` evaluates to the calling object. Inorder to fix this the `class` method should be invoked on `self` as follows.

```ruby
def speak
  "#{self.class} says "
end
```

Now the last three lines output

`"Sheep says baa!"`
`"Lamb says baa!baaaaaaa!"`
`"Cow says mooooooo!"`

### Example 48

```ruby
class Person
  def initialize(name)
    @name = name
  end
end

class Cat
  def initialize(name, owner)
    @name = name
    @owner = owner
  end
end

sara = Person.new("Sara")
fluffy = Cat.new("Fluffy", sara)
```

\# What are the collaborator objects in the above code snippet, and what makes them collaborator objects?

Collaborator objects are custom objects that are assigned to the state of another object. This way we can form associations between the two objects. Thereby making the methods of the collaborator object available to the other object

In the above code the object referenced by the local variable `sara` created from the `Person` class is stored as a state of the object `fluffy`. In `fluffy` the object `sara` is assigned to the instance variable `@owner` when the object referenced by the local variable `fluffy` is instantiated from the `Cat` class.

Here the object referenced by `sara` is the collaborator object which makes it's behaviours availabe to the object `fluffy`.

### Example 49

\# What methods does this `case` statement use to determine which `when` clause is executed?

```ruby
number = 42

case number
when 1          then 'first'
when 10, 20, 30 then 'second'
when 40..49     then 'third'
end
```

The case statement uses the `===` method explicitly. The calling object is treat as a group and checks if the argument is part of the group.

### Example 50

\# What are the scopes of each of the different variables in the above code?

```ruby
class Person
  TITLES = ['Mr', 'Mrs', 'Ms', 'Dr']

  @@total_people = 0

  def initialize(name)
    @name = name
  end

  def age
    @age
  end
end
```

The constant `TITLES` initialized in the line 2 is available throught the class and its subclasses.  The class variable acts as one copy through out the class and its subclasses. The instance variable `@name` is available only within a instance of a class. Once the instance is destroyed then the instance variable perishes along with it. Instance variables are scoped within the instance of the class. The instance variable `@age` is not initialized and hence it is not available anywhere as always evaluates to `nil`.

### Example 51 - Spike

\# The following is a short description of an application that lets a customer place an order for a meal:

* A meal always has three meal items: a burger, a side, and drink.
* For each meal item, the customer must choose an option.
* The application must compute the total cost of the order.

1. Identify the nouns and verbs we need in order to model our classes and methods.
2.  Create an outline in code (a spike) of the structure of this application.
3. Place methods in the appropriate classes to correspond with various verbs.

```ruby
# The following is a short description of an application that lets a customer place an order for a meal:

# - A meal always has three meal items: a burger, a side, and drink.
# - For each meal item, the customer must choose an option.
# - The application must compute the total cost of the order.

# 1. Identify the nouns and verbs we need in order to model our classes and methods.
# 2. Create an outline in code (a spike) of the structure of this application.
# 3. Place methods in the appropriate classes to correspond with various verbs.

class Order
  attr_reader :customer

  def initialize(customer)
    @customer = customer
  end

  def to_s
    puts "The total cost is £#{customer.order.sum} for the following items:"
    puts customer.items
    ""
  end

end

class Meal
  attr_reader :burger, :side, :drink

  def initialize
    @burger = 4.50
    @side = 1.50
    @drink = 3
  end
end

class Customer
  attr_reader :meal, :order, :items

  def initialize
    @order = []
    @items = []
    @meal = Meal.new
  end

  def items_ordered(item, select)
    if item
      order << select
      items << item
    end
  end

  def choose(burger=nil, side=nil, drink=nil)
    items_ordered(burger, meal.burger)
    items_ordered(side, meal.side)
    items_ordered(drink, meal.drink)
  end
end

bob = Customer.new
bob.choose("burger", "side", "drink")
total = Order.new(bob)
puts total

# The total cost is £9.0 for the following items:
# burger
# side
# drink
```

Another take on the code spike this time with a more detailed implementation

```ruby
# The following is a short description of an application that lets a customer place an order for a meal:

# - A meal always has three meal items: a burger, a side, and drink.
# - For each meal item, the customer must choose an option.
# - The application must compute the total cost of the order.

# 1. Identify the nouns and verbs we need in order to model our classes and methods.
# 2. Create an outline in code (a spike) of the structure of this application.
# 3. Place methods in the appropriate classes to correspond with various verbs.

=begin
  customer has orders
  orders have meal
  meals have cost
=end

module Display
  def display_error
    puts "Invalid selection! Please choose numbers 1, 2 or 3. Try again!"  
  end

  def list(food)
    food.each do |num, item|
      puts "#{num}. #{item.first}: £#{item.last}."
    end
  end
end

class Restaurant
  attr_reader :customer

  def initialize(customer)
    @customer = customer
  end

  def total
    customer.print_selection.map { |food| food.last }.sum
  end

  def final
    puts "#{customer.name} has ordered a meal combo consisting of:"
    customer.print_selection.each { |food| puts "#{food.first} for £#{food.last}." }
    puts "The total amount due is £#{total}."
  end
end

class Customer
  include Display

  attr_accessor :name, :order

  def initialize(name)
    @name = name
    @order = Orders.new
  end

  def prompt(food)
    choice = 0
    loop do
      puts "Please choose one of the option (1, 2, 3)"
      list(food)
      choice = gets.chomp.to_i
      break if [1, 2, 3].include? choice
      display_error
    end

    choice
  end

  def food_selected(food)
    item = food
    choice = prompt(food)
    order.selection << item[choice]
    puts
  end

  def order_food
    food_selected(order.meal.burger)
    food_selected(order.meal.sides)
    food_selected(order.meal.drinks)
  end

  def print_selection
    order.selection
  end
end

class Orders
  attr_reader :meal, :selection

  def initialize
    @meal = Meal.new
    @selection = []
  end
end

class Meal
  attr_reader :burger, :sides, :drinks

  def initialize
    @burger = { 1 => ["Cheese Burger", 6], 2 => ["Chicken Burger", 4], 3 => ["Veggie Burger", 3] }
    @sides = { 1 => ["Onion Rings", 2], 2 => ["Chicken Wings", 3], 3 => ["Potato Wedges", 1] }
    @drinks = { 1 => ["Spring Water", 1], 2 => ["Coca Cola", 1], 3 => ["Fanta", 1] }
  end
end

# bob = Customer.new("Bob")
# grillz = Restaurant.new(bob)
# bob.order_food
# grillz.final

# Please choose one of the option (1, 2, 3)
# 1. Cheese Burger: £6.
# 2. Chicken Burger: £4.
# 3. Veggie Burger: £3.
# 2

# Please choose one of the option (1, 2, 3)
# 1. Onion Rings: £2.
# 2. Chicken Wings: £3.
# 3. Potato Wedges: £1.
# 1

# Please choose one of the option (1, 2, 3)
# 1. Spring Water: £1.
# 2. Coca Cola: £1.
# 3. Fanta: £1.
# 3

# Bob has ordered a meal combo consisting of:
# Chicken Burger for £4.
# Onion Rings for £2.
# Fanta for £1.
# The total amount due is £7.
```

Take 3

```ruby
# The following is a short description of an application that lets a customer place an order for a meal:

# - A meal always has three meal items: a burger, a side, and drink.
# - For each meal item, the customer must choose an option.
# - The application must compute the total cost of the order.

# 1. Identify the nouns and verbs we need in order to model our classes and methods.
# 2. Create an outline in code (a spike) of the structure of this application.
# 3. Place methods in the appropriate classes to correspond with various verbs.

# Nouns - meals, burger, side, drink, customer, application, order, cost
# verbs - compute, chooses

module Display
  def prompt_select
    puts "Please select from one of the following using 1, 2, 3."
  end

  def raise_warning
    puts "Invalid selection!. Please try again (1, 2, or 3)."
  end
end

class Order
  attr_reader :customer_order, :cost

  def initialize
    @customer_order = {}
    @cost = []
  end

  def customer_selection(food)
    customer_order[food[0]] = food[1]
  end

  def total
    customer_order.each do |_, price|
      cost << price.chars.map(&:to_i).sum
    end
    cost.sum
  end

  def amount_due
    puts
    puts "The following was ordered:"
    customer_order.each do |item, cost|
      puts "====> #{item}: #{cost}"
    end
    puts "The amount due now is £#{total}"
  end
end

class Meal
  attr_reader :burger, :side, :drink

  def initialize
    @burger = [["Cheese Burger", "£7"], ["Chicken Burger", "£6"], ["Veggie Burger", "£4"]]
    @side = [["Onion Rings", "£1"], ["Chicken Wings", "£2"], ["Potato Wedges", "£2"]]
    @drink = [["Spring Water", "£1"], ["Fanta", "£1"], ["Sprite", "£1"]]
  end

  def list(food)
    food.each_with_index do |(item, cost), idx|
      puts "#{idx + 1}). #{item}: #{cost}"
    end
    puts
  end

  def display_menu
    puts "Please have a look at out Meal menu."
    list(burger)
    list(side)
    list(drink)
  end
end

class Customer
  include Display

  attr_reader :meal, :order

  def initialize
    @meal = Meal.new
    @order = Order.new
  end

  def choose(food)
    choice = 0
    loop do
      prompt_select
      meal.list(food)
      choice = gets.chomp.to_i
      break if [1, 2, 3].include? choice
      raise_warning
    end

    choice - 1
  end

  def selects_food
    meal.display_menu
    [choose(meal.burger), choose(meal.side), choose(meal.drink)]
  end

  def order_food
    food = [meal.burger, meal.side, meal.drink]
    counter = 0
    selects_food.each_with_index do |num, idx|
      order.customer_selection((food[counter])[num[idx]])
      counter += 1
    end
    order.amount_due
  end
end

=begin
order process
  - customer orders food
    - options provided
    - customer has to choose a type from each meal item
    - customer chooses a burger, side and a drink
  - Order is captured
    - the total cost is computed and the displayed
=end
bob = Customer.new
bob.order_food

# ============ exapected output ============
#Please have a look at out Meal menu.
# 1). Cheese Burger: £7
# 2). Chicken Burger: £6
# 3). Veggie Burger: £4

# 1). Onion Rings: £1
# 2). Chicken Wings: £2
# 3). Potato Wedges: £2

# 1). Spring Water: £1
# 2). Fanta: £1
# 3). Sprite: £1

# Please select from one of the following using 1, 2, 3.
# 1). Cheese Burger: £7
# 2). Chicken Burger: £6
# 3). Veggie Burger: £4

# 2
# Please select from one of the following using 1, 2, 3.
# 1). Onion Rings: £1
# 2). Chicken Wings: £2
# 3). Potato Wedges: £2

# 1
# Please select from one of the following using 1, 2, 3.
# 1). Spring Water: £1
# 2). Fanta: £1
# 3). Sprite: £1

# 2

# The following was ordered:
# ====> Chicken Burger: £6
# ====> Onion Rings: £1
# ====> Spring Water: £1
# The amount due now is £8
```

### Example 52

\# In the `make_one_year_older` method we have used `self`. What is another way we could write this method so we don't have to use the `self` prefix? Which use case would be preferred according to best practices in Ruby, and why?

```ruby
class Cat
  attr_accessor :type, :age

  def initialize(type)
    @type = type
    @age  = 0
  end

  def make_one_year_older
    self.age += 1
  end
end
```

The otherway we can write this method so we dont have to use the `self` prefix is by reassigning the `@age` instance variable directly in `line 10`.

```ruby
def make_one_year_older
  @age += 1
end
```

generally it is a good practice in Ruby to reassign the instance variables using the setter method. This is because the getter/setter methods are much easier to reference if we ever need to retrieve or modify the state of the object as we can make changes in just one place. I we do not want to expose all of the raw data that the instance variable references then we can hide all or part of the data by using the method access controller.

example

```ruby
class Student
  attr_reader :name, :grade
  def initialize(name, grade)
    @name = name
    @grade = grade
  end

  private

  attr_writer :grade
end

bob = Student.new("Bob", 89)
bob.grade
bob.grade = 50
```

Here trying to reassign the `@grade` instance variable raises an error. This is because the `grade` setter method is encapsulated by the `private` method access controller.

### Example 53

\# What is output and why? What does this demonstrate about how methods need to be defined in modules, and why?

```ruby
module Drivable
  def self.drive
  end
end

class Car
  include Drivable
end

bobs_car = Car.new
bobs_car.drive
```

Line 11 will raise an error because the `drive` instance method is nor defined in both the module and the class. Instead a module method `drive` is defined in the method definition from the `line 2 to 3` where the `self` keyword represents the module `Drivable`. In order to overcome this and output the desired results we can define the `drive` instance method without invoking it on the `self` keyword within the `Drivable`.

Example

```ruby
module Drivable
  def drive
  end
end

class Car
  include Drivable
end

bobs_car = Car.new
bobs_car.drive
```

Now no errors are raised when line 11 executes.

### Example 54

```ruby
class House
  attr_reader :price

  def initialize(price)
    @price = price
  end
end

home1 = House.new(100_000)
home2 = House.new(150_000)
puts "Home 1 is cheaper" if home1 < home2 # => Home 1 is cheaper
puts "Home 2 is more expensive" if home2 > home1 # => Home 2 is more expensive
```

\# What module/method could we add to the above code snippet to output the desired output on the last 2 lines, and why?

`home1` and `home2` are two local variable referencinng the objects created from the `House` class on `line 9 and 10`. In line 11 the expression `home1 < home2` raises an error. The above expression can also be written as `home1.<(home2)` this indicates that we are calling the `<` method which is looking to compare two `Integer` objects. Since we are dealing with two customs object Ruby raises an error. This is th same case in line 12 for the expression `home1 > home2` where we use the `>` method instead. Inorder for this issue to be resolved we will have to override these methods by having a custom implementation within our class `House.` This is done as follows

```ruby
class House
  attr_reader :price

  def initialize(price)
    @price = price
  end

  def >(other)
    price > other.price
  end

   def <(other)
    price < other.price
  end
end

home1 = House.new(100_000)
home2 = House.new(150_000)
puts "Home 1 is cheaper" if home1 < home2 # => Home 1 is cheaper
puts "Home 2 is more expensive" if home2 > home1 # => Home 2 is more expensive
```

 In `line 8 - 10` and in `line 12 - 15` we have defined  the methods `<` and `>` which override the original methods and hence we get the desired output.
