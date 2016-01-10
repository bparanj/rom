# Singleton Methods Demystified

## Objective

To learn about singleton methods and class methods and how they relate to each other.

## Steps

### Step 1

Let's define a class method drive in Car class. How can we ask Ruby for the class methods defined in Car class? We cannot do: 

```ruby
Car.class_methods
```

We will get NoMethodError.

```ruby
class Car
  def self.drive
    p 'driving'
  end
end

p Car.singleton_methods
```

This prints : 

```ruby
[:drive]
```

We can call the class method like this:

```ruby
Car.drive
```

To view the Class method **drive()** as a singleton method, we need to shift the perspective. Shift the perspective from Car class to Car as an instance of Class. We can define the drive class method like this:

```ruby
Car = Class.new

class << Car
  def drive
    p 'driving'  
  end
end

Car.drive
```

This also prints 'driving'. We now see that Car is an instance of class **Class** so it is a singleton method from that perspective. This accomplishes the same thing as this example:

```ruby
Car = Class.new

def Car.drive
  p 'driving'  
end

Car.drive
```

### Step 2

We can also define a class method by defining a method inside the singleton class like this:

```ruby
class Car
  class << self
    def drive
      p 'driving'
    end
  end
end

p Car.singleton_methods
```

This prints: 

```ruby
[:drive]
```

The effect is the same as step 1, we can still call the **drive()** method like this:

```ruby
Car.drive
```

### Step 3

Let's define a singleton method called drive for an instance of Car class like this:

```ruby
class Car

end

c = Car.new

def c.drive
  'driving'
end

p c.singleton_methods
```

This prints: 

```ruby
[:drive]
```

We can call the singleton method drive like this:

```ruby
p c.drive
```

This prints: 

```ruby
driving
```

Since this is a singleton method, the **drive()** method is not available for other instances of Car. This implies that we cannot do this:

```ruby
b = Car.new
b.drive
```

We get the error: 

```ruby
NoMethodError: undefined method ‘drive’ for Car.
```

### Step 4

We can do what we did in previous step like this:

```ruby
class Car

end

c = Car.new

class << c
  def drive
    'driving'
  end
end

p c.drive
```

This prints: 

```ruby
driving
```

Let's look at the singleton methods for Car class.

```ruby
p c.singleton_methods
```

This prints: 

```ruby
[:drive]
```

This step is the same as the previous step. They both illustrate different ways to define a method in the singleton class.

### Step 5

An alternative to defining a singleton method using:

```ruby
class << obj
```

construct is to mixin the method from a module. Here is an example:

```ruby
module Driveable
  def drive
    'driving'
  end
end

class Car
end

c = Car.new

class << c
  include Driveable
end

p c.drive
```

This prints driving.

```ruby
p c.singleton_methods
```

This prints [:drive]. This does the same thing we did in the previous step.

### Step 6

Let's now combine all the different ways we have seen so far:

* Defining a class method in a Class.
* Defining a singleton method for a specific car object.
* Using mixin to define a singleton method.

into one grand example:

```ruby
module Stoppable
  def stop
    'stopping'    
  end
end

class Car
  def self.start
    'starting'
  end
end

c = Car.new

def c.fly
  'flying'
end

class << c
  include Stoppable

  def drive
    'driving'
  end
end

p Car.singleton_methods
```

This prints [:start]

```ruby
p c.singleton_methods
```

This prints: 

```ruby
[:fly, :drive, :stop]
```

We can exclude methods that is included in the module, by passing false flag to the **singleton_methods()** like this:

```ruby
p c.singleton_methods(false)
```

This prints:

```ruby
[:fly, :drive]
```

These statements:

```ruby
p Car.start
p c.drive
p c.stop
p c.fly
```

print:

```ruby
starting
driving
stopping
flying
```

The first call is a class method call and the other three are singleton method calls.

### Step 7

We can also ask Ruby for the singleton_class of a Class like this:

```ruby
class Car
end

p Car.singleton_class
```

This prints: 

```ruby
#Class:Car
```

### Step 8

Let's look at a simple example for displaying the name of the singleton_class:

```ruby
class Car
  class << self
    def class_name
      to_s
    end
  end
end

p Car.class_name
```

This prints: 

```ruby
Car
```

We can also use **define_singleton_method()** to dynamically define singleton method. Here is an example that defines **to_s** singleton method in Car class:

```ruby
class Car

end

Car.define_singleton_method(:class_name) do
  to_s
end

p Car.class_name
```

This still prints:

```ruby
Car
```

Let's combine these two above examples into one example:

```ruby
class Car
  class << self
    def class_name
      to_s
    end
  end
end

Car.define_singleton_method(:whoami) do
  "I am : #{class_name}"
end

p Car.whoami
```

This prints: 

```ruby
I am : Car
```

### Step 9

As a last example, let's define a singleton_method on a string class.

```ruby
car = 'Beetle'
car.define_singleton_method(:drive) { "You are driving : #{self}"}
p car.drive
```

This prints: 

```ruby
You are driving : Beetle
```

Let's check the singleton methods for this specific string object.

```ruby
p car.singleton_methods
```

This prints [:drive].

## Summary

In this chapter, we saw different ways to define class methods and singleton methods and where they live.