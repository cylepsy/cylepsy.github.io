---
title: JavaScript Common Confusion
date: 2019-11-20 22:19:36
tags: JavaScript
---
## Names and Unnamed Function objects

* **Named functions** can be defined after calling.
* **Unnamed functions** have to be defined before calling.

### Example

```javascript
func();  //calling
var func=function(){  
  alert(1)  
}  
```

Codes above would trigger error of *func undefined*, while:

```javascript
func();  //calling
function func(){  
  alert(1)  
}  
```

And

```javascript
func();  //calling
function func(){  
  alert(1)  
}  
```

Would work normally.

Therefore, even if JavaScript is an interpreted language, it still searches the whole codes for corresponding definition when a function is called. The function names are only valid when defined with `function funcname()` method, instead of anonymous functions.
