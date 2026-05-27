
User input in C is captured using the `stdio.h` header.

```c
#include <stdio.h>
```

> This is how you import the header.


## The `stdin` buffer

`stdio.h` creates a buffer called `stdin` that lasts the whole runtime of the app and that holds user input. If you don't flush the buffer, previously inputted leftover data will spill into new inputs.

```c
#include <stdio.h>

int num1, num2;

scanf("%d", &num1);
scanf("%d", &num2);
```

> In this case, if you input `10.2` (line 4), `.2` will remain in buffer. Thus when inputting for example `8` the second time (line 5), you will actually input `.28` due to not flushing the buffer before hand.


## Flushing the buffer

Flushing is usually done by using `getchar()` in a while loop until it hits `\n`. This will consume all characters in the buffer up to and including `\n`.

```c
#include <stdio.h>

int num1, num2;

scanf("%d", &num1);
while (getchar() != '\n');

scanf("%d", &num2);
while (getchar() != '\n');
```

> This flushes the buffer after each input.
