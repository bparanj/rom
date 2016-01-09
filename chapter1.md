# The Method Lookup in Ruby

## Objective

To learn about the introspection abilities of Ruby and the method look-up.


# Steps

## Step 1

We already know that class Object is the super class of any user defined class. Let's define a greet method by opening the Ruby's built-in Object class.

```ruby
class Object
  def greet
    puts 'hi'
  end  
end
```

## Step 2

Let's create a class and call the method greet on it.

```ruby
class Greeter

end

g = Greeter.new
g.greet
```

This prints : 'hi'. The variable 'g' has an instance of Greeter class. When we call the greet() method, the value of self changes to the Greeter object 'g'.  

Then Ruby looks for the greet() method in the Greeter class. It does not find it there. It goes to the super-class of Greeter which is the Object. The greet() method is in Object class, it calls that method.











