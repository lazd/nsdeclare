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

## Response

You can choose to ask for the declaration string, which is the default, or ask to have an object as the reponse with the following format:

  * `namespace`: `string` object corresponding to the namespace,
  * `declaration`: `string` the declaration

### Declaration as a string

```js
var declare = require('nsdeclare');

var declaration = declare('MyApp.Templates', { result: 'string' });
// or default being `string`, simply
var declaration = declare('MyApp.Templates');
```

Result:
```js
global["MyApp"] = global["MyApp"] || {};
global["MyApp"]["Templates"] = global["MyApp"]["Templates"] || {};
```

### Declaration as an object

```js
var declare = require('nsdeclare');

var declaration = declare('MyApp.Templates', { result: 'object' });
```

Result:
```js
{
  namespace: 'this["MyApp"]["Templates"]',
  declaration: '
    this["MyApp"] = this["MyApp"] || {};
    this["MyApp"]["Templates"] = this["MyApp"]["Templates"] || {};
  '
}
```
