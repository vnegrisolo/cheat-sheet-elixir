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
