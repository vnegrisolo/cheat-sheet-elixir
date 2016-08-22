# Elixir Cheat Sheet

Elixir is a dynamic functional compiled language that runs over an Erlang Virtual Machine called BEAM.

Erlang and its BEAM is well known for running low-lattency, distributed and fault-tolerant applications.

Elixir was designed to take all that advantages in a modern coding language.

Elixir data types are immutable.

In Elixir a method is usually described with its arity (number of arguments), such as: `is_boolean/1`.

## File Types

- `.exs` => Elixir script file
- `.ex` => Elixir regular file
- `.beam` => Compiled Elixir file

## Compile and Run Elixir code

- `elixir <script_file>.exs` => run a script file
- `elixirc <file>.ex` => compile a file to `Elixir.<File>.beam`

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
- `is_integer 1`
- `is_float 4.6`
- `is_number 7.8`
- `is_atom :foo`
- `is_boolean false`
- `is_bitstring <<97:2>>`
- `is_binary <<97, 98>>`
- `is_list/1`
- `is_tuple/1`
- `is_map/1`
- `is_pid/1`
- `is_port/1`
- `is_reference/1`
- `is_function(fn a, b -> a + b end)` => function
- `is_function(fn a, b -> a + b end, 2)` => function with arity
- `Range.range?(1..3)`

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
- `&&` => truthy and
- `||` => truthy or
- `!` => truthy not
- `and` => boolean and
- `or` => boolean or
- `not` => boolean not

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
- `String.length("hello") #=> 5` => get the length of a string
- `String.upcase("hello") #=> "HELLO"` => upcase a string
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
- `:foo in [:foo, :bar] #=> true` => in operator

### Performance for Lists:

#### cheap functions:

- `[97 | [1, 6, 9]]` => prepend
- `hd([1, 5, 7])` => head
- `tl([1, 5, 7])` => tail

#### expensive functions:

- `[1, 5] ++ [3, 9] # [1, 5, 3, 9]` => concatenation
- `[1, 5] -- [9, 5] # [1]` => subtraction first occurrences
- `length([1, 4])`
- `:foo in [:foo, :bar] #=> true` => in operator

## Char List

A Char List is a List of code points where all elements are valid characters. Char Lists are surrounded by single-quote and are usually used as arguments to some old Erlang code.

- `'ab'` => char list
- `[97, 98]` => `'ab'`
- `[?a, ?b]` => `'ab'`
- `?x` => code points (ASCII code) for letter `x`
- `'hello' ++ 'world' # 'helloworld'` => concatenation
- `'hello' -- 'world' # 'hel'` => subtraction first occurrences
- `?l in 'hello' #=> true` => in operator

### Performance for Char Lists:

#### cheap functions:

- `[?H | 'ello']` => prepend

#### expensive functions:

- `'hello' ++ 'world' # 'helloworld'` => concatenation
- `'hello' -- 'world' # 'hel'` => subtraction first occurrences
- `length('Hello')`
- `?l in 'hello' #=> true` => in operator

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
- `map_size(%{name: "Mary"}) #=> 1` => map size

### Performance for Maps:

#### cheap functions:

- `%{name: "Mary", age: 29}[:name]` => fetch `:name`
- `%{name: "Mary", age: 29}.name` => fetch `:name` short notation
- `%{%{name: "Mary", age: 29} | age: 31}` => update value for existing key
- `map_size(%{name: "Mary"}) #=> 1` => map size

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
users[:john].age #=> 27

users = put_in users[:john].age, 31
users = update_in users[:mary].languages, &List.delete(&1, "Clojure")
```

## Ranges

- `range = 1..10` => range definition
- `Enum.reduce(1..3, 0, fn i, acc -> i + acc end) #=> 6` => range used in a reduce function to sum them up
- `Enum.count(range) #=> 10`
- `Enum.member?(range, 11) #=> false`

## do/end Keyword List and Block Syntax

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

## Recursion

There is **no for loop** in Elixir, due to Elixir immutability. Instead you need to use **recursion**:

```elixir
defmodule Logger do
  def log(msg, n) when n <= 0, do: ()
  def log(msg, n) do
    IO.puts msg
    log(msg, n - 1)
  end
end
Logger.log("Hello World!", 3)
# Hello World!
# Hello World!
# Hello World!
```

In functional programming languages **map** and **reduce** are two major algorithm concepts. They can be implemented with **recursion** or using the `Enum` module.

**reduce** will reduces the array into a single element:

```elixir
defmodule Math do
  def sum_list(list, sum \\ 0)
  def sum_list([], sum), do: sum
  def sum_list([head | tail], sum) do
    sum_list(tail, head + sum)
  end
end
Math.sum_list([1, 2, 3]) #=> 6

Enum.reduce([1, 2, 3], 0, &+/2) #=> 6
```

**map** modifies an existing array (new array with new modified values):

```elixir
defmodule Math do
  def double([]), do: []
  def double([head | tail]) do
    [head * 2 | double(tail)]
  end
end
Math.double([1, 2, 3]) #=> [2, 4, 6]

Enum.map([1, 2, 3], &(&1 * 2)) #=> [2, 4, 6]
```

## Pipe Operator

- `|>` => pipe operator

```elixir
1..100 |>
  Stream.map(&(&1 * 3)) |>
  Stream.filter(&(rem(&1, 2) != 0)) |>
  Enum.sum
#=> 7500
```

## Pattern Matching

In Elixir `=` sign is not just an assign operator, but a **Match Operator**.

This means that you assign variables from right side to the left based on patterns defined by the left one. If a pattern does not match a `MatchError` is raised.

This powerful tool is also used to decompose complex objects like tuples, lists, etc into smaller ones:

```elixir
x = 1 #=> assign 1 to x
2 = x #=> ** (MatchError)
1 = x #=> match and does not assign anything

<<0, 1, x>> = <<0, 1, 2, 3>> #=> ** (MatchError)
<<0, 1, x::binary>> = <<0, 1, 2, 3>>
<<0, 1>> <> <<x::binary>> = <<0, 1, 2, 3>>
<<0, 1>> <> <<x, y>> = <<0, 1, 2, 3>>
<<0, 1>> <> <<x>> <> <<y>> = <<0, 1, 2, 3>>

"world" <> x = "hello" #=> ** (MatchError)
"he" <> x = "hello"

{x, y, z} = {1, 2} #=> ** (MatchError)
{} = {1, 2} #=> ** (MatchError)
{:a, :b} = {:b, :a} #=> ** (MatchError)
{x, y} = {1, 2}

[x, 4] = [:a, 5] #=> ** (MatchError)
[] = [:a, 5] #=> ** (MatchError)
[:a, :b] = [:b, :a] #=> ** (MatchError)
[x, 4] = [:a, 4]

[x | y] = [] #=> ** (MatchError)
[x | y] = [1]
[x | y] = [1, 2, 3]

[a: x] = [b: 9] #=> ** (MatchError)
[a: x] = [a: 5]

%{a: x} = %{b: 5} #=> ** (MatchError)
%{} = %{a: 5} # empty map matches any map
%{a: x, b: 5} = %{b: 5, a: 7, c: 9}

first..last = 1..5
```

So in other words:

- non variables on the left side will be used to **restrict a pattern to match**
- variables using the pin operator on the left side will have its value to be used to **restrict a pattern to match**
- variables on the left side will be **assigned** with right side values

So **variables** and **non variables** behave differently with the match operator.

In order to assert an **empty map** you have to use a guard instead of pattern match, just like:

```elixir
(
  fn m when map_size(m) == 0 ->
    "empty map"
  end
).(%{}) #=> "empty map"
```

### Pin Operator

The Pin Operator `^` is used to treat variables the same way non variables with the match operator. In other words, the Pin Operator will evaluate the variable and use its value to **restrict a pattern**, preserving its original value.

```elixir
x = 1 #=> assign 1 to x
^x = 1 #=> match x value with right side 1
^x = 2 #=> ** (MatchError)
```

### Match Operator Limitation

You cannot make function calls on the left side of a match.

- `length([1, [2], 3]) = 3 #=> ** (CompileError) illegal pattern`

## Anonymous Functions

- `fn` => define functions
- `->` => one line function definition
- `.` => call a function
- `when` => guards

```elixir
add = fn a, b -> a + b end
add.(4, 5) #=> 9
```

We can have multiple clauses and guards inside functions.

```elixir
calc = fn
  x, y when x > 0 -> x + y
  x, y -> x * y
end
calc.(-1, 6) #=> 5
calc.(4, 5) #=> 45
```

## Modules And Named Functions

- `defmodule` => define Modules
- `def`  => define functions inside Modules
- `defp`  => define private functions inside Modules
- `when` => guards

```eilxir
defmodule Math do
  def sum(a, b), do: a + b
  def zero?(0), do: true
  def zero?(x) when is_integer(x), do: false
end

Math.sum(1, 2) #=> 3
```

## Default Argument

- `\\` => default argument

```elixir
defmodule Concat do
  def join(a, b, sep \\ " ") do
    a <> sep <> b
  end
end

IO.puts Concat.join("Hello", "world")      #=> Hello world
IO.puts Concat.join("Hello", "world", "_") #=> Hello_world
```

Default values are **evaluated runtime**.

```elixir
defmodule DefaultTest do
  def dowork(x \\ IO.puts "hello") do
    x
  end
end
DefaultTest.dowork #=> :ok
# hello
DefaultTest.dowork 123 #=> 123
DefaultTest.dowork #=> :ok
# hello
```

Function with multiple clauses and a default value requires a **function head** where default values are set:

```elixir
defmodule Concat do
  def join(a, b \\ nil, sep \\ " ") # head function

  def join(a, b, _sep) when is_nil(b) do
    a
  end

  def join(a, b, sep) do
    a <> sep <> b
  end
end

IO.puts Concat.join("Hello")               #=> Hello
IO.puts Concat.join("Hello", "world")      #=> Hello world
IO.puts Concat.join("Hello", "world", "_") #=> Hello_world
```

## Function Capturing

- `&` => function capturing
- `&1` => 1st argument

`&` could be used with a module function.

When capturing you can use the function/operator with its arity.

```elixir
&(&1 * &2).(3, 4) #=> 12
(&*/2).(3, 4) #=> 12

(&Kernel.is_atom(&1)).(:foo) #=> true
(&Kernel.is_atom/1).(:foo) #=> true
(&{:ok, [&1]}).(:foo) #=> {:ok, [:foo, :bar]}
(&[&1, &2]).(:foo, :bar) #=> [:foo, :bar]
(&[&1 | [&2]]).(:foo, :bar) #=> [:foo, :bar]
```

## IO

- `IO.puts "Foo"` => prints to stdout

## File

- `File.read "my-file.md"` => reads a file

## Elixir Special Unbound Variable

- `_` => unbound variable

## Elixir memory inspection

- `:c.memory` => inspect memory

```elixir
:c.memory
# [
#   total: 19262624,
#   processes: 4932168,
#   processes_used: 4931184,
#   system: 14330456,
#   atom: 256337,
#   atom_used: 235038,
#   binary: 43592,
#   code: 5691514,
#   ets: 358016
# ]
```
