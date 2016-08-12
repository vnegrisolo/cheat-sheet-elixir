# Elixir Cheat Sheet

Elixir is a dynamic functional compiled language that runs over an Erlang Virtual Machine called BEAM.

Erlang and its BEAM is well known for running low-lattency, distributed and fault-tolerant applications.

Elixir was designed to take all that advantages in a modern coding language.

Elixir data types are immutable.

In Elixir a method is usually described with its arity (number of arguments), such as: `is_boolean/1`.

## File Types

- `.exs` => Elixir script files
- `.ex` => Elixir regular file

## Comments

- `#` => single line comment

There are no multi-line comment

## Interactive Elixir

- `iex` => open Interactive Elixir
- `iex <file>` => open Interactive Elixir loading a file
- `<Ctrl>c + a` => close iex
- `h <method/arity>` => see help for a method
- `h <operator/arity>` => see help for a operator
- `i <object>` => information about an object

## Compile and Run Elixir code

- `elixir <script_file>.exs` => run a script file
- `elixirc <file>.ex` => compile a file to `Elixir.<File>.beam`

## Basic Types

- `1` => integer
- `0x1F` => integer
- `0b1010` => binary integer notation 10
- `0o777` => octadecimal integer notation 511
- `0x1F` => hexadecimal integer notation 31

- `-1.0` => float
- `5.7e-2` => float exponent notation 0.057

- `:atom` => atom / symbol

- `true` => boolean (atom)

- `<<97::size(2)>>` => bit string
- `<<97,98>>` => binay is a sub type of bit string (could be a string if all ASCII)
- `"elixir"` => string (binary)

- `[1, 2, 3]` => list (could be a char list if all ASCII)
- `'elixir'` => char list (list)

- `{1, 2, 3}` => tuple

## Type Testing

- `is_integer 1` => checks for integer
- `is_float 4.6` => checks for float
- `is_number 7.8` => checks for number
- `is_atom :foo` => checks for atom
- `is_boolean false` => checks for boolean
- `is_bitstring <<97:2>>` => checks for bit string
- `is_binary <<97, 98>>` => checks for binary
- `is_function(fn a, b -> a + b end)` => checks for function
- `is_function(fn a, b -> a + b end, 2)` => checks for function with arity

## Number Operators

- `10 / 2 => 5.0` => division always return a float
- `div(10, 2) => 5` => integer division
- `rem 10, 3 => 1` => integer remain of a division
- `round(3.58) => 4` => float round
- `trunc(3.58) => 3` => float trunc

## Boolean Operators

Falsy in Elixir is `false` and `nil`, otherwise will be truthy.

- `==` => equals operator
- `!=` => different operator
- `===` => strict equal operator (integer with float)
- `!==` => strict different operator (integer with float)
- `<` => less operator
- `<=` => less or equal operator
- `>` => greater operator
- `>=` => greater or equal operator
- `and` => boolean and operator
- `or` => boolean or operator
- `not` => boolean not operator
- `&&` => truthy and operator
- `||` => truthy or operator
- `!` => truthy not operator

It's possible to compare different data types. Here are the sorting order for data types: `number < atom < reference < functions < port < pid < tuple < list < bit string`.

## Binaries

- `<>` => concatenate strings
- `byte_size(<<5, 6>>)` => byte size of a binary
- `byte_size("foo")` => byte size of a string
- `?x` => ASCII code for letter `x`

## Strings

String is a sub type of Binary. Strings are surrounded by double-quotes and are encoded in `UTF-8`. Strings are binary sequence of bytes.

- `"hello #{:world}"` => string interpolation
- `"\n"` => new line
- `String.length("hello") # => 5` => get the length of a string
- `String.upcase("hello") # => "HELLO"` => upcase a string
- `"""` => multi-line string

## Performance considerations for Strings and Binaries:

#### cheap Strings and Binaries functions:

- `byte_size(<<97,98>>)`
- `byte_size("Hello")`

#### expensive Strings and Binaries functions:

- `String.length("Hello")`

## Lists

- `++` => concatenate operator
- `--` => subtraction operator
- `hd([1, 5, 7])` => head of a list
- `tl([1, 5, 7])` => tail of a list

If a list contains just printable ASCII numbers Elixir will print it as a Char List.

## Character List

A Char List is a sub type of List. A string surrounded by single-quote is actually a char list. Char list is a List.

- `'ab'` => string representation of a char list
- `[?a, ?b]` => `'ab'`
- `[97, 98]` => `'ab'`

### Performance considerations for Lists and Char Lists:

Lists are linked elements, so every element points to the memory where is the next one.

#### cheap List functions:

- `[0 | list]`

#### expensive List functions:

- `length([1, 4])`
- `length('Hello')`

## Tuples

- `tuple_size({:ok, "hello"})` => tuple size
- `elem({1, 2, 3}, 0)` => get tuple element by index

### Performance considerations for Tuples:

Tuples are stored contiguously in memory.

#### cheap Tuple functions:

- `elem({:ok, "hello"}, 1)`
- `tuple_size({:ok, "hello"})`

#### expensive Tuple functions:

- `put_elem({:ok, "hello"}, 1, "world")`

## Ranges

- `1..10` => range definition
- `Enum.reduce(1..3, 0, fn i, acc -> i + acc end) # => 6` => range used in a reduce function to sum them up
