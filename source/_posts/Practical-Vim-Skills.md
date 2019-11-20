---
title: Practical Vim Skills
date: 2019-11-19 01:32:01
tags: Vim
---

The contents of this article are noted from [this video](https://www.youtube.com/watch?v=wlR5gYd6um0&t=603s).

> I _love_ Vim because I've yet to hit the ceiling.

## Text Objects

Text objects allow you to operate from anywhere within a **defined body of texts**.

- **iw** => _"inner word"_ (works form anywhere in a word)
- **it** => _"inner tag"_ (the contents of an HTML tag)
- **i"** => _"inner quotes"_
- **ip** => _"inner paragraph"_
- **as** => _"a sentence"_

## Parameterized Text Objects

- **f,F** => _"find"_ the next character
- **t,T** => _"find"_ the next character (up to but **not included**)
- **/** => _search_ (up to the next match)

### Example ('|' indicates the cursor)

```html
<div class="users">
  <p>|Users List</p>
  <ul>
    <li>Chris</li>
    <li>Ben</li>
    <li>Joe</li>
  </ul>
</div>
```

How to change the contents before _'List'_?

> Use `ctL` to change up to _'List'_

## Misc

### Repeat Change

Using the **dot (.)** to repeat the last _change_ (motion).

### Relative Number

Turn on relative line numbers for easiear life.

```shell
set relativenumber
```

### Visual-Mode

Try **not** to use Visual-Mode and think if there's a better way.

(tbc in 24.19)
