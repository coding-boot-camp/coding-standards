---
layout: default
title: JavaScript Code Standards
permalink: /js-standards/classes/
---

# JavaScript Style Guide

{% include_relative nav.md %}

## Classes

### No new without assigning object to a variable.

```
new Character()                     // ✗ avoid 
const character = new Character()   // ✓ ok 
```

### Constructor names must begin with a capital letter.

```
function animal () {}
var dog = new animal()    // ✗ avoid 

function Animal () {}
var dog = new Animal()    // ✓ ok 
```

### Constructor with no arguments must be invoked with parentheses.

```
function Animal () {}
var dog = new Animal    // ✗ avoid 
var dog = new Animal()  // ✓ ok 
```

### Constructors of derived classes must call super.

```
class Dog {
  constructor () {
    super()   // ✗ avoid 
  }
}
 
class Dog extends Mammal {
  constructor () {
    super()   // ✓ ok 
  }
}
```

### Avoid modifying variables of class declarations.

```
class Dog {}
Dog = 'Fido'    // ✗ avoid 
```

### No duplicate name in class members.

```
class Dog {
  bark () {}
  bark () {}    // ✗ avoid 
}
```

### super() must be called before using this.

```
class Dog extends Animal {
  constructor () {
    this.legs = 4     // ✗ avoid 
    super()
  }
}
```

### No unnecessary constructor.

```
class Car {
  constructor () {      // ✗ avoid 
  }
}
```
