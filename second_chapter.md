# Class and Object

## Objective

To learn about the Ruby's built-in Class and Object.

## Steps

### Step 1


```ruby

```

### Step 2



```ruby

```



### Step 3



```ruby


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

