---
title: Tables and Metatables in Lua
date: 2019-12-15 16:32:57
tags:
	- lua
	- oop
---
Recently I'm building a small game with the awesome [LÖVE](https://love2d.org) engine using Lua.
And I ran into these two important data structures - **tables** and **metatables**.

## Table

A table is an associative array. Tables are neither values nor variables, they are **objects**.

### Creating

They don't need to be declared, they are created by *constructor expression*. Each value in it can be assigned with a key or not. A key can be any data type.

```lua
-- create an empty table.
mytable = {}

-- key value 1 is assinged to string value "Lua"
mytable[1] = "Lua"

-- key value "index" is assinged to string value "value"
mytable["index"] = "value"
```

<!-- more -->

If we assign table *a* to another variable *b*, then both a and *b* point to the table memory. If none of them points to the table anymore, the memory will be released automatically.

```lua
-- now b and mytable points to the same table
b = mytable

-- the output should be "value"
print (b"index")

-- we can still acess the value using b
mytable = nil

-- the memory is released
b = nil
```

---

### Manipulating

Below are some common manipulation functions for tables:

```lua
table.concat(table, sep, start, end)

table.insert(table, pos, value)

table.remove(table, pos)

table.sort(table, comp)
```

#### Concatenate

```lua
fruits = {"apple", "orange", "banana"}

print(table.concat(fruits))
-- appleorangebanana

print(table.concat(fruits,","))
-- apple,orange,banana

print(table.concat(fruits,", ", 2,3))
-- orange, banana
```

#### Inserting and removing

```lua
fruits = {"apple", "orange", "banana"}

table.insert(fruits, "grape")
print(fruits[4])
-- grape

table.insert(fruits, 2, "mango")
print(fruits[2])
-- mango

table.remove(fruits, 5)
print(fruits[5])
-- nil
```

## Metatables

Metatables also are used for OOP-style programming in Lua.

