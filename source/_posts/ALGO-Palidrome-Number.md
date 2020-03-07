---
title: ALGO - Palidrome Number
date: 2020-03-08 01:55:18
tags: 
	- ALGO
	- C
---
## Problem
Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

### Bonus

Solve it without converting *int* to *string*.

## Answer
### Ordinary Answer

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int ifPan(char *x) {
  // check if negative
  if (*x == '-')
    return 0;
  int i = 0;
  while (i < strlen(x) / 2) {
    // comparing char from head and tail to middle
    printf("%c is comparing with %c\n", x[i], x[strlen(x) - 1 - i]);
    if (x[i] != x[strlen(x) - 1 - i])
      return 0;
    i++;
  }
  return 1;
}

int main(int argc, char **argv) {
  printf("%d", ifPan(argv[1]));
  return 0;
}
```
<!-- more -->
### Smart Answer
With the bonus

```c
#include <math.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int ifPan(int s) {
  if (s < 0)
    return 0;
  if (s == 0 || s == 1)
    return 1;
  // Calculate the digits of target
  int digits = ceil(log10(s));
  int r = 0, i = 0;
  // Creating a reversed number,
  // But we only need to loop through a less half of the number
  while (i < digits / 2) {
    r = 10 * r + s % 10;
    s = s / 10;
    printf("count %d, s = %d, r = %d\n", i, s, r);
    i++;
  }

  if (digits % 2 != 0)
    // if odd, trim target at last digit (the middle digit of original)
    // and compare with reversed
    return r == s / 10;
  else
    // if even compare with reserved
    return r == s;
}

int main(int argc, char **argv) {
  int source = atoi(argv[1]);

  printf("%d", ifPan(source));
  return 0;
}
```
