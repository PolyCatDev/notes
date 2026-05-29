
Make is a popular build system for C and C++.

In make you write rules to be executed in a file named `Makefile`.


## Rules

A rule in make is made out of 3 components:

1. the target - file that will be created
2. the dependencies - what files are needed to make that file
3. the recipe - the commands to actually generate the target form dependencies

```make
app: main.c
    clang main.c -o app
```

> `app` is the target, `main.c` is the dependency of `app` and `clang main.c -o app` is the recipe.


## How C/C++ projects are compiled by convention using make

The makefile is used to track each and every file in the project. These files all get compiled separately to object files and then linked together into one executable.

> [!Note]
> This is why we use header files. You cannot directly import object files in C. So we import the header files that then point to functions inside object files. That's how the linker knows how to links the object files.

```make
app: main.o foo.o bar.o
    clang main.o foo.o bar.o -o app

main.o: main.c
    clang -c main.c -o main.o

foo.o: foo.c
    clang -c foo.c -o foo.o

bar.o: bar.c
    clang -c bar.c -o bar.o
```

> This generates object files `main.o`, `foo.o` and `bar.o` and links them together if `make app` is ran.


## Variables

Make has support for user defined variables as well as some special built in variables so the programmer doesn't constantly have to repeat themselves.

```make
CC = clang

app: main.o foo.o bar.o
    ${CC} $^ -o $@

main.o: main.c
    ${CC} -c $^ -o $@

foo.o: foo.c
    ${CC} -c $^ -o $@

bar.o: bar.c
    ${CC} -c $^ -o $@
```

> This, without hard coding anything in the makefile, generates object files `main.o`, `foo.o` and `bar.o` and links them together if `make app` is ran.

- `CC` (stands for "c compiler") is user defined and evaluates to `clang`
- `$@` is built in and evaluates to target name of the current rule
- `$^` is built in and evaluates to dependency names of the current rule


## Running tasks

Make can also be used to run tasks by using `.PHONY: <target-name>` before a rule. This tells make that this target won't output a file.

```make
.PHONY: clean

clean:
    rm -rf build app
```

> This, without make expecting an output file, removes a hypothetical `build` folder and `app` binary if `make clean` is ran.
