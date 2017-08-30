---
layout: default
title: JavaScript Code Standards
permalink: /js-standards/comparisons/
---

# JavaScript Style Guide

{% include_relative nav.md %}

## Comparisons

### Always use === instead of ==.
*Exception: obj == null is allowed to check for null || undefined.*

```
if (name === 'John')   // ✓ ok 
if (name == 'John')    // ✗ avoid 
if (name !== 'John')   // ✓ ok 
if (name != 'John')    // ✗ avoid 
```

### The left operand of relational operators must not be negated.

```
if (!key in obj) {}       // ✗ avoid 
if (!(key in obj)) {}     // ✓ ok 
```

### Avoid Yoda conditions.

```
if (42 === age) { }    // ✗ avoid 
if (age === 42) { }    // ✓ ok 
```
