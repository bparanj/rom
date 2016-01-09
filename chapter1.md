# The Current Object, 'self' in Ruby

## Objective

To learn about the introspection abilities of Ruby and the method look-up.

## Steps

### Step 1

We already know that class Object is the super class of any user defined class. Let's define a greet method by opening the Ruby's built-in Object class.

```ruby
class Object
  def greet
    puts 'hi'
  end  
end
```

### Step 2

Let's create a class and call the method greet on it.

```ruby
class Greeter

end

g = Greeter.new
g.greet
```

This prints : 'hi'. The variable 'g' has an instance of Greeter class. When we call the greet() method, the value of self changes to the Greeter object 'g'.  

Then Ruby looks for the greet() method in the Greeter class. It does not find it there. It goes to the super-class of Greeter which is the Ruby's built-in Object class. The greet() method is in Object class, it calls that method.

### Step 3

We can ask ruby for its method look up path like this:

```ruby
class Object
  def greet
    p 'hi'
  end
end

class Greeter

end

p Greeter.ancestors
```

This prints : [Greeter, Object, Kernel, BasicObject]. 

The order in which the classes appear in the array represents the order in which Ruby looks for the methods. The sequence is as shown below:

1. Greeter Class
2. Object Class
3. Kernel Module
4. BasicObject Class

 
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

