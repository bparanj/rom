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

The **Class** is Ruby's built-in class that provides the new method that we can use to instantiate the car object.

```ruby
p Class.public_instance_methods(false).sort
```




 
### Step 4

Let's look at a simple example that we can use to experiment and learn.

```ruby
class Greeting
  def initialize(text)
    @text = text
  end

  def welcome
    @text
  end
end

o = Greeting.new('Hi')
p o.class
```

This prints : 'Greeting'. We know the instance of Greeting, the object 'o' gets created using the Greeting class. We can also get the instance methods, instance variables as follows:


```ruby
p o.class.instance_methods(false)
```

This prints: [:welcome]

```ruby
p o.instance_variables
```

This prints: [:@text]

## Summary

In this chapter, you learned the introspection abilities of Ruby in the context of Ruby Object Model. We were able to query for instance variables, instance methods and ancestors. Why do we need to worry about class hierarchy in Ruby? Because it determines the method look-up in Ruby.

