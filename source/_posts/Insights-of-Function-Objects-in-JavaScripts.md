---
title: Insights of Function Objects in JavaScripts
date: 2019-11-20 22:19:36
tags: JavaScript
---

## Names and Unnamed Function objects

- **Named functions** can be defined after calling.
- **Unnamed functions** have to be defined before calling.

### Example 1

```javascript
func(); //calling
var func = function() {
  alert(1);
};
```

Codes above would trigger error of _func undefined_, while:

```javascript
func(); //calling
function func() {
  alert(1);
}
```

And

```javascript
func(); //calling
function func() {
  alert(1);
}
```

Would work normally.

Therefore, even if JavaScript is an interpreted language, it still searches the whole codes for corresponding definition when a function is called. The function names are only valid when defined with `function funcname()` method, instead of anonymous functions.

## The hidden argument: arguments

When a function is being called, there's another hidden argument created: `arguments`. It similar to an array but not one. It stores the actual arguments passed to the function, but not limited by the parameter lists defined when the function is declared.

### Example 2

```JavaScript
function func(a,b){
    alert(a);
    altert(b);
    for (var i = 0; i < arguments.length; i++){
        alert(arguments[i]);
    }
}
func(1,2,3);
```

The result `1, 2, 1, 2, 3` would popup respectively. Therefore, when defining a function, we can access the parameters via `arguments` even if the parameter list is not specified, which brings us a lot flexibility.

Another attribute of `arguments` is _callee_ which indicates a reference of the function itself.

### Example 3

```JavaScript
var sum = function(n){
  if (1 ==n) return 1;
  else return n + arguments.callee(n-1);
  //same as below
  else return n + sum(n - 1);
}
```

While callee is not the only proof shows that `arguments` are different from _array_ objects. The codes below shows `arguments` not created with _array_ type.

```JavaScript
Array.prototype.p1 = 1;
alert(new Array().p1);
function func(){
  alert(arguments.p1);
}
func();
```

The first _alert_ shows 1, which means the array has arributes _p1_, while calling _func_ shows **undefined**, which means _p1_ is not an attribute of `arguments`. Hence `arguments` is not an array object.
