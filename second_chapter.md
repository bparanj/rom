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

```




```ruby

```



```ruby

```



## Summary

In this chapter, you learned the introspection abilities of Ruby 

