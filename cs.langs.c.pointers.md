
Pointers are the C data type that stores memory addresses.
They're usually used to indirectly modify data (passing by value).

## Address-of Operator

You can evaluate a pointer value whose value is the memory address of a variable using the `&` operator.

```c
int number = 10;
printf("%p", &number)
```

> This defines a variable called `number`, then the evaluated pointer value pointing to `number` gets printed.
> This program effectively prints out the memory address of the variable named `number`.


## Defining Pointers

Pointers in C are defined using the `*` operator:

```c
uint8_t *number;
```

> This defines a pointer called `number` that can only point to unsigned 8 bit integers.


```c
uint8_t number = 10;
uint8_t *pointToNumber = &number;
```

> This defines a pointer called `pointToNumber` that can only point to type `uint8_t`, the defined pointer is then assigned the evaluated pointer value pointing to `number`.
