
Stuff I tend to forget about bash.

## Builtins

### `command`

With no arguments it bypasses aliases.

```tty
$ command ls
file_1 file_2 file_3
```

With verbose tag it returns what the command evaluates to.

```tty
$ command -v bash
/usr/bin/bash

OR

$ command -v ls
alias ls='lsd'
```


### `type`

It very much so tell you the type of something in the shell.

```tty
$ type ls
ls is aliased to `lsd'
```

But also useful for getting the path of a tool whilst bypassing aliases.

```tty
$ type -P ls
/usr/bin/ls
```


## For loops

```bash
list=("a" "b" "c")

for i in "${list[@]}"; do
    echo $i
done
```


## Associative arrays

```bash
# Declare associative array
declare -A hashmap=(
    ["key_1"]="value_1"
    ["key_2"]="value_2"
    ["key_3"]="value_3"
)

# Return a value based on a specific key
echo ${hashmap["key_1"]}

# Return all values
echo ${hashmap[@]}

# Return all keys
# (i) Specific keys based on values can't be returned
echo ${!hashmap[@]}
```
