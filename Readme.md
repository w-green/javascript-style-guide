# Javascript Style Guide

This is a guide for writing consistent JavaScript.

There is a .jshintrc which enforces these rules as closely as possible.

This guide was largely taken from [Felix Geisendörfer's node style guide](https://github.com/felixge/node-style-guide). It has been modified to keep inline with our own opinions.

## Table of contents

* [2 Spaces for indention](#2-spaces-for-indention)
* [No trailing whitespace](#no-trailing-whitespace)
* [Use Semicolons](#use-semicolons)
* [80 characters per line](#80-characters-per-line)
* [Use single quotes](#use-single-quotes)
* [Opening braces go on the same line](#opening-braces-go-on-the-same-line)
* [Method chaining](#method-chaining)
* [Declare one variable per var statement](#declare-one-variable-per-var-statement)
* [Use lowerCamelCase for variables, properties and function names](#use-lowercamelcase-for-variables-properties-and-function-names)
* [Use UpperCamelCase for class names](#use-uppercamelcase-for-class-names)
* [Use UPPERCASE for Constants](#use-uppercase-for-constants)
* [Object / Array creation](#object--array-creation)
* [Use the === operator](#use-the--operator)
* [Spacings for function declaration](#spacings-for-function-declaration)
* [Write small functions](#write-small-functions)
* [Name your closures](#name-your-closures)
* [No nested closures](#no-nested-closures)
* [Use slashes for comments](#use-slashes-for-comments)
* [Don't use switch](#dont-use-switch)
* [Don't use eval](#dont-use-eval)

Follow the link to see instructions on using the jshint file... [Using the jshint file](#using-the-jshint-file)


## 2 Spaces for indention

Use 2 spaces for indenting your code and never mix tabs and
spaces.

## No trailing whitespace

Clean up any trailing whitespace in your JS files before committing. Most IDEs will have an option to do this on save.

## Use Semicolons

According to [scientific research][hnsemicolons], the usage of semicolons is
a core value of our community. Consider the points of [the opposition][], but
be a traditionalist when it comes to abusing error correction mechanisms for
cheap syntactic pleasures.

[the opposition]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[hnsemicolons]: http://news.ycombinator.com/item?id=1547647

## 80 characters per line

Try to limit your lines to 80 characters.

## Use single quotes

Use single quotes, unless you are writing JSON.

*Right:*

```js
var foo = 'bar';
```

*Wrong:*

```js
var foo = "bar";
```

## Opening braces go on the same line

Your opening braces go on the same line as the statement.

*Right:*

```js
if(true) {
  console.log('winning');
}
```

*Wrong:*

```js
if(true)
{
  console.log('losing');
}
```

## Method chaining

One method per line should be used if you want to chain methods.

You should also indent these methods so it's easier to tell they are part of the same chain.

*Right:*

```js
User
  .findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });
````

*Wrong:*

```js
User
.findOne({ name: 'foo' })
.populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });

User.findOne({ name: 'foo' }).populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' }).populate('bar')
  .exec(function(err, user) {
    return true;
  });
````

## Declare one variable per var statement

Declare one variable per var statement.

*Right:*

```js
var keys   = ['foo', 'bar'];
var values = [23, 42];

var object = {};
while (keys.length) {
  var key = keys.pop();
  object[key] = values.pop();
}
```

*Wrong:*

```js
var keys = ['foo', 'bar'],
    values = [23, 42],
    object = {},
    key;

while (keys.length) {
  key = keys.pop();
  object[key] = values.pop();
}
```

## Use lowerCamelCase for variables, properties and function names

Variables, properties and function names should use `lowerCamelCase`.  They
should also be descriptive. Single character variables and uncommon
abbreviations should generally be avoided.

*Right:*

```js
var adminUser = db.query('SELECT * FROM users ...');
```

*Wrong:*

```js
var admin_user = db.query('SELECT * FROM users ...');
```

## Use UpperCamelCase for class names

Class names should be capitalized using `UpperCamelCase`.

*Right:*

```js
function BankAccount() {
}
```

*Wrong:*

```js
function bank_Account() {
}
```

## Use UPPERCASE for Constants

Constants should be declared as regular variables or static class properties,
using all uppercase letters.

*Right:*

```js
var SECOND = 1 * 1000;

function File() {
}
File.FULL_PERMISSIONS = 0777;
```

*Wrong:*

```js
const SECOND = 1 * 1000;

function File() {
}
File.fullPermissions = 0777;
```

## Object / Array creation

Use trailing commas and put *short* declarations on a single line. Only quote
keys when your interpreter complains:

*Right:*

```js
var a = ['hello', 'world'];
var b = {
  good: 'code',
  'is generally': 'pretty',
};
```

*Wrong:*

```js
var a = [
  'hello', 'world'
];
var b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## Use the === operator

Programming is not about remembering [stupid rules][comparisonoperators]. Use
the triple equality operator as it will work just as expected.

*Right:*

```js
var a = 0;
if (a !== '') {
  console.log('winning');
}

```

*Wrong:*

```js
var a = 0;
if (a == '') {
  console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

## Use descriptive conditions

Any non-trivial conditions should be assigned to a descriptively named variable or function:

*Right:*

```js
var isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if (isValidPassword) {
  console.log('winning');
}
```

*Wrong:*

```js
if (password.length >= 4 && /^(?=.*\d).{4,}$/.test(password)) {
  console.log('losing');
}
```


## Spacings for function declaration

Use no space before parentheses.
Use one space before the curly braces.

*Right:*

```js
function getId() {
  // function body
}
```

*Wrong:*

```js
function getId () {
  // function body
}
```

*Wrong:*

```js
function getId(){
  // function body
}
```

## Write small functions

Keep your functions short. Short functions allow readers to follow logic much clearer.

## Return early from functions

To avoid deep nesting of if-statements, always return a function's value as early
as possible.

*Right:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

*Wrong:*

```js
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

Or for this particular example it may also be fine to shorten things even
further:

```js
function isPercentage(val) {
  var isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```

## Name your closures

Name your closures. Anonymous functions make debugging a nightmare.
Naming functions allows us to produce better stack traces, and dramatically helps us when running profile tests.

*Right:*

```js
element.on('click', function doSomethingCrazy() {
  console.log('crazy stuff');
});
```

*Wrong:*

```js
element.on('click', function() {
  console.log('crazy stuff');
});
```

## No nested closures

Use closures, but don't nest them. Otherwise your code will become a mess.

*Right:*

```js
setTimeout(function() {
  client.connect(afterConnect);
}, 1000);

function afterConnect() {
  console.log('winning');
}
```

*Wrong:*

```js
setTimeout(function() {
  client.connect(function() {
    console.log('losing');
  });
}, 1000);
```

## Use slashes for comments

Use slashes for both single line and multi line comments. Try to write
comments that explain higher level mechanisms or clarify difficult
segments of your code.

*Right:*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE', 'SOMETHING', 'VALUE']
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
function loadUser(id, cb) {
  // ...
}

var isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
  // ...
}
```

*Wrong:*

```js
// Execute a regex
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// Usage: loadUser(5, function() { ... })
function loadUser(id, cb) {
  // ...
}

// Check if the session is valid
var isSessionValid = (session.expires < Date.now());
// If the session is valid
if (isSessionValid) {
  // ...
}
```

## Don't use switch

Say you're creating a game where the nonplayer fight actions are selected based on an algorithm defined elsewhere and passed in to doAction as a string. The switch ... case form looks like this:

```js
function doAction(action) {
  switch (action) {
    case 'hack':
      return 'hack';
    break;

    case 'slash':
      return 'slash';
    break;

    case 'run':
      return 'run';
    break;

    default:
      throw new Error('Invalid action.');
    break;
  }
}
```

The method lookup version looks like this:

```js
function doAction(action) {
  var actions = {
    'hack': function () {
      return 'hack';
    },

    'slash': function () {
      return 'slash';
    },

    'run': function () {
      return 'run';
    }
  };

  if (typeof actions[action] !== 'function') {
    throw new Error('Invalid action.');
  }


  return actions[action]();
}
```

At first glance, it might seem like this is more complicated syntax, but it has a few advantages:

- It uses the standard curly-bracket blocks used everywhere else in JavaScript.

- You never have to worry about remembering the break.

- Method lookup is much more flexible. Using an action object allows you to alter the cases dynamically at runtime, for example, to allow dynamically loaded modules to extend cases, or even swap out some or all of the cases for modal context switching.

- Method lookup is object oriented by definition. With switch ... case, your code is more procedural.

## Don't use eval

The desire to use eval() should be considered a code smell (as in, "something smells fishy"). It's a good indication that there is probably a better way to accomplish what you're after.


.......................

## Using the jshint file

A quick guide is below but if you wanted to look into jshint further you can find the [docs here](http://jshint.com/docs/).

Install jshint globally
npm install jshint -g
(you might need sudo ... sudo npm install jshint -g )

Place the .jshintrc file in the root of your project.

run this in the terminal
jshint filePath/fileName.js

e.g.
jshint alchemiyaServices.js

This will spit out any suggestions...


