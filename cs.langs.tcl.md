TCL (Tool Command Language) is a scripting language where everything is a string. This includes stuff like types (of which there are only strings), commands and even the language syntax itself.

## Strings and commands

__Strings__ can be declare like this `"string"` or like this `{string}`. Strings declared between quotation marks will have values substituted inside of them whilst the ones between curly braces are completely static. Here's what I mean:

```tcl
set who "Cat"
puts "Hello $who" ;# Prints `Hello Cat`
puts {Hello $who} ;# Prints `Hello $who`
```


__Commands__ are essentially functions that accept strings as inputs and that are called with convention `<cmd-name> <arg1> <arg2> <etc>`. They work a lot like in bash (or most other shells for that manner) and they are defined using the `proc` command.

```tcl
proc greet {name} {
  puts "Hello $name"
}

greet "Iris" ;# Prints `Hello Iris`
```

For all builtin commands see [this list](https://www.tcl-lang.org/man/tcl8.5/TclCmd/contents.htm).


## Running code from within a string

There is a builtin command called `eval` which evaluates whatever you pass it as if it were code. So if we define a static string containing code we can evaluate the string as code. So for example:

```tcl
set code {puts "Printed this from a string"}

puts $code ;# Prints `puts "Printed this from a string"`
eval $code ;# Prints `Printed this from a string`

set cmd "eval"
$cmd $code ;# Prints `Printed this from a string`
```

This is what I meant when I said that even the language's syntax is a string.


## Command substitution

Similar to shells, command substitution can be done using square brackets (`[command]`). So for example:

```tcl
proc animal {} {return "Cat"}
puts "Hello [animal]" ;# Prints `Hello Cat`
```


## Modifying data outside a procedure's scope

By default all values defined within a procedure leave within said procedure's scope.

```tcl
set x 10

proc inc_by_5 {nr} {
    return [incr nr 5]
}

puts [inc_by_5 $x] ;# Prints `15`
```

But if we wanted to modify a variable defined outside a procedure's scope we don't have pointers to do so. What we do instead is use the `upvar` command which informs the parser that the given variable leaves one scope above the current one. This means that procedure don't know about the global scope unless explicitly told.

```tcl
set global_var 10

proc inc_global_by_5 {} {
  upvar global_var local_var
  incr local_var 5
}

puts [inc_global_by_5] ;# Prints `15`
```

If we wanted to do the same but without having to reassign a new local variable we can use the `uplevel` command. This command tells the parser to execute a procedure one (or more) scopes above it. This way procedures that work on data in the same scope from which said procedure was called can be made.

```tcl
set counter 10
set nr_to_add 5

proc add_to_global_counter {} {
    uplevel 1 {expr $counter + $nr_to_add}
}

puts [add_to_global_counter] ;# Prints `15`
```
