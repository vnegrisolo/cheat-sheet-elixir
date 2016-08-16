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
- `<<97,98>>` => binary
- `"elixir"` => string

- `{1, 2, 3}` => tuple

- `[1, 2, 3]` => list
- `'elixir'` => char list

- `[a: 5, b: 3]` => keyword list short notation
- `[{:a, 5}, {:b, 3}]` => keyword list long notation

- `%{name: "Mary", age: 29}` => map short notation (keys must be atoms)
- `%{:name => "Mary", :age => 29}` => map long notation

## Type Testing

- `is_nil/1`
- `is_integer 1` => checks for integer
- `is_float 4.6` => checks for float
- `is_number 7.8` => checks for number
- `is_atom :foo` => checks for atom
- `is_boolean false` => checks for boolean
- `is_bitstring <<97:2>>` => checks for bit string
- `is_binary <<97, 98>>` => checks for binary
- `is_list/1`
- `is_tuple/1`
- `is_map/1`
- `is_pid/1`
- `is_port/1`
- `is_reference/1`
- `is_function(fn a, b -> a + b end)` => checks for function
- `is_function(fn a, b -> a + b end, 2)` => checks for function with arity

## Converting Types

- `to_char_list("hełło")` => convert a string to char list
- `to_string('hełło')` => convert a char list to string
- `Map.to_list(%{:a => 1, 2 => :b})` => convert a map to list of tuples or keyword list

## Number Operators

- `10 / 2 => 5.0` => division always return a float
- `div(10, 2) => 5` => integer division
- `rem 10, 3 => 1` => integer remain of a division
- `round(3.58) => 4` => float round
- `trunc(3.58) => 3` => float trunc

## Boolean Operators

Falsy in Elixir is `false` and `nil`, otherwise will be truthy.

- `==` => equals
- `!=` => different
- `===` => strict equal (integer with float)
- `!==` => strict different (integer with float)
- `<` => less
- `<=` => less or equal
- `>` => greater
- `>=` => greater or equal
- `and` => boolean and
- `or` => boolean or
- `not` => boolean not
- `&&` => truthy and
- `||` => truthy or
- `!` => truthy not

It's possible to compare different data types and that's the sorting order: `number < atom < reference < functions < port < pid < tuple < list < bit string`.

## Bit Strings

- `<<97::4>>` => short notation with 4 bits
- `<<97::size(4)>>` => long notation with 4 bits
- `byte_size(<<5::4>>)` => bit string byte size

### Performance for Bit Strings:

#### cheap functions:

- `byte_size(<<97::4>>)`

#### expensive functions:

## Binaries

Binaries are 8 bits multiple Bit Strings. Binaries are 8 bits by default.

- `<<97>>` => short notation with 8 bits
- `<<97::size(8)>>` => long notation with 8 bits
- `<>` => concatenate binaries/strings

### Performance for Binaries:

#### cheap functions:

- `byte_size(<<97>>)`

#### expensive functions:

## Strings

String is a Binary of code points where all elements are valid characters. Strings are surrounded by double-quotes and are encoded in `UTF-8` by default.

- `"hello"` => string
- `<<97, 98>>` => string "ab"
- `<<?a, ?b>>` => string "ab"
 `?x` => code points (ASCII code) for letter `x`
- `"hello #{:world}"` => string interpolation
- `"\n"` => new line
- `String.length("hello") # => 5` => get the length of a string
- `String.upcase("hello") # => "HELLO"` => upcase a string
- `"""` => multi-line string begin/end

### Performance for Strings:

#### cheap functions:

- `byte_size("hello")`

#### expensive functions:

- `String.length("Hello")`

## Tuples

Tuple is a list that is stored contiguously in memory.

- `{:ok, "hello"}`
- `tuple_size({:ok, "hello"})` => tuple size
- `elem({:ok, "hello"}, 0)` => get tuple element by index
- `put_elem({:ok, "hello"}, 1, "world")`

### Performance for Tuples:

#### cheap functions:

- `tuple_size({:ok, "hello"})`
- `elem({:ok, "hello"}, 1)`

#### expensive functions:

- `put_elem({:ok, "hello"}, 1, "world")`

## Lists

List is a linked list structure where each element points to the next one in memory. When subtraction just the first ocurrence will be removed.

- `[:ok, "hello"]`
- `[97 | [1, 6, 9]]` => prepend
- `[1, 5] ++ [3, 9] # [1, 5, 3, 9]` => concatenation
- `[1, 5] -- [9, 5] # [1]` => subtraction first occurrences
- `hd([1, 5, 7])` => head
- `tl([1, 5, 7])` => tail

### Performance for Lists:

#### cheap functions:

- `[97 | [1, 6, 9]]` => prepend
- `hd([1, 5, 7])` => head
- `tl([1, 5, 7])` => tail

#### expensive functions:

- `[1, 5] ++ [3, 9] # [1, 5, 3, 9]` => concatenation
- `[1, 5] -- [9, 5] # [1]` => subtraction first occurrences
- `length([1, 4])`

## Char List

A Char List is a List of code points where all elements are valid characters. Char Lists are surrounded by single-quote and are usually used as arguments to some old Erlang code.

- `'ab'` => char list
- `[97, 98]` => `'ab'`
- `[?a, ?b]` => `'ab'`
- `?x` => code points (ASCII code) for letter `x`
- `'hello' ++ 'world' # 'helloworld'` => concatenation
- `'hello' -- 'world' # 'hel'` => subtraction first occurrences

### Performance for Char Lists:

#### cheap functions:

- `[?H | 'ello']` => prepend

#### expensive functions:

- `'hello' ++ 'world' # 'helloworld'` => concatenation
- `'hello' -- 'world' # 'hel'` => subtraction first occurrences
- `length('Hello')`

## Keyword Lists

Keyword list is a list of tuples where first elements are atoms. When fetching by key the first match will return. If a keyword list is the last argument of a function the square brackets `[` are optional.

- `[a: 5, b: 3]` => keyword list short notation
- `[{:a, 5}, {:b, 3}]` => keyword list long notation
- `[{:a, 6} | [b: 7]] # [a: 6, b: 7]` => prepend
- `[a: 5] ++ [a: 7] # [a: 5, a: 7]` => concatenation
- `[a: 5, b: 7] -- [a: 5] # [b: 7]` => subtraction first ocurrences
- `([a: 5, a: 7])[:a] # 5` => fetch by key
- `length(a: 5, b: 7)` => optional squared brackets `[`

### Performance for Keyword Lists:

#### cheap functions:

- `[{:a, 6} | [b: 7]] # [a: 6, b: 7]` => prepend

#### expensive functions:

- `[a: 5] ++ [a: 7] # [a: 5, a: 7]` => concatenation
- `[a: 5, b: 7] -- [a: 5] # [b: 7]` => subtraction first ocurrences
- `([a: 5, a: 7])[:a] # 5` => fetch by key
- `length(a: 5, b: 7)` => optional squared brackets `[`

## Maps

Map holds a key value structure.

- `%{name: "Mary", age: 29}` => map short notation (keys must be atoms)
- `%{:name => "Mary", :age => 29}` => map long notation
- `%{name: "Mary", age: 29}[:name]` => fetch `:name` hash notation
- `%{name: "Mary", age: 29}[:born]` => returns nil when do not find in the hash notation
- `%{name: "Mary", age: 29}.name` => fetch `:name` short notation
- `%{name: "Mary", age: 29}.born # ** (KeyError)` => blows an error when key does not exists
- `%{%{name: "Mary", age: 29} | age: 31}` => update value for existing key
- `%{%{name: "Mary", age: 29} | born: 1990} # ** (KeyError)` => blows an error when updating non existing key

### Performance for Maps:

#### cheap functions:

- `%{name: "Mary", age: 29}[:name]` => fetch `:name`
- `%{name: "Mary", age: 29}.name` => fetch `:name` short notation
- `%{%{name: "Mary", age: 29} | age: 31}` => update value for existing key

#### expensive functions:

## Nested data Structures

- `put_in/2`
- `update_in/2`
- `get_and_update_in/2`

```elixir
users = [
  john: %{name: "John", age: 27, languages: ["Erlang", "Ruby", "Elixir"]},
  mary: %{name: "Mary", age: 29, languages: ["Elixir", "F#", "Clojure"]}
]
users[:john].age # => 27

users = put_in users[:john].age, 31
users = update_in users[:mary].languages, &List.delete(&1, "Clojure")
```

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

[a: x] = [a: 5]

first..last = 1..5

<<0, 1, x :: binary>> = <<0, 1, 2, 3>>
x # => <<2, 3>>

"he" <> rest = "hello"
rest #=> "llo"

%{a: x} = %{b: 5, a: 7}
x # => 7

%{} = %{a: 5} # empty map matches any map
%{c: x} = %{a: 5} # => ** (MatchError)
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
