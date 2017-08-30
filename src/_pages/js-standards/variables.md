---
layout: default
title: JavaScript Code Standards
permalink: /js-standards/variables/
---

# JavaScript Style Guide

{% include_relative nav.md %}


## Variables

While it is not automatically enforced, it is a good practice that variable names generally shouldn't be abbreviated.

```
// Good
function saveUser(user) {
    localStorage.set('user', user);
}

// Bad, it's hard to reason about abbreviations in blocks as they grow.
function saveUser(u) {
    localStorage.set('user', u);
}
```

The caveat being single-line arrow functions, where abbreviations are allowed to reduce noise if the context is clear enough. For example, if you're calling map of forEach on a collection of items, it's clear that the parameter is an item of a certain type, which can be derived from the collection's substantive variable name.

```
// Good
function saveUserSessions(userSessions) {
    userSessions.forEach(s => saveUserSession(s));
}

// Ok, but pretty noisy.
function saveUserSessions(userSessions) {
    userSessions.forEach(userSession => saveUserSession(userSession));
}
```

### No unused variables.

```
function myFunction () {
  var result = something()   // ✗ avoid 
}
```

### Use camelcase when naming variables.

```
  var my_var = 'hello'           // ✗ avoid 
  var myVar = 'hello'            // ✓ ok 
```

### For var declarations, write each declaration in its own statement.

```
// ✓ ok 
var silent = true
var verbose = true
 
// ✗ avoid 
var silent = true, verbose = true
 
// ✗ avoid 
var silent = true,
    verbose = true
```    

### Trailing commas not allowed.

```
var obj = {
    message: 'hello',   // ✗ avoid 
}
```

### Commas must be placed at the end of the current line.

```
  var obj = {
    foo: 'foo'
    ,bar: 'bar'   // ✗ avoid 
  }
 
  var obj = {
    foo: 'foo',
    bar: 'bar'   // ✓ ok 
  }
```

### Dot should be on the same line as property.

```
  console.
    log('hello')  // ✗ avoid 
 
  console
    .log('hello') // ✓ ok 
```

### No space between function identifiers and their invocations.

```
console.log ('hello') // ✗ avoid 
console.log('hello')  // ✓ ok 
```

### Add space between colon and value in key value pairs.

```
var obj = { 'key' : 'value' }    // ✗ avoid 
var obj = { 'key' :'value' }     // ✗ avoid 
var obj = { 'key':'value' }      // ✗ avoid 
var obj = { 'key': 'value' }     // ✓ ok 
```

### Avoid modifying variables declared using const.

```
const score = 100
score = 125       // ✗ avoid 
```

### No redeclaring variables.

```
let name = 'John'
let name = 'Jane'     // ✗ avoid 
 
let name = 'John'
name = 'Jane'         // ✓ ok 
```

### Initializing to undefined is not allowed.

```
let name = undefined    // ✗ avoid 
 
let name
name = 'value'          // ✓ ok 
```