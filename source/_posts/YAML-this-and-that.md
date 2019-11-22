---
title: YAML this and that
date: 2019-11-22 02:22:57
tags:
  - YAML
  - Markup Language
---

> YAML Ain't Markup Language

[Credits](https://www.ruanyifeng.com/blog/2016/07/yaml.html)

There are lots of reason to learn about using YAML. ~~Like editing the config file of this blog.~~

## Basic Syntax

There are three types of data structures in YAML:

- **Dictionaries**: Key/value pairs.
- **Arrays/list** A sequence of values.
- **Scalars** : Atomic values.

### Dictionaries

Use **conlon+space** for a key/value pair.

```yaml
animal: pets
```

Equivalent in JS:

```JavaScript
{ animal: 'pets'}
```

Another style in YAML:

```yaml
hash: { name: Steve, foo: bar }
```

Equivalent in JS:

```JavaScript
{hash: { name: 'Steve', foo:'bar' } }
```

### Arrays

A list of words start with hyphen and space form an array

```yaml
- cat
- Dog
- Goldfish
```

Equivalent in JS:

```JavaScript
[ 'Cat', 'Dog', 'Goldfish' ]
```

If a submember of the data structure is an array, indent before it.

```yaml
- - Cat
  - Dog
  - Goldfish
```

Equivalent in JS:

```JavaScript
[['Cat', 'Dog', 'Goldfish' ]]
```

Arrays can also be transfered into one-line style:

```yaml
animal: [Cat, Dog]
```

Equivalent in JS:

```JavaScript
{ animal: ['Cat', 'Dog']}
```

### Scalars

Scalars are basic, unseperatable values:

- Strings
- Booleans
- Integers
- Floats
- Null
- Time
- Date

### Strings

Quotes are not used by default.

```yaml
str: This is a string.
```

Equivalent in JavaScript:

```JavaScript
{str: 'This is a string.'}
```

But if the sting contains spaces or any special symbols, then put them in a quote:

```yaml
str: 'contents: string'
```

Strings can be splited into multiple lines. There must be an indentation from the second line.

```yaml
str: this is a 
  multiple
  line
  string.
```

Equivalent in JavaScript:

```JavaScript
{str: 'this is a  multiple  line  string.'}
```
