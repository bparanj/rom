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

### Step 6

You might be curious: How do we grab the top level default object (**main**)? Let's grab the value of the current object from the **self** and assign it to our own variable **m**.

```ruby
m = self

m.puts 'hi'
```

We get the same error message as we did in step 4.

```ruby
NoMethodError: private method ‘puts’ called for main:Object
```

We cannot call the puts private method with an explicit receiver. This is like doing:

```ruby
class Car

  private

  def change_gear
    'changing gear'
  end
end

c = Car.new
c.change_gear
```

This will give you the following error.

```sh
NoMethodError: private method ‘change_gear’ called for #<Car:0x007>
```

### Step 7

We can use **send()** method to send the **puts()** message to the **main** object:

```ruby
m = self

m.send(:puts,'hi')
will work and is the same as:

self.send(:puts,'hi')
```

This breaks encapsulation and is generally not a good idea unless you have a good reason to do so.

#### Lesson Learned

The self takes the value of an instance of Object, this is **main**. The value of self is implicit, you cannot explicitly provide a receiver to call private methods. For instance, you must call the **puts()** without a receiver at the top level.

### Step 8

In the Ruby documentation, puts is an instance method in IO class.

```ruby
io = IO.new(1)
io.puts 'hello'
```

The IO constructor argument 1 here indicates standard output. This prints **hello** to standard output which is the terminal.

### Step 9

It's the same as doing:

```ruby
$stdout.puts 'hello'
```

Here the **$stdout** is the global variable for standard output. How come we were able to provide an explicit receiver in this case?

### Step 10

Let's ask Ruby for the public instance methods of IO class.

```ruby
puts IO.public_instance_methods(false).grep(/put/)
```

The result shows that the puts is a public method:

```sh
putc
puts
```

In this case we are not calling a private method in Object class but we are calling the public method **puts** in **IO class**. By the way, the false argument to the method filters out the methods from it's super-class.

## Summary

In this chapter we briefly saw how everything is an object in Ruby and the role of **self** in a Ruby program. 

Answer the following questions either by creating an experiment or from your understanding.

1. What is self?
2. Why we cannot use an explicit receiver to call puts at the top level?
3. Where is puts defined if you are calling from top level?
4. How is puts available at the top level without a receiver?
5. How to grab the top level default object?

If you can answer these questions, you are on your way to mastering the Ruby Object Model.