---
layout: default
title: JavaScript Code Standards
permalink: /js-standards/
---

# JavaScript Style Guide

{% include_relative nav.md %}

## Based on StandardJS

Developers want to develop, not spend all of their days formatting code. To this end, we've based this style guide off of [StandardJS](https://standardjs.com/) which will handle formatting your code for your automatically. 

From StandardJS's site: 

> No one wants to maintain multiple hundred-line style configuration files for every module/project they work on. Enough of this madness!

The easiest way to install our code standards is to install StandardJS globally

```
npm install standard -g
```

Having StandardJS installed gives the added benefit of having *most* but not all of your style 'errors' fixed automatically. Once StandardJS is installed, run 

```
standard --fix 
```

Please note that most problems are fixable, but some errors (like forgetting to handle errors) must be fixed manually.

To save you time - we've added a script to the `package.json` of the `BCS-v2` and the `bcs-api` git repos that allows you to run code formatting. 

```
npm codeformat
```

Running this command will run `standard --fix` and present you with the console output.

StandardJS provides many rules and stylistic guardrails. This guide serves to highlight the most important of those.