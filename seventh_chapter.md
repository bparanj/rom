# Develop Sinatra Clone

## Objective

To apply the basics we learned in the Ruby Object Model article series to develop a Sinatra clone called Chico.

## Steps

### Step 1

```ruby
get '/' do
  'hi'
end
```

If you run this program, you get:

```ruby
NoMethodError: undefined method ‘get’ for main:Object
```

### Step 2

We can open the Object class and define the **get()** method:

```ruby
class Object
  def get(path)
    yield
  end
end

get '/' do
  p 'hi'
end
```

This prints: 

```ruby
hi
```

#### Problems

* The **get()** method is invoked immediately.
* Opening the Object class to add the get method makes it available everywhere.

In Sinatra apps, the get() method gets called only when a request is made to that specific URI. We don't want to pollute the Object with our library methods.

### Step 3

How to mixin a method to top level?

```ruby
module Kernel

  def get(path)
    yield
  end
end

get('/') do
  p 'hi'
end
```

This prints: 

```ruby
hi
```

Mixing it to the Kernel also makes the get() method available at the top level and the method gets invoked immediately. We can make the **get()** method private, like the puts method we encountered in the previous chapters.

```ruby
module Kernel

  private

  def get(path)
    yield
  end
end

get('/') do
  p 'hi'
end
```

But, it will not solve any of our problems.

### Step 4

Let's write a minimal Sinatra application. Create mine.rb:

```ruby
require 'sinatra'
```

You can run it like this:

```ruby
$ruby mine.rb
```

You can see that the server runs on port 4567. You can stop the server by pressing Ctrl+C.

### Step 5

How can we accomplish the same? If you read the source code for Sinatra, you will see that it uses:

```ruby
at_exit
```

hook. Let's use the at_exit hook:

```ruby
at_exit do 
  p 'Chico has taken the stage' 
  begin
    puts "Press Ctrl-C to quit the server"
    loop {}
  rescue Interrupt => e
    puts "Yay! The crowd applauds."
  end
end
```

Another way to interrupt the Ctrl-C:

```ruby
Signal.trap('SIGNINT') do

end 
```

The current implementation for loop method does not do anything. We need to listen for incoming requests and call the corresponding methods defined by the developer. We will discuss it in upcoming chapters.

Summary
In this article, we applied the Ruby Object Model basics to develop a Sinatra Clone.