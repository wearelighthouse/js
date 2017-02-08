# A Lighthouse Style Guide: JavaScript

*So much fatigue...*

## Table of Contents

1. [npm](#1-npm)
2. [Style Guide](#2-style-guide)
3. [Linting](#3-linting)
4. [`webpack`, Babel & ES6](#4-webpack-babel--es6)

## 1. `npm`

[`npm`](https://www.npmjs.com/) is **the** package manager for JavaScript, at least that's what their website says! The truth is its not the only one but it is a bloody good one so we've chosen to use it! The easiest way to get up and running with it is to install it using [Homebrew](http://brew.sh/), if you don't have [Homebrew](http://brew.sh/) install it! Once that's done you can install `npm` with the following command:

`brew install node`

**N.B.** [Node.js](https://nodejs.org/en/) is a JavaScript runtime whose package ecosystem is `npm`, this is why we install `node` above and not `npm`.

For a more detailed overview of `npm` and how to use it checkout our [`devDependencies`](https://github.com/wearelighthouse/devDependencies#2-npm) style guide.

## 2. Style Guide

The good people over at [Airbnb](https://github.com/airbnb) have put together a [pretty awesome style guide](https://github.com/airbnb/javascript) for JavaScript that we use as our base. We have made a few changes however to keep inline with our [PHP style guide](https://github.com/wearelighthouse/php) which follows [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md).

The differences are as follows:


### Indentation

4 spaces not 2! There is an argument out there talking about a 4% file size reduction when using 2 spaces but as long as your files are minified we feel 4 spaces makes for more readable code.

#### Switch Case Statements

`case` statements **must** be indented 1 level.

~~~javascript
// Bad
switch (someTest) {
case 'foo':
    break;

case 'bar':
    break;

default:
    break;
}

// Good
switch (someTest) {
    case 'foo':
        break;

    case 'bar':
        break;

    default:
        break;
}
~~~

### Brace Style

#### Classes/Methods/Functions

Taken from [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md):

> The opening brace MUST go on its own line, and the closing brace MUST go on the next line following the body

~~~javascript
// Bad
class SomeClass {
    constructor() {
        // Method body
    }
    // Other class methods
}

function someFunction() {
    // Function body
}

// Good
class SomeClass
{
    constructor()
    {
        // Method body
    }

    // Other class methods
}

function someFunction()
{
    // Function body
}
~~~

#### Control Structures

Also taken from [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md):

> There MUST be one space between the closing parenthesis and the opening brace

~~~javascript
// Bad
if (someTruthyTest)
{
    // If body
}

for (var i = 0; i < 10; i++)
{
    // For body
}

// Good
if (someTruthyTest) {
    // If body
}

for (var i = 0; i < 10; i++) {
    // For body
}
~~~

## 3. Linting

Reading through the entire Airbnb style guide would take and you probably have work to do, enter [`eslint`](http://eslint.org/)! Airbnb have even provided eslint configuration for their style guide (thanks very much!) which we are using as the base of our configuration. `eslint` is a project `devDependency` and as such for every project that has JavaScript if should be included in its [package.json](resources/package.json). Use the following command to accomplish that:

~~~
(
  export PKG=eslint-config-airbnb-base;
  npm info "$PKG" peerDependencies --json | command sed 's/[\{\},]//g ; s/: /@/g' | xargs npm install --save-dev "$PKG"
)
~~~

This repository includes a [resources](resources) folder with an `eslint` config file - [`.eslintrc`](resources/.eslintrc) - dump this file in the root of your project once the above is installed and you are ready to lint!

Lint a file by running the following command from the root of your project:

`./node_modules/.bin/eslint someJavaScriptFile.js`

This is cumbersome so you should probably install a package for your favourite text editor to take care of this.

### Sublime Text

Follow these [instructions](https://packagecontrol.io/packages/SublimeLinter-contrib-eslint) to get setup with `eslint` in Sublime Text.

### Linting `brace-style`

Currently the [`brace-style`](http://eslint.org/docs/rules/brace-style) rule only allows one of three options that does not cover our above style guide. Fortunately there is a [pull request](https://github.com/eslint/eslint/issues/6828) in the process of fixing this and once it is we can lint for correct style of braces!

## 4. `webpack`, Babel & ES6

[ES6](https://github.com/lukehoban/es6features) is pretty awesome and makes it so much nicer to write JavaScript, unfortunately it is **still** not fully supported in all browsers. Fortunately [`webpack`](https://webpack.github.io/) and [Babel](https://babeljs.io/) can help us out here and infact ES6 modules are natively supported in Webpack 2 so if you're only using them (which is fine) you don't event need Babel!

For a more detailed overview of `webpack` and Babel checkout our [`devDependencies`](https://github.com/wearelighthouse/devDependencies#5-webpack--babel) style guide.
