# Method Scope 

## Learning Goals

- Recognize what scope is
- Recognize local scope

## Introduction

Now that we've talked about methods, we will also discuss another very important
concept -- scopes! Scope defines where in a program a _variable_ is accessible.
A variable is a name that Ruby associates with a particular object. These
objects are locations in memory that hold any data to be used by the program. It
is important to understand scope, not just in Ruby, but in any programming
language. Understanding this concept well can help developers avoid errors, like
_variables_ not being defined and incorrect variable assignments, that can cause
confusion and frustration.

## Recognize What Scope Is

Think of method scope like a hotel room. There are no windows to other rooms
(you cannot see what's going on in other rooms). Inside of this room, we can see
the variables. These variables are "known" and "visible" inside of the room.
Other variables in another room are not known in or from this particular room,
but are known and visible in those other rooms.

Every time there is a method call (let's say that we've invited in some other
unregistered guests), when it enters the room, it's now in a "new" scope. 

Ruby has four types of variable scope: `local`, `global`, `instance` and
`class`. The type of variable that is important to recognize right now are
`local` variables.

## Recognize Local Scope

Things that are inside the "room" are "local" to this method's scope. They are
only visible in this scope. Outside of it, they are unknown. That means the
staff at the hotel will never know we have 7 guests crammed into a 2 bed room!

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

```NameError: undefined local variable or method `local_variable' for
main:Object```

When Ruby executes a program, it evaluates one statement after another. When it
encounters a plain word like `local_variable` then it will check if, within the
current scope, it knows a local variable with the same name. If so, it will use
the value that is associated to this variable. If there’s no local variable with
this name, then it will look for a method. If there’s also no method with this
name it will then raise the error message.

**Note:** In Ruby, both local variable names and method names, are written the
same way -- in plain words.

The Ruby will put a local variable in scope whenever it sees it being assigned
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

## Conclusion

Ruby is a language that has been designed to make programming more approachable.
Variable scope in Ruby translates to functionality in other languages like
JavaScript. Understanding scope will allow you to employ many strategies in
program design that help you toward having a more maintainable and error-free
codebase.

## Resources

[Understanding Scope in Ruby](https://www.sitepoint.com/understanding-scope-in-ruby/)
[Scopes](http://ruby-for-beginners.rubymonstas.org/writing_methods/scopes.html)