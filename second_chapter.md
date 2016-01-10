# Class and Object

## Objective

To learn about the Ruby's built-in Class and Object.

## Steps

### Step 1

Let's take a look at user defined classes.

```ruby
class Car 
  def drive
    puts 'driving...'
  end
end

c = Car.new
c.drive
```

This prints: 'driving...'.

We created an instance of our car class and called the drive method.

### Step 2

Everything in Ruby is an object. Even the class Car we defined is an object. If that is the case then the Car class must be an instance of some class. What is that class?

```ruby
class Car

end

p Car.class
```

This prints **Class**. The Car class is an instance of a class called **Class**.

### Step 3

The **Class** is Ruby's built-in class that provides the **new()** method that we can use to instantiate the car object.

```ruby
p Class.public_instance_methods(false).sort
```

This prints [:allocate, :new, :superclass]. As a developer you will not call **allocate()** method. You will use the **new()** and **superclass()** methods.
 
### Step 4

When you use the Ruby language keyword **class**, Ruby does something like this:

```ruby
Car = Class.new 
```

Let's print the class of Car.

```ruby
p Car.class
```

This prints **Class**. Since Car is an object you can call the instance method **new** like this:

```ruby
car = Car.new
```

As shown earlier in step 1. Because **new** is an instance method provided by Ruby's built-in class called **Class**.

### Step 5

Let's create a subclass:

```ruby
class Beetle < Car

end

p Beetle.class
```

This prints **Class**. Our new Beetle class also an instance of class **Class**. It gets the methods such as new(), superclass() and allocate() from **Class**.

### Step 6

What is the superclass of Beetle?

```ruby
p Beetle.superclass
```

This prints **Car**. This is obvious since we defined Beetle to be subclass of Car. 

### Step 7

How about the Car class?

```ruby
p Car.superclass
```

This prints : Object. The class **Object** is Ruby's built-in class. It comes into picture when you consider the inheritance hierarchy.

### Step 8

This is implicit. There is no need to explicitly provide the super class:

```ruby
class Car < Object

end

p Car.class
```

### Step 9

In the previous chapter, we saw the value of self.class is Object. We can also do this:

```ruby
class Car < self.class

end

p Car.superclass
```

This prints **Object**.

Step 10
This makes the following code run just fine.

class Car < self.class
  def drive
    puts 'driving...'
  end
end

c = Car.new
c.drive
There is no need to explicitly specify the superclass in this case. But, that's what is going on behind the scenes.

Summary
In this article, we explored how everything is an object in Ruby. All objects are instances of the Ruby's built-in class called Class. The Ruby built-in Object comes into play in the inheritance hierarchy.
```ruby

```




```ruby

```



```ruby

```



## Summary

In this chapter, you learned the introspection abilities of Ruby 

