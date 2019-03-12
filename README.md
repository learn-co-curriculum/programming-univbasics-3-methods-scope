# Method Scope 

## Learning Goals

- Recognize what scope is
- Recognize global scope
- Recognize local scope
- Recognize scopes overlap

## Introduction

Now that we've talked about methods, we will also discuss another very important
concept -- scopes! Scope defines where in a program a _variable_ is accessible.
A variable is a name that Ruby associates with a particular value: For example
`dog = "Poodle"` or `age = 32`. These variables hold any information we want
to save and reuse. Understanding this concept well can help developers avoid
errors and debug _extremely_ sneaky bugs.

## Recognize What Scope Is

Say you go to a Mexican restaurant for tacos for lunch. You go in and sit down.
A waiter comes along, takes your order and disappears. You wait...

And wait...

And wait...

You decide to flag down the waitstaff and ask, "Hey, I've been waiting a really
long time, do you know where my order is?"

Within the context of it being lunch time in this taco restaurant, and that you
have created a relationship with the waiter, the waitstaff knows that "order for
person at table #12" should be in their notepad, or should be in the kitchen.
Your order is like a variable and has meaning in that context. "Order for table #12"
is a variable that "points to" your delicious tacos.

Say you walked over to a store across the street and asked "Do you know where
order for table #12 is?" In that context your variable doesn't make sense.
They don't know about taco orders, they don't know about tables, and they
certainly don't know about your recent order of tacos.

In real life we have a sense of "scope" is something we're familiar with. But in
code scope functions much the same way.

## Recognize Global Scope

When we assign a variable, we're defining it in the global scope. Global
variables in Ruby are accessible from anywhere in the Ruby program. Even inside
of a method we can access variables in that scope.

Global variable names are start with a dollar sign ($). For example:
`$global_variable` or `$GLOBAL_VARIABLE`.

Global variables may sound preferable to use since they are available
everywhere, however, this is a strongly discouraged pattern in Ruby programming.
Global variables make programs unpredictable. It's harder to track where changes
are happening.

On top of that confusion, if you have a big program, you'll likely run into
naming issues. If the names are not unique enough, there will be conflicts, and
you'll have to keep track of all of those global variables.

There are a few special global variables that can be used, but for the most
part, they aren't used. You won't really need to know all that much about global
variables to understand most Ruby programs, but you should at least know that
they're there.

Now that' we've seen globally scoped variables are accessible in methods, is the
reverse true? It is not. Variables defined in local scopes cannot be accessed in
global scopes.

## Recognize Local Scope

Things like a taco order in a taco restaurant are "local" to that context, and a
local variable is "local" to that method's scope. It is only visible in this
scope. Outside of it, it is unknown.

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
encounters a plain word like `local_variable` then it will check if, within the
current scope, it knows a local variable with the same name. If so, it will use
the value that is associated to this variable. If there’s no local variable with
this name, then it will look for a method. If there’s also no method with this
name it will then raise the error message.

**Note:** In Ruby, both local variable names and method names, are written the
same way -- in plain words.

Ruby will put a local variable in scope whenever it sees it being assigned
to something. It doesn’t matter if the code is not executed, the moment the
interpreter sees an assignment a local variable, it puts it in scope. Here, we
will properly define `local_variable`:

```ruby
def my_ruby_method 
  local_variable = 'Hello World!'
  puts local_variable
end
# => Hello World!
```

Now if you run this code in IRB, you will see the the out**put** "Hello World!".

## Recognize Scopes Overlap

Every time we create a new method, you create a new scope. It’s like Ruby is
opening a gate for you and taking you to an entirely different context with
entirely different variables.

!["Universal Studios Hollywood"](https://www.universalstudioshollywood.com/wp-content/themes/ush_theme/assets/images/USH_Map_2018_Final.jpg)

If you've ever spent any time in a amusement park, you likely experienced coming
into a what felt like a "whole new world" each time you enter a new section of
the park. "The Wizarding World of Harry Potter" looks very different from
Springfield U.S.A., home of "The Simpsons", and there are completely different
rides and attractions.

However, scopes overlap. When we go to a taco restaurant, a pet grooming store,
or into an amusement park with different sections, we don't stop being a human.
In any of these locations, anyone working there still knows we're human. Scopes,
or contexts, "overlap." Something that is defined in a "higher" scope is visible
in a "lower" scope. A method is defined inside inside of a class. Any method is
considered a lower scope than the class, like an amusement park with many
sections, or a shopping mall with many restaurants and shops inside.

## Conclusion

Understanding scope will allows us to employ many strategies in program design
that help you toward having a more maintainable and error-free codebase in Ruby
and even in other languages like JavaScript! Remember that scope is about
context; in the local context, only that method will know about those variables.
In the global context, as the name implies, the variables are accessible to the
whole application. With this base knowledge, learning and applying other
variables scopes will seem familiar to you.

## Resources

[Understanding Scope in Ruby](https://www.sitepoint.com/understanding-scope-in-ruby/)
[Scopes](http://ruby-for-beginners.rubymonstas.org/writing_methods/scopes.html)
[Global Variables in Ruby](https://www.thoughtco.com/global-variables-2908384)