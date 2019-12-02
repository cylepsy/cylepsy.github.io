---
title: Fixing Missing C Headers in ccls on macOS
date: 2019-12-01 22:45:32
tags:
  - C
  - Language Server
  - ccls
  - coc.nvim
---

Recently I switched from _Vim_ to _NeoVim_ because some people keep telling me that Vim is bloated and yadayada.
Even though the latest version of Vim 8 has been developed with a bunch of new features, I was still attempted to switch to NeoVim.

## Conquer of Complete

The first plug-in I came across was [nvimcoc](https://github.com/neoclide/coc.nvim), or a.k.a. **Conquer of Complete**.  
It is an intelliSense engine for Vim 8 and NeoVim, which can work as a Language server client.
In a word, it makes your Vim more VS Code-ish.

## ccls

And ccls is a language server for linting C-Family codes.
Since I'm currently trying to relearn everything in a old school C99 way, thanks to [Nick Walton](https://www.youtube.com/watch?v=Tm2sxwrZFiU), I decided to try out ccls as my first language server.
~~(Well, technically no, because we've all used VS Code.)~~

Anyway, I installed ccls via Homebrew, and tried to use it to lint a dummy C program. Everything seemed OK until something really strange went on.

**ccls won't load my c headers!**

At first I found this when I got an error on _printf_:

```c
 printf("this shit!");
^
```

`[ccls 2] [W] implicitly declaring library function 'printf' with type 'int (const char *, ...)'`

Meanwhile at the top of the file:

```c
#include <stdio.h>
          ^
```

`[ccls 1] [E] 'stdio.h' file not found`

Strangely, my Apple Clang compiler worked just fine. After researching I found that C headers in Mac OS Mojave has been moved to a different directory. I tried to install the header SDK after making sure I've installed the command line tool, and ...

{% asset_img "error.png" "The installation error"%}

Now the nightmare begins. There were so many posts on the internet about fixing this kind of issues, like [this one](https://github.com/MaskRay/ccls/issues/191) or [this one](https://github.com/frida/frida/issues/338).

Obviously, none of those worked for me.

## The Actual fix

Finally I found [this article](https://ianding.io/2019/07/29/configure-coc-nvim-for-c-c++-development/), in which the author also suffered from the same issues.

> If you are using macOS, then chances are ccls cannot find system headers and as a result reports a bunch of errors.
> This is because new macOS systems moves system headers into the macOS SDK directory and no longer places them in /usr/include. And the reason why ccls can find the system headers previously is that /usr/include is hard-coded into ccls during compilation. But now, since the macOS SDK path is not hard-coded, it cannot find them any more.

By using the command `g++ -E -x c++ - -v < /dev/null` I was able to get a list of include paths.
In my case it is:

```
/Library/Developer/CommandLineTools/usr/include/c++/v1
/Library/Developer/CommandLineTools/usr/lib/clang/10.0.1/include
/Library/Developer/CommandLineTools/usr/include
/Library/Developer/CommandLineTools/SDKs/MacOSX10.14.sdk/usr/include
/Library/Developer/CommandLineTools/SDKs/MacOSX10.14.sdk/System/Library/Frameworks
```

By adding them to the .ccls file, the problem seemed to be partly solved by this. While the error still occurs.

To me it seemed like a repeated inclusion issue. In the end I manually located the path of `stdio.h`, which in my case is `/Library/Developer/CommandLineTools/SDKs/MacOSX10.14.sdk/usr/include`.

After deleting everything except this line, ccls finally loaded `stdio.h`, and other STLs.

{% asset_img "final.png" "The final output."%}
