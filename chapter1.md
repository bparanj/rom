# The Current Object, self in Ruby

## Objective

To learn about the current object **self** and the top level context in Ruby.

## Steps

### Step 1

In Ruby, there is always one object that plays the role of current object which is the default receiver. We call it the **self**. Let's see the value of self.


```ruby
puts self
```

This prints: **main**. 

This tells us that Ruby has created an object called **main** for us at the top level. And all the code we write at the top level will use **main** as the receiver in method calls. 

What is top level? You are in top level when you have not entered into a class or module definition or exited from all class or module definitions.

### Step 2

If main is an object, it must be instance of some class. We can ask Ruby to tell us which class main is an instance of:

```ruby
puts self.class
```

This prints **Object**. We now know, Ruby did something like this:

```ruby
main = Object.new
```

This provides us the default receiver **main**.

### Step 3

Let's print hello in the standard output.

```ruby
puts 'hello'
```

As expected, this prints **hello**. 
 
### Step 4

If you use an explicit receiver, the **self** to call the puts:

```ruby
self.puts 'hi'
```

We get:

```ruby
NoMethodError: private method ‘puts’ called for main:Object
```

This is because puts is a private method in Object. In Ruby you cannot have an explicit receiver to call a private method. Why? Because that's the definition of private method in Ruby.

### Step 5

Can we use main Object to call puts?

```ruby
main.puts 'hi'
```

We get:

```ruby
NameError: undefined local variable or method ‘main’ for main:Object
```

Even though Ruby prints **main** as the current object at the top level. There is no such variable called **main**. The **main** is the human visible representation of the current object.

## Summary

In this chapter, 

