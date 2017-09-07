---
layout: default
title: JavaScript Code Standards
permalink: /js-standards/functions/
---

# JavaScript Style Guide

{% include_relative nav.md %}

## Functions

### Async/Await over Promise/Callback

Using async/await is preferred over the promise/callback method for asynchronous calls

### Function Keyword vs Arrow Functions

Function declarations should use the function keyword.

```
// Good
function scrollTo(offset) {
    // ...
}

// Using an arrow function doesn't provide any benefits here, while the
// `function`  keyword immediately makes it clear that this is a function.
const scrollTo = (offset) => {
    // ...
};
```

Terse, single line functions can also use the arrow syntax. There's no hard rule here.

```
// Good
function sum(a, b) {
    return a + b;
}

// It's a short and simple method, so squashing it to a one-liner is ok.
const sum = (a, b) => a + b;
// Good
export function query(selector) {
    return document.querySelector(selector);
}

// This one's a bit longer, having everything on one line feels a bit heavy.
// It's not easily scannable unlike the previous example.
export const query = selector => document.querySelector(selector);
```

Higher order functions can use arrow functions if it improves readability.

```
function sum(a, b) {
    return a + b;
}

// Good
const adder = a => b => sum(a, b);

// Ok, but unnecessarily noisy.
function adder(a) {
    return function (b) {
        return sum(a, b);
    };
}
```

Anonymous functions should use arrow functions.

```
['a', 'b'].map(a => a.toUpperCase());
```

Unless they need access to `this`.

Try to keep your functions pure and limit the usage of the `this` keyword.

Object methods must use the shorthand method syntax.

```
// Good
export default {
    methods: {
        handleClick(event) {
            event.preventDefault();
        },
    },
};

// Bad, the `function` keyword serves no purpose.
export default {
    methods: {
        handleClick: function (event) {
            event.preventDefault();
        },
    },
};
```

### Arrow Function Parameter Brackets

An arrow function's parameter brackets must be omitted if the function is a one-liner.

```
// Good
['a', 'b'].map(a => a.toUpperCase());

// Bad, the parentheses are noisy.
['a', 'b'].map((a) => a.toUpperCase());
```

If the arrow function has its own block, parameters must be surrounded by brackets.

```
// Good, although according to this style guide you shouldn't be using an
// arrow function here!
const saveUser = (user) => {
    //
};

// Bad
const saveUser = user => {
    //
};
```

If you're writing a higher order function, you should emit the parentheses even if the returned function has braces.

```
// Good
const adder = a => b => {
    sum(a, b);
};

// Bad, looks inconsistent in this context.
const adder = a => (b) => {
    sum(a, b);
};
```

### Use camelcase when naming functions.

```
  function my_function () { }    // ✗ avoid 
  function myFunction () { }     // ✓ ok 
```

### No space between function identifiers and their invocations.

```
console.log ('hello') // ✗ avoid 
console.log('hello')  // ✓ ok 
```

### No duplicate arguments in function definitions.

```
function sum (a, b, a) {  // ✗ avoid 
  // ... 
}
 
function sum (a, b, c) {  // ✓ ok 
  // ... 
}
```

### Immediately Invoked Function Expressions (IIFEs) must be wrapped.

```
const getName = function () { }()     // ✗ avoid 
 
const getName = (function () { }())   // ✓ ok 
const getName = (function () { })()   // ✓ ok 
```