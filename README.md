# Method Scope 

## Learning Goals

- Recognize what scope is
- Recognize global scope
- Recognize local scope
- Recognize scopes overlap

## Introduction

Now that we've talked about methods, we will discuss another very important
concept: scopes!

"Scope" defines where in a program a _variable_ is accessible or "visible."  A
"variable is a name that Ruby associates with data. For example, `dog =
""Poodle"` or `age = 32`. Variables hold the information we want to save and
"reuse.

But sometimes you can't access variables. They're said to be "invisible" or
"inaccessible" outside of a certain "scope." Scope is particularly important
as we start writing methods because parameters are visible only within the
`def...end` boundaries that "bound" the method's definition.

```ruby
# "why" can't be used here
def sing(why="for my laughter")
# "why" can't be used here
  puts "Sing #{why}"
end
# "why" can't be used here
sing
sing("for my tears")
```

We need to understand why and how variables
are "scoped." Understanding this concept well helps developers avoid errors and
debug _extremely_ sneaky bugs.

## Recognize What Scope Is

Say you go to a Mexican restaurant and order tacos for lunch. You go in and sit
down. A waiter comes along, takes your order and disappears. You wait...

And wait...

And wait...

After waiting too long, you decide to flag down the waiter and ask, "Hey,
I've been waiting for a long time. Do you know where my order is?"

Your question exists in a "scope". The "scope" is defined by a few facts
like:

* It's lunchtime...
* You're eating in this particular Mexican restaurant
* _and_ that you have created a relationship with the waiter when they took your order

The waiter knows that the data associated with the variable `your_order` should
be recorded in their notepad. They immediately know to look in the kitchen
to see if your tacos are sitting out, getting cold.

The idea of `your_order` is like a variable and has meaning in the context or "scope" of this
particular restaurant and this particular time. 

Say you walked over to a dry cleaner across the street and asked: "Do you know where
the order for table #12 is?" In that _context_ the `your_order` variable doesn't
make sense.  Or what if you walked into the restaurant two weeks later and asked about
`your_order`. The waiter would be confused. Restaurant orders are
"scoped" or "exist in a context of" a time and place.

So, in real life, we have a sense of "scope." Code scope functions similarly.

## Recognize Global Scope

When we assign a variable, outside of a method, we're defining it in the
**global** scope. So-called **global variables** in Ruby are accessible from
anywhere in the Ruby program. Even inside of a method we can access variables
in that scope.

Global variable names start with a dollar sign (`$`). For example:
`$global_variable`.

Global variables may sound preferable to use since they are available
everywhere; however, this is strongly discouraged in all programming
languages. Global variables make programs unpredictable. It's harder to track
where changes are happening. If we create a too-broadly-scoped variable like `$data`
and change it in many places through the operations of multiple
methods, it's really hard to debug what's going on.

On top of that confusion, if you have a big program you'll likely run into
naming issues. If the variable names are not unique enough, there will be conflicts, and
we'll have to keep track of all of those global variables. We like to keep
the scope as small as possible. It's a lot like keycards in a hotel: every person
should have the keycard to the room they've rented for the night; cleaning
staff should have keycards that work on the floors to which they're assigned;
and the manager and emergency services staff should be the _only_ people with a
"global access" keycard.

Now we've seen that globally-scoped variables are accessible in methods.
The reverse is not true. Variables defined in **local** scopes cannot be
accessed in other scopes **or** the global scope.

## Recognize Local Scope

Things like a taco order in a Mexican restaurant are "local" to that context.

In
the same way, a

* local variable in a method or
* a _parameter_ for a method is "local" to its containing method's scope.

It's worth repeating: ***all parameters in a method are locally scoped
to their defining method***.

Here's our example code again:

```ruby
# "why" can't be used here
def sing(why="for my laughter")
# "why" CAN be used here
  puts "Sing #{why}"
end
# "why" can't be used here
sing
sing("for my tears")
```

It is only visible in this scope. Outside of it, it is unknown.

In Ruby, local variables begin with a lowercase letter or `_`. They can look
like a simple `word` or `snake_cased` phrase. A local variable declared in a
method cannot be accessed outside of that method.

```ruby
def my_ruby_method
  puts local_variable
end
```

If you paste this code into IRB and call `my_ruby_method`, you'll get an error.
When you call a variable that has not yet been defined, you will see an error:

```ruby
NameError: undefined local variable or method `local_variable' for
main:Object
```

When Ruby executes a program, it evaluates one statement after another. When it
encounters a word like `local_variable` then it will check if, within the
current scope, it knows a local variable with the same name. If so, it will use
the value that is associated with this variable. If there’s no local variable with
this name, then it will look for a method. If there’s _also_ no method or global
variable with this name, Ruby will then raise the error message.

Here, we define `local_variable` and use it:

```ruby
def my_ruby_method 
  local_variable = 'Hello World!'
  puts local_variable
end
my_ruby_method # => Hello World!
```

Now if you run this code in IRB, you will see the output "Hello World!".


## Recognize Scopes Overlap

Every time we create a new method, you create a new scope. It’s like Ruby is
opening a gate for you and taking you to an entirely different context with
entirely different variables.

!["Universal Studios Hollywood"](https://www.universalstudioshollywood.com/wp-content/themes/ush_theme/assets/images/USH_Map_2018_Final.jpg)

If you've ever spent any time in an amusement park, you likely experienced coming
into a what felt like a "whole new world" each time you enter a new section of
the park. "The Wizarding World of Harry Potter" looks very different from
Springfield U.S.A., home of "The Simpsons," and there are completely different
rides and attractions.

However, scopes overlap. When we go to a taco restaurant, a pet grooming store,
or into an amusement park with different sections, we don't stop being a human.
In any of these locations, anyone working there still knows we're human. Scopes,
or contexts, "overlap." Something that is defined in a "higher" scope is visible
in a "lower" scope. The reverse, sensibly, is not true.

In code we can represent this idea like:

```ruby
$species = "human"

def visit_universal(name)
  visit_wizarding_world(name)
  visit_springfield_usa(name)
end

def visit_wizarding_world(name)
  simple_name = "Hogwart's"
  puts "#{name}, a #{$species}, visits #{simple_name}"
end

def visit_springfield_usa(name)
  simple_name = "the home of 'The Simpsons'"
  puts "#{name}, a #{$species}, visits #{simple_name}"
end

visit_universal("Byron")

# Prints...
# Byron, a human, visits Hogwart's
# Byron, a human, visits the home of 'The Simpsons'
```

The variable `$human`, a globally-scoped variable, "casts its shadow" into all
the local scopes created by method definitions. But the locally-scoped
variables' information cannot be gotten outside of those variables' defining
context.

## Conclusion

Understanding scope allows us to employ many strategies in program design
that help you toward having more maintainable code.

Remember that scope is about
context; in the local context, only that context will know about those variables.
In the global context, as the name implies, the variables are accessible to the
whole application.

## Resources

[Understanding Scope in Ruby](https://www.sitepoint.com/understanding-scope-in-ruby/)
[Scopes](http://ruby-for-beginners.rubymonstas.org/writing_methods/scopes.html)
[Global Variables in Ruby](https://www.thoughtco.com/global-variables-2908384)
