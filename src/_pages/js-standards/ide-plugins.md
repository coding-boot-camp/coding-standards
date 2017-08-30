---
layout: default
title: JavaScript Code Standards
permalink: /js-standards/ide-plugins/
---

# JavaScript Style Guide

{% include_relative nav.md %}

## IDE Plugins

### Sublime Text

Using Package Control, install [SublimeLinter](http://www.sublimelinter.com/en/latest/) and [SublimeLinter-contrib-standard](https://packagecontrol.io/packages/SublimeLinter-contrib-standard).

For automatic formatting on save, install [StandardFormat](https://packagecontrol.io/packages/StandardFormat).

### Atom

Install [linter-js-standard](https://atom.io/packages/linter-js-standard).

Alternatively, you can install [linter-js-standard-engine](https://atom.io/packages/linter-js-standard-engine). Instead of bundling a version of standard it will automatically use the version installed in your current project. It will also work out of the box with other linters based on [standard-engine](https://github.com/Flet/standard-engine).

For automatic formatting, install [standard-formatter](https://atom.io/packages/standard-formatter). For snippets, install [standardjs-snippets](https://atom.io/packages/standardjs-snippets).

### Visual Studio Code

Install [vscode-standardjs](https://marketplace.visualstudio.com/items/chenxsan.vscode-standardjs). (Includes support for automatic formatting.)

For JS snippets, install: [vscode-standardjs-snippets](https://marketplace.visualstudio.com/items?itemName=capaj.vscode-standardjs-snippets). For React snippets, install [vscode-react-standard](https://marketplace.visualstudio.com/items/TimonVS.ReactSnippetsStandard).

### WebStorm (PhpStorm, IntelliJ, RubyMine, JetBrains, etc.)

WebStorm recently announced native support for standard directly in the IDE.

If you still prefer to configure standard manually, [follow this guide](https://standardjs.com/webstorm.html). This applies to all JetBrains products, including PhpStorm, IntelliJ, RubyMine, etc.