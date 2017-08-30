---
layout: default
title: JavaScript Code Standards
permalink: /js-standards/objects/
---

# JavaScript Style Guide

{% include_relative nav.md %}

## Objects

### Object Destructuring

Destructuring is preferred over assigning variables to the corresponding keys.

Destructuring is very valuable for passing around configuration-like objects.

```
function uploader({
    element,
    url,
    multiple = false,
    beforeUpload = noop,
    afterUpload = noop,
}) {
    // ...
}
```


### No duplicate keys in object literals.

```
var user = {
  name: 'Jane Doe',
  name: 'John Doe'    // ✗ avoid 
}
```

### No extending native objects.

```
Object.prototype.age = 21     // ✗ avoid 
```

### No empty destructuring patterns.

```
const { a: {} } = foo         // ✗ avoid 
const { a: { b } } = foo      // ✓ ok 
```

### Objects must contain a getter when a setter is defined.

```
var person = {
  set name (value) {    // ✗ avoid 
    this.name = value
  }
}
 
var person = {
  set name (value) {
    this.name = value
  },
  get name () {         // ✓ ok 
    return this.name
  }
}
```

