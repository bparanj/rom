# Class Methods Demystified

## Objective

To answer the burning question : Where does the class methods live?

## Steps

### Step 1

Let's define an instance method **drive()** in Car class.

```ruby
class Car
  def drive
    p 'driving'
  end
end

p Car.instance_methods(false).sort
```

This prints : [:drive]

There is no surprise here, if we define an instance method, it shows up in the output.

### Step 2

What if we had defined a class method **drive()** instead?

```ruby
class Car
  def self.drive
    p 'driving'
  end
end

p Car.instance_methods(false).sort
```

This prints [] because there is no instance methods in Car. There is class method **drive()**. The question is where does the class methods like **drive()** live?

### Step 3

The class methods live in a ghostclass, eigenclass or metaclass. We can use a special syntax that gives us a reference to the ghost class as follows:

```ruby
class Car
  def self.drive
    p 'driving'
  end
end

eigenclass = class << Car
  self
end

p eigenclass.instance_methods(false).sort
```

This prints : [:drive]

We can see that the ghost class holds the class method we have defined in the Car class. Ruby 1.9 introduced singleton_methods that we can use like this:

```ruby
p Car.singleton_methods
```

This prints [:drive].

### Step 4

To illustrate the point made in the previous step, we can define the class method for Car in it's singleton like this:

```ruby
class Car
end

class << Car
  def drive
    'driving'
  end
end

p Car.drive
```

This is same as this:

```ruby
class Car
  def self.drive
    'driving'
  end
end

p Car.drive
```

And so is this:

```ruby
class Car
  class << self
    def drive
      'driving'
    end
  end
end

p Car.drive
```

The last form of defining a class methods will lead to difficulty in maintenance. Because you cannot determine whether it is an instance method or a class method. This happens when the class methods are way down below its class << self declaration.

### Step 5

What class is this ghost class an instance of? Let's ask Ruby:

```ruby
p eigenclass.class
```

This prints: Class

### Step 6

What is object hierarchy of the ghost class? Let's ask Ruby:

```ruby
p eigenclass.ancestors
```

This prints:

```ruby
[#<Class:Car>, #<Class:Object>, #<Class:BasicObject>, Class, Module, Object, Kernel, BasicObject]
```

In Ruby 1.9 and later, we can also do:

```ruby
p Car.singleton_class.ancestors
```

This shows there is a whole new hierarchy consisting of ghost classes for Car, Object and BasicObject. Compare this to the ancestors of a normal class:

```ruby
p Car.ancestors
```

This prints:

```ruby
[Car, Object, Kernel, BasicObject]
```

Now we don't see any ghosts in this case.

### Step 7

We can go one level up and do a similar experiment.

```ruby
class Object
  def self.drive
    p 'driving'
  end
end

g = class << Object
self
end

p g.ancestors
```

This prints:

```ruby
[#<Class:Object>, #<Class:BasicObject>, Class, Module, Object, Kernel, BasicObject]
```

### Step 8

Let's go one more level up and repeat a similar experiment.

```ruby
g = class << BasicObject
self
end

p g.ancestors
```

This prints:

```ruby
[#<Class:BasicObject>, Class, Module, Object, Kernel, BasicObject]
```

### Step 9

```ruby
class BasicObject
  def self.drive
    p 'driving...'
  end
end

class Car
end

Car.drive
```

This prints: driving

Sub classes can call it's parent's class methods. If you are familiar with ActiveRecord library of Rails, we can do something like this:

```ruby
module ActiveRecord
  class Base
    def self.find
      'finding...'
    end
  end
end

class Car < ActiveRecord::Base
end

Car.find
```

## Summary

In this chapter, we designed experiments to answer the question: Where does the class method live?. 

We found that they live in singleton class and they have their own hierarchy. We also saw that class methods are inherited by the sub classes.