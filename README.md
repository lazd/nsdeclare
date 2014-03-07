# nsdeclare
> Safely declare a namespace using dot notation

## Namespace declaration

```js
var declare = require('nsdeclare');

var declaration = declare('MyApp.Templates');
```

Result:
```js
this["MyApp"] = this["MyApp"] || {};
this["MyApp"]["Templates"] = this["MyApp"]["Templates"] || {};
```

## Assignment

```js
var declare = require('nsdeclare');

var declaration = declare('MyApp.Templates.Main', { value: 'function() { return "Main"; }' });
```

Result:
```js
this["MyApp"] = this["MyApp"] || {};
this["MyApp"]["Templates"] = this["MyApp"]["Templates"] || {};
this["MyApp"]["Templates"]["Main"] = function() { return "Main"; };
```

## Avoiding redeclaration

```js
var declare = require('nsdeclare');

var options = {
  declared: {}
};

var declaration = [
  declare('MyApp.Views', options),
  declare('MyApp.Templates', options),
  declare('MyApp.Models', options),
  declare('MyApp.Collections', options)
].join('\n');
```

Result:
```js
this["MyApp"] = this["MyApp"] || {};
this["MyApp"]["Views"] = this["MyApp"]["Views"] || {};
this["MyApp"]["Templates"] = this["MyApp"]["Templates"] || {};
this["MyApp"]["Models"] = this["MyApp"]["Models"] || {};
this["MyApp"]["Collections"] = this["MyApp"]["Collections"] || {};
```

## Custom separators

```js
var declare = require('nsdeclare');

var declaration = declare('MyApp.Templates', { separator: '' });
```

Result:
```js
this["MyApp"] = this["MyApp"] || {};this["MyApp"]["Templates"] = this["MyApp"]["Templates"] || {};
```

## Custom root

```js
var declare = require('nsdeclare');

var declaration = declare('MyApp.Templates', { root: 'global' });
```

Result:
```js
global["MyApp"] = global["MyApp"] || {};
global["MyApp"]["Templates"] = global["MyApp"]["Templates"] || {};
```
