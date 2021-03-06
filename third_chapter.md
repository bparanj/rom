# Hierarchy of Class, Object and Module

## Objective

To learn the hierarchy of Ruby built-in classes, Class, Object and Module.

## Steps

### Step 1

In the previous chapter we experimented with user defined classes. We learned that user defined classes implicitly extend from Object. 

What is the Ruby's built-in Object's class? In other words, Object is an object, so it must be an instance of some class, what is that class? We can ask Ruby:

```ruby
p Object.class
```

This prints : Class

### Step 2

The Ruby's built-in Class itself is an object. We can find out the class used to make instances of Class.

```ruby
p Class.class
```

This prints: Class. This seems to be like the chicken and egg problem. How is **Class** created from Class? But Ruby is consistent.

Whenever you use the language construct **class** to create a Class, Ruby uses Class to create instances. The class can be either user defined or the existing Ruby's built-in classes.

### Step 3

In the previous chapter, we saw that Object was the super-class of any user defined class. What is the super-class of Object?

```ruby
p Object.superclass
```

This prints : BasicObject

### Step 4

What is the super-class of BasicObject?

```ruby
p BasicObject.superclass
```

This prints **nil**. This means **BasicObject** is the root of the hierarchy. The BasicObject is an instance of Class. You can verify it like this:

```ruby
p BasicObject.class
```

### Step 5

What is the super-class of Class?

```ruby
p Class.superclass
```

This prints : Module.

### Step 6

The class Module is an object. What class is it an instance of?

```ruby
p Module.class
```

This prints : Class

### Step 7

How can module be a class? Let's say we have a Vehicle module:

```ruby
module Vehicle
  def wheels
    1000
  end
end

p Vehicle.class
```

This prints : Module. The Module is a class because Ruby defines Module like this:

```ruby
class Module

end 
```

You already know that everything in Ruby is an object.

### Step 8

Instead of doing this:

```ruby
module Vehicle
  def wheels
    100
  end
end

class Car
  include Vehicle
end

c = Car.new
p c.wheels
```

We can do the same thing we did above like this:

```ruby
Vehicle = Module.new do
  def wheels
    100
  end
end

class Car
  include Vehicle
end

c = Car.new
p c.wheels
```

Why would you want to do it the second way? We will discuss the answer in an upcoming chapter.

### Step 9

Let's now compare the methods in Module, Class and Object. Here are the methods in Module.

```ruby
p Module.public_methods(false).sort
```

This prints:

[:allocate, :constants, :nesting, :new, :superclass]

Here is the methods in Class.

```ruby
p Class.public_methods(false).sort
```

This prints:

[:allocate, :constants, :nesting, :new, :superclass]

Here is the methods in Object.

```ruby
p Object.public_methods(false).sort
```

This prints:

[:allocate, :new, :superclass]

So you can see we can create instances of Module, Class and Object. Because they have the method **new()**.

### Step 10

We already know that user defined classes are instances of Class. Instead of doing this:

```ruby
class Car
  def drive
    p 'driving...'
  end
end

c = Car.new
c.drive
```

We can do this:

```ruby
Car = Class.new do
  def drive
    p 'driving...'
  end

end

c = Car.new
c.drive
```

Both versions of the Car examples print 'driving...'. Why would you want to do it the second way? We will discuss the answer in an upcoming chapter.

## Summary

In this chapter you learned the Ruby's built-in class hierarchy. The class hierarchy consists of Class, Object, Module and BasicObject. You also saw how we can create modules and classes by creating them on the fly and adding methods to it.