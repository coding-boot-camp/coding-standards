---
layout: default
title: JavaScript Code Standards
permalink: /js-standards/spacing/
---

# JavaScript Style Guide

{% include_relative nav.md %}

## General Styles

### 2 spaces vs 4 spaces
It's 2. 

Yes, people have strong opinions about this one. But use 2.

### No semicolons.

```
window.alert('hi')   // ✓ ok 
window.alert('hi');  // ✗ avoid 
```

### Use a single import statement per module.

```
import { myFunc1 } from 'module'
import { myFunc2 } from 'module'          // ✗ avoid 
 
import { myFunc1, myFunc2 } from 'module' // ✓ ok 
```

### Always prefix browser globals with window..
Exceptions are: document, console and navigator.

```
window.alert('hi')   // ✓ ok 
```

### No using eval().

```
eval( "var result = user." + propName ) // ✗ avoid 
var result = user[propName]             // ✓ ok 
```

### No floating decimals.

```
const discount = .5      // ✗ avoid 
const discount = 0.5     // ✓ ok 
```

### Regular strings must not contain template literal placeholders.

```
const message = 'Hello ${name}'   // ✗ avoid 
const message = `Hello ${name}`   // ✓ ok 
```

### Avoid string concatenation when using __dirname and __filename.

```
const pathToFile = __dirname + '/app.js'            // ✗ avoid 
const pathToFile = path.join(__dirname, 'app.js')   // ✓ ok 
```

## Use single quotes for strings except to avoid escaping.

```
console.log('hello there')
$("<div class='box'>")
```

### Add a space after keywords.

```
if (condition) { ... }   // ✓ ok 
if(condition) { ... }    // ✗ avoid 
```

### Add a space before a function declaration's parentheses.

```
function name (arg) { ... }   // ✓ ok 
function name(arg) { ... }    // ✗ avoid 
 
run(function () { ... })      // ✓ ok 
run(function() { ... })       // ✗ avoid 
```

### Infix operators must be spaced.

```
// ✓ ok 
var x = 2
var message = 'hello, ' + name + '!'
// ✗ avoid 
var x=2
var message = 'hello, '+name+'!'
```

### Commas should have a space after them.

```
// ✓ ok 
var list = [1, 2, 3, 4]
function greet (name, options) { ... }
// ✗ avoid 
var list = [1,2,3,4]
function greet (name,options) { ... }
```

### Keep else statements on the same line as their curly braces.

```
// ✓ ok 
if (condition) {
  // ... 
} else {
  // ... 
}
// ✗ avoid 
if (condition) {
  // ... 
}
else {
  // ... 
}
```

### Multiple blank lines not allowed.

```
// ✓ ok 
var value = 'hello world'
console.log(value)

// ✗ avoid 
var value = 'hello world'
 
 
console.log(value)
```

### For the ternary operator in a multi-line setting, place ? and : on their own lines.

```
// ✓ ok 
var location = env.development ? 'localhost' : 'www.api.com'
 
// ✓ ok 
var location = env.development
  ? 'localhost'
  : 'www.api.com'
 
// ✗ avoid 
var location = env.development ?
  'localhost' :
  'www.api.com' 
```

### Add spaces inside single line blocks.

```
function foo () {return true}    // ✗ avoid 
function foo () { return true }  // ✓ ok 
```
