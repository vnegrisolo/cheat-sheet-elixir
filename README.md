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
- `is_list/1`
- `is_map/1`
- `is_nil/1`
- `is_pid/1`
- `is_port/1`
- `is_reference/1`
- `is_tuple/1`

## Converting Types

- `to_char_list("hełło")` => convert a string to char list
- `to_string('hełło')` => convert a char list to string

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

- `<>` => concatenate binaries/strings
- `byte_size(<<5, 6>>)` => byte size of a binary
- `byte_size("foo")` => byte size of a string
- `?x` => ASCII code (code points) for letter `x`

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
- `[97 | list]` => append to a list

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

## Keyword List and do/end Block Syntax

In Elixir you can use either **Keyword List** syntax or  **do/end Block** syntax:

```elixir
sky = :gray

if sky == :blue do
  :sunny
else
  :cloudy
end

if sky == :blue, do: :sunny, else: :cloudy

if sky == :blue, do: (
  :sunny
), else: (
  :cloudy
)
```

## Conditional Flows (if/else/case/cond)

### if / else

```elixir
sky = :gray
if sky == :blue, do: :sunny, else: :cloudy
```

### unless / else

```elixir
sky = :gray
unless sky != :blue, do: :sunny, else: :cloudy
```

### case / when

```elixir
sky = {:gray, 75}
case sky, do: (
  {:blue, _}         -> :sunny
  {_, t} when t > 80 -> :hot
  _                  -> :check_wheather_channel
)
```

On **when guards** short-circuiting operators `&&`, `||` and `!` are **not** allowed.

### cond

`cond` is equivalent as `if/else-if/else` statements.

```elixir
sky = :gray
cond do: (
  sky == :blue -> :sunny
  true         -> :cloudy
)
```

## Pattern Matching

In Elixir `=` sign is not just an assign operator, but a **Match Operator**.

This means that you assign variables from right side to the left based on patterns defined by the left one. If a pattern does not match a `MatchError` is raised.

This powerful tool is also used to decompose complex objects like tuples, lists, etc into smaller ones:

```elixir
x = 1 # => assign 1 to x
2 = x # => ** (MatchError)
1 = x # => match and does not assign anything

{a, b, c} = {1, 2} # => ** (MatchError)
{a, b} = {1, 2}
a # => 1
b # => 2

[head | tail] = [1,2,3]
head # => 1
tail # => [2,3]

first..last = 1..5

<<0, 1, x :: binary>> = <<0, 1, 2, 3>>
x # => <<2, 3>>

"he" <> rest = "hello"
rest #=> "llo"
```

So in other words:

- variables on the left side will be **assigned** with right side values
- non variables on the left side will be used to **restrict a pattern to match**

So **variables** and **non variables** behave differently with the match operator.

### Pin Operator

The Pin Operator `^` is used to treat variables the same way non variables with the match operator. In other words, the Pin Operator will evaluate the variable and use its value to **restrict a pattern**, preserving its original value.

```elixir
x = 1 # => assign 1 to x
^x = 1 # => match x value with right side 1
^x = 2 # => ** (MatchError)
```

### Match Operator Limitation

You cannot make function calls on the left side of a match.

- `length([1, [2], 3]) = 3 # => ** (CompileError) illegal pattern`

## Anonymous Functions

- `add = fn a, b -> a + b end` => function definition
- `add.(1, 2)` => call a function

We can have multiple clauses and guards inside functions.

```elixir
calc = fn
  x, y when x > 0 -> x + y
  x, y -> x * y
end
```

## IO

- `IO.puts "Foo"` => prints to stdout

## Elixir Special Unbound Variable

- `_` => unbound variable
