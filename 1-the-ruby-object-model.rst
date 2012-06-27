
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
