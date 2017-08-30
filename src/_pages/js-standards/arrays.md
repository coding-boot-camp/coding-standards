---
layout: default
title: JavaScript Code Standards
permalink: /js-standards/arrays/
---

# JavaScript Style Guide

{% include_relative nav.md %}

## Arrays

### Array Destructuring

Destructuring is preferred over assigning variables to the corresponding keys.

```
// Good
const [hours, minutes] = '12:00'.split(':');

// Bad, unnecessarily verbose, and requires an extra assignment in this case.
const time = '12:00'.split(':');
const hours = time[0];
const minutes = time[1];
```

### Use array literals instead of array constructors.

```
var nums = new Array(1, 2, 3)   // ✗ avoid 
var nums = [1, 2, 3]            // ✓ ok 
```

### Sparse arrays are not allowed.

```
let fruits = ['apple',, 'orange']       // ✗ avoid 
```