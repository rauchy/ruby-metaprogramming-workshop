
# Ruby Metaprogramming Workshop

                  Omer Rauchwerger
                  omer@rauchy.net

Note: I *may* be completly wrong here.

~~~~

## Part 1 - The Ruby Object Model

* Classes are code
* Classes vs. objects
* something

~~~~

### Classes are code

Before we begin, it is super important that you grok that classes are code. For example:

    class Foo
      puts "Inside Foo!"
    end

    # => Inside Foo!

~~~~

In fact, classes can be reopened at any time:

    class Foo
      puts "Inside Foo!"
    end

    class Foo
      puts "Inside Foo again!"
    end

    # => Inside Foo!
         Inside Foo again!

Or simply:

    3.times do
      class Foo
        puts "OMG"
      end
    end

~~~~

You can also define methods this way:

    class Foo
      def say_hello
        puts "Hello"
      end

      def say_goodbye
        puts "Goodbye"
      end
    end

    foo = Foo.new
    foo.say_hello
    foo.say_goodbye

    # => Hello
         Goodbye

~~~~

If you define a method that's already been defined, you override it

    class String
      def upcase
        downcase # muhaha
      end
    end

    "Hello".upcase

    # => hello

This is called Monkeypatching.

~~~~

### Classes vs. objects

* Objects are instances of classes
* Variables are kept inside objects
* Methods are kept inside classes

    class Foo
      def wake_up!
        @status = "OK OK, I'm up!"
      end
    end

    f = Foo.new
    f.wake_up!

    cd f # use pry for this
    ls

    # => Foo#methods: wake_up
         self.methods: __binding_impl__
         instance variables: @status
         locals: _  _dir_  _ex_  _file_  _in_  _out_  _pry_

Note that wake_up is under Foo#methods and @status is under instance variables.
It kinda makes sense - the only thing that varies between different instances of a class is state.
Methods are always the same, so they are stored in the class. 

~~~~

All objects have an object id and a class:

    "foo".object_id # => 70225091169540
    "foo".class # => String

Here's one to remember: Ruby classes are objects themselves. I'll prove it:

    String.object_id # => 70114959626620
    String.class # => Class

A Class' class is Class and it inherits from Module, which inherits from Object, which inherits from BasicObject, which is the root of all objects.

    Class.object_id # => 70225089471040
    Class.superclass # => Module
    Module.superclass # => Object
    Object.superclass # => BasicObject
    BasicObject.superclass # => nil
