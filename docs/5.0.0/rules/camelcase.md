---
title: camelcase - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/master/docs/rules/camelcase.md
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Require CamelCase (camelcase)

When it comes to naming variables, style guides generally fall into one of two camps: camelcase (`variableName`) and underscores (`variable_name`). This rule focuses on using the camelcase approach. If your style guide calls for camelCasing your variable names, then this rule is for you!

## Rule Details

This rule looks for any underscores (`_`) located within the source code. It ignores leading and trailing underscores and only checks those in the middle of a variable name. If ESLint decides that the variable is a constant (all uppercase), then no warning will be thrown. Otherwise, a warning will be thrown. This rule only flags definitions and assignments but not function calls. In case of ES6 `import` statements, this rule only targets the name of the variable that will be imported into the local module scope.

## Options

This rule has an object option:

* `"properties": "always"` (default) enforces camelcase style for property names
* `"properties": "never"` does not check property names

### always

Examples of **incorrect** code for this rule with the default `{ "properties": "always" }` option:

```js
/*eslint camelcase: "error"*/

import { no_camelcased } from "external-module"

var my_favorite_color = "#112C85";

function do_something() {
    // ...
}

obj.do_something = function() {
    // ...
};

function foo({ no_camelcased }) {
    // ...
};

function foo({ isCamelcased: no_camelcased }) {
    // ...
}

function foo({ no_camelcased = 'default value' }) {
    // ...
};

var obj = {
    my_pref: 1
};

var { category_id = 1 } = query;

var { foo: no_camelcased } = bar;

var { foo: bar_baz = 1 } = quz;
```

Examples of **correct** code for this rule with the default `{ "properties": "always" }` option:

```js
/*eslint camelcase: "error"*/

import { no_camelcased as camelCased } from "external-module";

var myFavoriteColor   = "#112C85";
var _myFavoriteColor  = "#112C85";
var myFavoriteColor_  = "#112C85";
var MY_FAVORITE_COLOR = "#112C85";
var foo = bar.baz_boom;
var foo = { qux: bar.baz_boom };

obj.do_something();
do_something();
new do_something();

var { category_id: category } = query;

function foo({ isCamelCased }) {
    // ...
};

function foo({ isCamelCased: isAlsoCamelCased }) {
    // ...
}

function foo({ isCamelCased = 'default value' }) {
    // ...
};

var { categoryId = 1 } = query;

var { foo: isCamelCased } = bar;

var { foo: isCamelCased = 1 } = quz;

```

### never

Examples of **correct** code for this rule with the `{ "properties": "never" }` option:

```js
/*eslint camelcase: ["error", {properties: "never"}]*/

var obj = {
    my_pref: 1
};
```

## When Not To Use It

If you have established coding standards using a different naming convention (separating words with underscores), turn this rule off.

## Version

This rule was introduced in ESLint 0.0.2.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/camelcase.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/camelcase.md)
