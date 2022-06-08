# Common Data Types

## Learning Goals

- Learn common data types in Python by comparing to equivalent data types in
  JavaScript: strings, numbers, nil, booleans, arrays, and hashes

## Introduction

Just like in JavaScript, Python has several common built-in data types for
representing different kinds of information in our applications. In this lesson,
we'll explore these different data types and see the similarities and
differences to how Python and JavaScript treat these data types.

Make sure to follow along with the examples in this lesson in the Python shell! As an
object-oriented language, Python gives you a lot of tools to inspect different
data types, so you'll learn more by getting your hands on the code.

## Strings

Like JavaScript, Python lets you define strings with either single quotes or
double quotes:

```py
"I'm a string"
'Me too!'
```

You can also create a new string by using the `String` class constructor method
(though it's not common you'd need to):

```py
String.new("I'm a string")
```

If you want use string interpolation in Python, use double quotes like so:

```py
# Python
dog_name = "Lucy"
puts "Say hello to my dog #{dog_name}"
```

This would be the equivalent of the following JavaScript code:

```js
// JavaScript
const dogName = "Lucy";
console.log(`Say hello to my dog ${dogName}`);
```

Backticks in Python are used for [another purpose][executing terminal commands],
so **don't use backticks for strings in Python**.

[executing terminal commands]: https://www.bigbinary.com/blog/backtick-system-exec-in-ruby

To see some more things you can do with strings in Python, open up the Python shell and run the
following:

```py
"hello"
# => "hello"
"hello".upcase
# => "HELLO"
"HELLO".downcase
# => "hello"
"hello".capitalize
# => "Hello"
"hello".reverse
# => "olleh"
"hello" + "world"
# => "helloworld"
"hello" * 3
# => "hellohellohello"
```

You'll often hear it said that **"in Python, everything is an object"**. All of
the methods that we called on strings above are available because the string
literal "hello" is an **instance** of the `String` class. Thanks to Python's
[introspection][] features, you can see for yourself:

```py
"hello".class
# => String
```

[introspection]: https://www.leighhalliday.com/ruby-introspection-metaprogramming

Calling the `methods` method on any Python object will display a list of all the
methods that object responds to (you'll see `:upcase`, `:downcase`, `:reverse`
and more in that list):

```py
"hello".methods
# => [:unicode_normalize, :unicode_normalize!, :ascii_only?, :to_r, :encode, :encode!, ...
```

> You can even see a few additional methods that aren't part of the String class
> when you call `methods` on a string. Those additional methods are available
> because the String class inherits from other more primitive Python classes,
> including `BasicObject`. You can see this by running `String.ancestors`, which
> will return an array of all the parent classes the `String` class inherits
> from! We'll cover inheritance in more depth in the section on Object Oriented
> Programming.

You can learn more about the many String methods by reading the
[Ruby documentation][string docs] on Strings.

[string docs]: http://ruby-doc.org/core-2.7.3/String.html

## A Note on Notation

In Python, there are two different kinds of methods: **instance methods** and
**class methods**. You won't encounter class methods until the section on
object-oriented programming, but technically all the methods we're writing now
are instance methods. An instance method means a method that's called on an
_instance_ (one unique object) of a class.

In Python, we use the `#` at the beginning of a method when referring to it in
documentation to indicate that it's an instance method, and the `.` at the
beginning to indicate class methods:

- `#`: instance method
- `.`: class method

For example, these two variables refer to _instances_ of the `String` class:

```py
str1 = "hello"
str2 = "there"
```

We can call the _instance method_ `#upcase` on both of these strings because
they are both members of the String class, and share all the methods defined on
that class.

You'll see this syntax used often in our lessons and in the Python documentation,
so just know:

- When a method starts with a `#` in documentation, it's an instance method
- When a method starts with a `.` in documentation, it's a class method

## Numbers

In Python, unlike JavaScript, there are two types of numbers: Integers and Floats.

**Integers** are whole numbers, like `7`.

**Floats** are decimal numbers, like `7.3`.

There are a number of methods available to you for operating on or manipulating
integers. You can read more about [Integers here][integer docs] and more about
[Floats here][float docs]. For now, we'll just check out a few examples:

[integer docs]: http://ruby-doc.org/core-2.7.3/Integer.html
[float docs]: http://ruby-doc.org/core-2.7.3/Float.html

```ruby
7.5.floor
# => 7
7.5.ceil
# => 8
10.next
# => 11
```

You can convert some other data types to integers or floats with the `#to_i` and
`#to_f` methods:

```py
"1".to_i
# => 1
"1.1".to_i
# => 1
"1.1".to_f
# => 1.1
```

Unlike JavaScript, Python won't convert an Integer to a Float when performing math
operations, unless one side of the operation is already a Float:

```py
4 / 3
# => 1
4 / 3.0
# => 1.3333333333333333
4 / 3.to_f
# => 1.3333333333333333
```

## Nil

In Python, there is one special value that represents the **absence** of a value,
`nil`. You've already seen `nil` as the return value of the `#puts` method:

```py
puts "I return nil"
# I return nil
# => nil
```

In JavaScript, there are two different data types for representing the absence
of value: `null` and `undefined`:

```js
let noValue;
console.log(noValue);
// => undefined
noValue = null;
console.log(noValue);
// => null
```

`undefined` in JavaScript generally comes up in a few places: when a variable
has been created, but hasn't been assigned a value, and when a function doesn't
have any return value. `null`, on the other hand, is used to explicitly signify
the absence of any value.

Unlike JavaScript, Python won't let you create a variable without assigning a value.
You must explicitly assign a value of `nil` if you want an "empty" variable:

```py
no_value
# NameError (undefined local variable or method `no_value' for main:Object)
no_value = nil
# => nil
```

## Booleans

There are only two values of the Boolean data type: `true` and `false`. In Python,
however, there is no such thing as a Boolean class. Instead, every appearance,
or instance, of `true` and `false` in your program are instances of `TrueClass`
and `FalseClass` respectively:

```py
true.class
# => TrueClass
false.class
# => FalseClass
```

Python, like JavaScript, has the concept of "truthy" and "falsy" values as well:
values which, when coerced to their equivalent boolean value, or evaluated as
part of a conditional statement, return either true or false:

```py
!!true
# => true
!!false
# => false
!!1
# => true
!!0
# => true
!!""
# => true
!!nil
# false
```

In Python, **only `nil` and `false` are falsy values**. Everything else is truthy,
even 0 and empty strings.

Contrast this with JavaScript, where `null`, `undefined`, `false`, `0`, `NaN`,
and `""` are all falsy values:

```js
!!null;
// => false
!!undefined;
// => false
!!false;
// => false
!!0;
// => false
!!NaN;
// => false
!!"";
// => false
```

## Symbols

A symbol is a representation of a piece of data. Symbols look like this
`:my_symbol`. You write symbols by placing a `:` in front of the symbol name:

```py
:this_is_a_symbol
```

If you make a symbol, `:my_symbol`, and then use that symbol later on in your
code, your program will refer to the same area of memory in both cases. This is
different from, for example, strings, which take up new areas of memory every
time they are used:

```py
:my_symbol.object_id
# => 2061148
:my_symbol.object_id
# => 2061148
"my string".object_id
# => 200
"my string".object_id
# => 220
```

The `#object_id` method returns an internal identifier used by Python representing
the object's identity; we can see from the code above that the same symbol
always returns the same `object_id` while the same string does not. That means
they’re referencing different objects in memory, since Python allocates new memory
for each string.

While JavaScript also has a Symbol data type, you'll find that symbols are used
much more frequently in Python than they are in JavaScript. One use case for
symbols that we'll see shortly is as keys on a hash (the Python equivalent of a
JavaScript object).

## Arrays

Python, like JavaScript, has an Array class for storing ordered lists of data. You
can store any type of data in an array.

There are a number of ways to create an array. Just like with creating strings,
you can use the literal constructor or the class constructor.

`[1, 3, 400, 7]` is an array of integers. Any set of comma separated data
enclosed in brackets is an array. So, by simply writing something like the
above, you can create an array:

```py
[1, 3, 400, 7]
# => [1, 3, 400, 7]
```

You can also create an array with the [`Array.new` syntax][array docs]. Just
typing `Array.new` will create an empty array (`[]`):

```py
Array.new
# => []
```

There are many ways to operate on arrays and on each individual item, or
element, within an array. Later on in the course, we'll learn about methods for
iterating over arrays (as with the `.forEach`, `.map`, etc methods in
JavaScript). For now, we'll preview a few array methods, and you can check out
more [here][array docs].

```py
[1, 3, 400, 7].length
# => 4
[5, 100, 234, 7, 2].sort
# => [2, 5, 7, 100, 234]
[1, 2, 3].reverse
# => [3, 2, 1]
```

[array docs]: http://Python-doc.org/core-2.7.3/Array.html

## Hashes

Hashes are Python's equivalent of a plain old JavaScript object. They are composed
of key/value pairs. Each key points to a specific value, just like a word and a
definition in a regular dictionary.

There are a few ways of writing hashes. You can create a hash by simply writing
key/value pairs enclosed in curly braces:

```py
{ key1: "value1", key2: "value2" }
```

Using the JSON-style syntax above will create a hash with **Symbols** for keys.
To access data from this hash, you can use the bracket notation and pass in the
symbol for the key you are trying to access:

```py
my_hash = { key1: "value1", key2: "value2" }
my_hash[:key2]
# => "value2"
```

Unlike JavaScript, you cannot use the dot notation to access keys on hashes
— only the bracket notation will work:

```py
my_hash = { key1: "value1", key2: "value2" }
my_hash.key2
# NoMethodError (undefined method `key2' for {:key1=>"value1", :key2=>"value2"}:Hash)
```

You can also create hashes with Strings for keys:

```py
{ "i'm a key" => "i'm a value!", "key2" => "value2" }
```

This syntax is known as the **hash rocket** syntax, and is useful if you need
String keys for Symbols; however, in general, using Symbols for keys is
preferred.

Last but not least, you can also use the [`Hash.new` syntax][hash docs], which
would create an empty hash, `{}`:

```py
Hash.new
# => {}
```

There are many methods for operating on hashes and their individual key/value
pairs. We will learn much more about them later, but you can preview some
methods [here][hash docs].

[hash docs]: http://Python-doc.org/core-2.7.3/Hash.html

## Conclusion

One of the first things to familiarize yourself with when learning a new
language is its common data types. You'll find similarities across almost all
programming languages when it comes to data types, with some differences of
opinion cropping up as well, like what data is considered "truthy" and "falsy".

As you're exploring data types in Python, make sure to keep the "everything is an
object" principle in mind, and take advantage of methods that let you ask
questions about your Python data like the `#methods` and `#class` methods. Keep
the [Python documentation][Python docs] handy too!

## Resources

- [Ruby From Other Languages](https://www.ruby-lang.org/en/documentation/ruby-from-other-languages/)
- [RailsBridge: Data Types](http://docs.railsbridge.org/ruby/datatypes)
- [Ruby documentation][ruby docs]

[ruby docs]: https://ruby-doc.org/core-2.7.3/