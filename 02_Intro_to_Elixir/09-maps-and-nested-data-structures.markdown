---
layout: page
title: Maps and Nested Data Structures
date: 2016-10-1 13:38:30 -0700
---


# Maps

Maps in Elixir provides a quick key-value store called a map. Maps can be created by using the `%{}` syntax:

```elixir
iex> map = %{:a => 1, 2 => :b}
iex> map[:a]  # 1
iex> map[2]   # :b
iex> map[:c]  # nil
iex> # We can use the . syntax to access variables too
iex> map.a   # 1
iex> # but not for an element that doesn't exist...
iex> map.c    # error
```

Maps do not contain ordering and can allow any value to be set as the key, however, it's recommended to stick to literals (strings, atoms, and numbers).

## Nested data structures

Elixir provides a way for us to hold variables inside of maps. We'll use this all over the place in Phoenix, where we'll have variables that represent data structures in our database. For instance, we can create a list of users that is a key-value map to another nested map:

```elixir
iex> users = [
  john: %{name: "John", age: 27, languages: ["Erlang", "Ruby", "Elixir"]},
  mary: %{name: "Mary", age: 29, languages: ["Elixir", "F#", "Clojure"]}
]
```

We can then get variables using the `[]` and `.` syntax:

```elixir
iex> users[:john].age # 27
```

We can then manipulate variables by using the `put_in/2` function to create a new value:

```elixir
iex> users = put_in users[:john].age, 31
iex> users #
john: %{name: "John", age: 27, languages: ["Erlang", "Ruby", "Elixir"]},
mary: %{name: "Mary", age: 29, languages: ["Elixir", "F#", "Clojure"]}
```

Check out the [Kernel module](http://elixir-lang.org/docs/stable/elixir/Kernel.html) documentation for more information on other functions available to use when using nested data structures.

## Executing scripts

So far we've used on the `iex` tool to execute Elixir functionality in real-time. This is not always convenient, especially when we start writing bigger and bigger functions.

Rather than typing in the REPL, we can write to a file with our elixir code and execute it using the `elixir` command-line function:

```elixir
$ echo "IO.puts \"Hello world\"" > test.exs
$ elixir test.exs
"Hello world"
```
