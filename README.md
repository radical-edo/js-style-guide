
## Table of Contents

  1. [Dictionary](#dictionary)
  1. [General Rules](#general-rules)
  1. [Code formatting and styling](#code-formatting-and-styling)
  1. [Objects](#objects)
  1. [Loops](#loops)
  1. [Conditionals](#conditionals)
  1. [Arrays](#arrays)
  1. [Arguments](#arguments)
  1. [Strings](#strings)
  1. [Functions](#functions)
  1. [Properties](#properties)
  1. [Variables](#variables)
  1. [Callbacks](#callbacks)
  1. [Try-catch](#try-catch)
  1. [Conditional Expressions & Equality](#conditional-expressions--equality)
  1. [Comments](#comments)
  1. [Type Casting & Coercion](#type-casting--coercion)
  1. [Naming Conventions](#naming-conventions)
  1. [Accessors](#accessors)
  1. [Constructors](#constructors)
  1. [License](#license)
  1. [Reference](#reference)

## Dictionary

  Some terms are used in this style guide, which may be confusing for a reader

  - `class` - will refere to any method of serving objects, wheter it's a *ES6* classes which basically are
    *CoffeeScript* classes, or those are object factories. Examples:

  ```js
  var ClassName = (function () { // ES6/CoffeeScript class pattern in ES5
    function ClassName() {}

    ClassName.prototype.instanceMethod = function () {
    };

    return ClassName;
  })();

  var classInstance = new ClassName();

  var factoryName = function () { // object factory pattern
    var factoryInstance = {};

    factoryInstance.instanceMethod = function () {
    };

    return factoryInstance;
  };

  var factoryObject = factoryName();
  ```

  - `const` reverse to variables that cannot be changed and are only once defined.
    This is a feature of *ES6*, however in *ES5* you have to keep that in mind when coding.

## General Rules

  - use `'use strict';` mode

  - always prefer functional programing over procedual. Meaning write a lot of small functions
    instead of one big function that does everything. Doing so will facilitate function chains, which in turn improve code readability

  - a `class` should have at the most 100 lines of code.

  - a single line of code should have at the most 100 columns wide. white spaces count

  - in every project you should always include at least some sort of utility library, examples: `lodash`, `mout`
    the reason being we don't want to re-invent the wheel. maybe you won't need them in the first few
    days of development. but down line..., you will.


**[⬆ back to top](#table-of-contents)**

## Code formatting and styling

  - semicolons **Yup.**

    ```javascript
    // bad
    (function() {
      var name = 'Skywalker'
      return name
    })()

    // good
    (function() {
      var name = 'Skywalker';
      return name;
    })();

    // good
    ;(function() {
      var name = 'Skywalker';
      return name;
    })();
    ```
  - Leading commas: **Nope.**

    ```javascript
    // bad
    var hero = {
        firstName: 'Bob'
      , lastName: 'Parr'
      , heroName: 'Mr. Incredible'
      , superPower: 'strength'
    };

    // good
    var hero = {
      firstName: 'Bob',
      lastName: 'Parr',
      heroName: 'Mr. Incredible',
      superPower: 'strength'
    };
    ```

  - Additional trailing comma: **Nope.** This can cause problems with IE6/7 and IE9 if it's in quirksmode. Also, in some implementations of ES3 would add length to an array if it had an additional trailing comma. This was clarified in ES5 ([source](http://es5.github.io/#D)):

  > Edition 5 clarifies the fact that a trailing comma at the end of an ArrayInitialiser does not add to the length of the array. This is not a semantic change from Edition 3 but some implementations may have previously misinterpreted this.

    ```javascript
    // bad
    var hero = {
      firstName: 'Kevin',
      lastName: 'Flynn',
    };

    var heroes = [
      'Batman',
      'Superman',
    ];

    // good
    var hero = {
      firstName: 'Kevin',
      lastName: 'Flynn'
    };

    var heroes = [
      'Batman',
      'Superman'
    ];
    ```

  - Use soft tabs set to 2 spaces

    ```javascript
    // bad
    function () {
    ∙∙∙∙var name;
    }

    // bad
    function () {
    ∙var name;
    }

    // good
    function () {
    ∙∙var name;
    }
    ```

  - Place 1 space before the leading brace.

    ```javascript
    // bad
    function test(){
      console.log('test');
    }

    // good
    function test() {
      console.log('test');
    }

    // bad
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog'
    });

    // good
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog'
    });
    ```

  - Set off operators with spaces.

    ```javascript
    // bad
    var x=y+5;

    // good
    var x = y + 5;
    ```

  - End files with a single newline character.

    ```javascript
    // bad
    (function(global) {
      // ...stuff...
    })(this);
    ```

    ```javascript
    // bad
    (function(global) {
      // ...stuff...
    })(this);↵
    ↵
    ```

    ```javascript
    // good
    (function(global) {
      // ...stuff...
    })(this);↵
    ```

  - Use indentation when making long method chains.

    ```javascript
    // bad
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // good
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // bad
    var leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
        .attr('width',  (radius + margin) * 2).append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);

    // good
    var leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .class('led', true)
        .attr('width',  (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);
    ```

  - naming

    - `class` names are *pascal cased* with the exception of _factory patter_ - this has to be *camel cased*
    - instance names, variable names, functions names are *camel cased*
    - `const` names are *capitalized* and *snaked cased* - example `THIS_IS_A_CONST_VARIABLE = 12`
      Idea is for this variable to stand out and inform the developer no to re-define this variable.

  - _`require`_ if in CommonJS envrioment. require in the following order (and always on top of the file):

    1. core modules
    1. *npm* modules
    1. others
  
    with space in between each type of requires, example:

    ```javascript
    var fs = require('fs');
    var path = require('path');

    var _ = require('lodash');
    var Promise = require('bluebird');

    var User = require('../models/user');
    var Post = require('../models/post');
    ```

  - _`module.exports`_
  
    - is only called once per file

    - no need to crawl through the file and see what has been exported. it should always be visible
      and easy to find

    - exported value is always at the end of the file.

    - nothing can be written after the export statment


  - Do not use the `.js` when requiring modules

    ```javascript
      // bad
      var Batmobil = require('./models/Car.js');

      // good
      var Batmobil = require('./models/Car');
    ```


**[⬆ back to top](#table-of-contents)**

  - file names

    Although the convetion in JavaScript any names are usally *camel cased* the file names should be *snaked cased*, mening: `user_store.js` over `userStore.js` or `UserStore.js` or even `userstore.js`. 
    Mostly because for *git* there is no difference between last 3 examples.

  - _`if..else`_
  
  ```js
  // good
  if (/* condition */) {
  } else {
  }
  ```

  - _`function`_

  ```javascript
  // good
  function () {
  }

  function namedFn() {
  }
  ```


**[⬆ back to top](#table-of-contents)**

## Asynchronous code

  - prefer promises over callbacks

    As a general rule when you need to handle an asynchronus code use promises if this at all possible.
    If handling with a bult-in method that doesn't return a promise consider wrapping that peace of code and return a promise

    ```javascript
      function readFromFile(filePath) {
        return new Promise(function (resolve, reject) {
          fs.readFile(filePath, function (err, data) {
            if (err) {
              return reject(err);
            }
            resolve(data);
          });
        });
      })

      readFromFile('package.json')
        .then(function (data) {
        })
        .catch(function (err) {
        })
    ```

    Or if you have *bluebird* package available (which you should), consider using `Promise.promisifyAll`

    ```javascript
    var fs = require('fs');

    var Promise = require('bluebird');

    Promise.promisifyAll(fs);

    fs.readFileAsync('package.json')
      .then(function (data) {})
      .catch(function (err) {});
    ```

    More on [promisifcation|https://github.com/petkaantonov/bluebird/blob/master/API.md#promisification]

**[⬆ back to top](#table-of-contents)**

## Objects

  - Use the literal syntax for object creation.

    ```javascript
    // bad
    var item = new Object();

    // good
    var item = {};
    ```

**[⬆ back to top](#table-of-contents)**

## Loops

  - don't use traditional loops to iterate over an array, use bult-in js methods like `forEach`, `map`

  ```javascript
  // bad
  function (arr) {
    for (var i = 0; i < arr.length; i++) {
      // do stuff
    }
  }

  // good
  function (arr) {
    arr.forEach(function (el, i) {
      // do stuff
    });
  }

  // bad
  function (arr) {
    for (var i = 0; i < arr.length; i++) {
      // do stuff
    }
    return arr;
  }

  // good
  function (arr) {
    return arr.map(function (el, i) {
      // do stuff
    });
  }
  ```

  reason behind this. promotes a chainable code which is nicely readable
  and `for` loop has a small side effect. the index/iterator value after the loop has finished is set to whatever
  index was last used.

  - to iterate over the `Object` props use a utility function library (if lodash that would be `forOwn`)

  or at least

  ```js
  Object.keys(obj).forEach(function (prop) {
    // do stuff
  });
  ```

## Conditionals

  - _`switch..case`_

    - do not use it
      
      generally `switch..case` promotes a big function that has a tendency to blow out of a proportion
      hard to maintain and over time. such function will have a big cyclomatic complexity

    - instead use one of the following
      
      as [strategyPattern](http://encosia.com/first-class-functions-as-an-alternative-to-javascripts-switch-statement)

      or us inheritance

    - as a side note
      `switch..case` can have up to 128 _case-clauses_, any more than that and the function is not optimizable

  - `if..else`

    - try to avoid `if..else if..else`
      
      meaning this

      ```javascript
      if () {
      } else if () {
      } else {
      }
      ```

      for the same reasons as why not to use `switch..case` the function will grow in size and becomes hard to maintain
      if the `else..if` will be added and added.

## Arrays

  - Use the literal syntax for array creation

    ```javascript
    // bad
    var items = new Array();

    // good
    var items = [];
    ```

  - If you don't know array length use Array#push.

    ```javascript
    var someStack = [];


    // bad
    someStack[someStack.length] = 'abracadabra';

    // good
    someStack.push('abracadabra');
    ```

  - When you need to copy an array use Array#slice. [jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)

    ```javascript
    var len = items.length;
    var itemsCopy = [];
    var i;

    // bad
    items.forEach(function (item, i) {
      itemsCopy[i] = item;
    });

    // good
    itemsCopy = items.slice();
    ```

**[⬆ back to top](#table-of-contents)**

## Arguments

  `arguments` are a bit tricky since they are wrong usage can cause optimization problems. Only the following usages is considered safe.

  - `arguments.length`
  - `arguments[i]`, *where `i` is always a valid integer index into the `arguments`, and cannot be out of bound*
  - `Function#apply`, meaning
    
    ```javascript
    var instance = new Instance();
    var fn = function fn() {}

    (function () {
      fn.apply(instnace, arguments);
    })('a', 'b', 'c', 'd');
    ```

**[⬆ back to top](#table-of-contents)**

## Strings

  - Use single quotes `''` for strings

    ```javascript
    // bad
    var name = "Bob Parr";

    // good
    var name = 'Bob Parr';

    // bad
    var fullName = "Bob " + this.lastName;

    // good
    var fullName = 'Bob ' + this.lastName;
    ```

  - Strings longer than 80 characters should be written across multiple lines using string concatenation.

  - Note: If overused, long strings with concatenation could impact performance. [jsPerf](http://jsperf.com/ya-string-concat) & [Discussion](https://github.com/airbnb/javascript/issues/40)

    ```javascript
    // bad
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // good
    var errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';
    ```

  - When programmatically building up a string, use Array#join instead of string concatenation.

    ```javascript
    var items;
    var messages;

    messages = [{
      state: 'success',
      message: 'This one worked.'
    }, {
      state: 'success',
      message: 'This one worked as well.'
    }, {
      state: 'error',
      message: 'This one did not work.'
    }];

    // bad
    function inbox(messages) {
      items = '<ul>';
      for (var i = 0; i < messages.length; ++i) {
        items += '<li>' + messages[i].message + '</li>';
      }
      return items + '</ul>';
    }

    // good
    function inbox(messages) {
      items = '<ul>';
      messages.forEach(function (message) {
        items += '<li>' + message.message + '</li>';
      });
      return items + '</ul>';
    }

    // better
    function inbox(messages) {
      return '<ul><li>' + messages.map(function (message) {
        return message.message;
      }).join('</li><li>') + '</li></ul>';
    }
    ```

**[⬆ back to top](#table-of-contents)**


## Functions

  - Function expressions:

    ```javascript
    // anonymous function expression
    var anonymous = function () {
      return true;
    };

    // named function expression
    var named = function named() {
      return true;
    };

    // immediately-invoked function expression (IIFE)
    (function() {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    ```

  - Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead.

    ```javascript
    // bad
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // good
    var test;
    if (currentUser) {
      test = function test() {
        console.log('Yup.');
      };
    }
    ```

  - Never name a parameter `arguments`, this will take precedence over the `arguments` object that is given to every function scope.

    ```javascript
    // bad
    function nope(name, arguments) {
      // ...stuff...
    }

    // good
    function yup(name, args) {
      // ...stuff...
    }
    ```

  - Function should never have more than 5 lines of code.

    The idea behind this one is to limit the `function` responsiblities. and it's easier to test
    the code

  - Function should have at the most 3 arguments
    
    if you are passing more chances are that you need to pass an object
    

**[⬆ back to top](#table-of-contents)**


## Properties

  - Use dot notation when accessing properties.

    ```javascript
    var luke = {
      jedi: true,
      age: 28
    };

    // bad
    var isJedi = luke['jedi'];

    // good
    var isJedi = luke.jedi;
    ```

  - Use subscript notation `[]` when accessing properties with a variable.

    ```javascript
    var luke = {
      jedi: true,
      age: 28
    };
    function getProp(prop) {
      return luke[prop];
    }

    var isJedi = getProp('jedi');
    ```

**[⬆ back to top](#table-of-contents)**


## Variables

  - Always use `var` to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace.
    Captain Planet warned us of that. As mentioned in the [General rules](#general-rules) section you should always `use strict` mode. So the this action will
    raise an error.

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    var superPower = new SuperPower();
    ```

  - Declare each variable on a newline, with a `var` before each of them.

    ```javascript
    // bad
     var items = getItems(),
          goSportsTeam = true,
          dragonball = 'z';

    // good
     var items = getItems();
     var goSportsTeam = true;
     var dragonball = 'z';
    ```

    If there are too many declartions in a function, chances are the functions is to big and has too many resposiblities

  - Declare unassigned variables last. This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

    ```javascript
    // bad
    var i;
    var items = getItems();
    var dragonball;
    var goSportsTeam = true;
    var len;

    // good
    var items = getItems();
    var goSportsTeam = true;
    var dragonball;
    var length;
    var i;
    ```

  - Avoid redundant variable names, use `Object` instead.

    ```javascript

    // bad
    var kaleidoscopeName = '..';
    var kaleidoscopeLens = [];
    var kaleidoscopeColors = [];

    // good
    var kaleidoscope = {
      name: '..',
      lens: [],
      colors: []
    };
    ```

  - Assign variables at the top of their scope. This helps avoid issues with variable declaration and assignment hoisting related issues.

    ```javascript
    // bad
    function() {
      test();
      console.log('doing stuff..');
      //..other stuff..
      var name = getName();
      if (name === 'test') {
        return false;
      }
      return name;
    }

    // good
    function() {
      var name = getName();
      test();
      console.log('doing stuff..');
      //..other stuff..
      if (name === 'test') {
        return false;
      }
      return name;
    }
    ```

    An exception can be made, if you are using a guard statement

    ```javascript
    // bad
    function() {
      var name = getName();
      if (!arguments.length) {
        return false;
      }
      return true;
    }

    // good
    function() {
      if (!arguments.length) {
        return false;
      }
      var name = getName();
      return true;
    }
    ```

## Callbacks

  - *Promises over callbacks*, but if you do have them. follow rules mentioned below

  - Always check for errors in callbacks. in *node.js* first argument of a callback will be an `error` object

  ```javascript
  //bad
  database.get('pokemons', function(err, pokemons) {
    console.log(pokemons);
  });

  //good
  database.get('drabonballs', function(err, drabonballs) {
    if (err) {
      // handle the error somehow, maybe return with a callback
      return console.log(err);
    }
    console.log(drabonballs);
  });
  ```

  - Return on callbacks

  ```javascript
  //bad
  database.get('drabonballs', function(err, drabonballs) {
    if (err) {
      // if not return here
      console.log(err);
    }
    // this line will be executed as well
    console.log(drabonballs);
  });

  //good
  database.get('drabonballs', function(err, drabonballs) {
    if (err) {
      // handle the error somehow, maybe return with a callback
      return console.log(err);
    }
    console.log(drabonballs);
  });
  ```

**[⬆ back to top](#table-of-contents)**


## Try catch

  - only throw in synchronous functions

  Try-catch blocks cannot be used to wrap async code. They will bubble up to to the top, and bring
  down the entire process.

  ```javascript
  //bad
  function readPackageJson (callback) {
    fs.readFile('package.json', function(err, file) {
      if (err) {
        throw err;
      }
      ...
    });
  }
  //good
  function readPackageJson (callback) {
    fs.readFile('package.json', function(err, file) {
      if (err) {
        return  callback(err);
      }
      ...
    });
  }
  ```

  - in synchronus function the `try..catch` causes problems. mainly due the fact that this function cannot be optimized.
    Nontheless, sometimes this cannot be avoided, but the damage can be minized

  ```javascript
  // bad
  var parseJson = function parseJson(string) {
    var data;
    try {
      data = JSON.parse(string);
    } catch (e) {
      return console.error('Invalid JSON string');
    }
    // do something with the 'data'
    // ...
  }

  // good
  var tryCatch = function tryCatch(fn, ctx, args) {
    try {
      return fn.apply(ctx, args);
    } catch (e) {
      return e;
    }
  }

  var parseJson = function parseJson(string) {
    var data = tryCatch(JSON.parse, null, [string]);
    if (data instanceof Error) {
      return console.error('Invalid JSON string');
    }
    // do something with the 'data'
    // ...
  }
  ```

  the `tryCatch` function contains the part of the code that's not optimized, this allows `parseJson` function to be optimized.

  with *lodash*
  ```javascript
  // better

  var _ = require('lodash');

  var parseJson = function parseJson(string) {
    var data = _.attempt(JSON.parse.bind(null, str));
    if (_.isError(data)) {
      return console.error('Invalid JSON string');
    }
    // do something with the 'data'
    // ...
  }
  ```

**[⬆ back to top](#table-of-contents)**

## Conditional Expressions & Equality

  - Use `===` and `!==` over `==` and `!=` with one exception.
    
    ```javascript
      var obj = { foo: true };
      if (obj.foo != null) {
        console.log('obj has foo prop');
      }

      if (obj.bar == null) {
        console.log('obj prop bar is null or undefined');
      }
    ```

    somtimes we may want to know if the value is acutally `null` or `undefined`
    but most of the times those neither of those values are acceptable. so no need to write
    explicitly `obj.bar === null && obj.bar === undefined`

  - don't build complicated conditinals it's hard to follow them, consider wrapping some condtions into a single function

  ```javascript
  // bad
  if (user1.hasHand() && user1.isFriendlyTwords(user2) && user2.hasHand() && user2.isFriendlyTwords(user1)) {
    user1.greets(user2);
    user2.greets(user1);
  }

  // good
  if (user1.wantsToShakeHandWith(user2) && user2.wantsToShakeHandWith(user1)) {
    user1.greets(user2);
    user2.greets(user1);
  }
  ```

**[⬆ back to top](#table-of-contents)**


## Comments

  - Use `/** ... */` for multiline comments. Include a description, specify types and values for all parameters and return values.

    ```javascript
    // bad
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param <String> tag
    // @return <Element> element
    function make(tag) {

      // ...stuff...

      return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed in tag name
     *
     * @param <String> tag
     * @return <Element> element
     */
    function make(tag) {

      // ...stuff...

      return element;
    }
    ```

  - Never comment out a piece of code. If it's commented out then it's not needed. Just delete it.

  - Don't use comments to explain a functionality. If the code is to hard to understand and it's confusing
    you should refactor it.

  - Avoid unnecesary or pointless comments f.e.

    ```javascript
    // declaring `total` variable and setting it to 0
    var total = 0;

    //....

    // logging into the console the acumulated `total` value
    console.log(total);
    ```

  - Do not use `// FIXME:` to annotate problems

    ```javascript
    function Calculator() {

      // FIXME: shouldn't use a global here
      total = 0;

      return this;
    }
    ```

    if there is a problem, fix it, don't leave it for later.

  - Do not use `// TODO:` to annotate solutions to problems

    ```javascript
    function Calculator() {

      // TODO: total should be configurable by an options param
      this.total = 0;

      return this;
    }
    ```

    if there is something that you think will improve the code base do it. don't leave it for later.
    chances are that you will never do it and the comment will be there forever.

**[⬆ back to top](#table-of-contents)**

## Type Casting & Coercion

  - Perform type coercion at the beginning of the statement.
  - Strings:

    ```javascript
    //  => this.reviewScore = 9;

    // bad
    var totalScore = this.reviewScore + '';

    // good
    var totalScore = '' + this.reviewScore;

    // bad
    var totalScore = '' + this.reviewScore + ' total score';

    // good
    var totalScore = this.reviewScore + ' total score';
    ```

  - Use `parseInt` for Numbers and always with a radix for type casting.

    ```javascript
    var inputValue = '4';

    // bad
    var val = new Number(inputValue);

    // bad
    var val = +inputValue;

    // bad
    var val = inputValue >> 0;

    // bad
    var val = parseInt(inputValue);

    // good
    var val = Number(inputValue);

    // good
    var val = parseInt(inputValue, 10);
    ```

  - If for whatever reason you are doing something wild and `parseInt` is your bottleneck and need to use Bitshift for [performance reasons](http://jsperf.com/coercion-vs-casting/3)

  - **Note:** Be careful when using bitshift operations. Numbers are represented as [64-bit values](http://es5.github.io/#x4.3.19), but Bitshift operations always return a 32-bit integer ([source](http://es5.github.io/#x11.7)). Bitshift can lead to unexpected behavior for integer values larger than 32 bits. [Discussion](https://github.com/airbnb/javascript/issues/109). Largest signed 32-bit Int is 2,147,483,647:

    ```javascript
    2147483647 >> 0 //=> 2147483647
    2147483648 >> 0 //=> -2147483648
    2147483649 >> 0 //=> -2147483647
    ```

  - Booleans:

    ```javascript
    var age = 0;

    // bad
    var hasAge = new Boolean(age);

    // good
    var hasAge = Boolean(age);

    // good
    var hasAge = !!age;
    ```

**[⬆ back to top](#table-of-contents)**


## Naming Conventions

  - Use readable synonyms in place of reserved words.

    ```javascript
    // bad
    var superman = {
      class: 'alien'
    };

    // bad
    var superman = {
      klass: 'alien'
    };

    // good
    var superman = {
      type: 'alien'
    };
    ```

  - Avoid single letter names. Be descriptive with your naming.

    ```javascript
    // bad
    function q() {
      // ...stuff...
    }

    // good
    function query() {
      // ..stuff..
    }
    ```

  - Use camelCase when naming objects, functions, and instances

    ```javascript
    // bad
    var OBJEcttsssss = {};
    var this_is_my_object = {};
    function c() {}
    var u = new user({
      name: 'Bob Parr'
    });

    // good
    var thisIsMyObject = {};
    function thisIsMyFunction() {}
    var user = new User({
      name: 'Bob Parr'
    });
    ```

  - Use PascalCase when naming constructors or classes

    ```javascript
    // bad
    function user(options) {
      this.name = options.name;
    }

    var bad = new user({
      name: 'nope'
    });

    // good
    function User(options) {
      this.name = options.name;
    }

    var good = new User({
      name: 'yup'
    });
    ```

  - Use a leading underscore `_` when naming private properties

    ```javascript
    // bad
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';

    // good
    this._firstName = 'Panda';
    ```

  - When saving a reference to `this` use `_this`.

    ```javascript
    // bad
    function() {
      var self = this;
      return function() {
        console.log(self);
      };
    }

    // bad
    function() {
      var that = this;
      return function() {
        console.log(that);
      };
    }

    // good
    function() {
      var _this = this;
      return function() {
        console.log(_this);
      };
    }
    ```

  - Name your functions. This is helpful for stack traces.

    ```javascript
    // bad
    var log = function(msg) {
      console.log(msg);
    };

    // good
    var log = function log(msg) {
      console.log(msg);
    };
    ```

**[⬆ back to top](#table-of-contents)**


## Accessors

  - Accessor functions for properties are not required
  - If you do make accessor functions use getVal() and setVal('hello')

    ```javascript
    // bad
    dragon.age();

    // good
    dragon.getAge();

    // bad
    dragon.age(25);

    // good
    dragon.setAge(25);
    ```

  - If the property is a boolean, use isVal() or hasVal()

    ```javascript
    // bad
    if (!dragon.age()) {
      return false;
    }

    // good
    if (!dragon.hasAge()) {
      return false;
    }
    ```

  - It's okay to create get() and set() functions, but be consistent.

    ```javascript
    function Jedi(options) {
      options || (options = {});
      var lightsaber = options.lightsaber || 'blue';
      this.set('lightsaber', lightsaber);
    }

    Jedi.prototype.set = function(key, val) {
      this[key] = val;
    };

    Jedi.prototype.get = function(key) {
      return this[key];
    };
    ```

**[⬆ back to top](#table-of-contents)**

## Constructors

  - Assign methods to the prototype object, instead of overwriting the prototype with a new object. Overwriting the prototype makes inheritance impossible: by resetting the prototype you'll overwrite the base!

    ```javascript
    function Jedi() {
      console.log('new jedi');
    }

    // bad
    Jedi.prototype = {
      fight: function fight() {
        console.log('fighting');
      },

      block: function block() {
        console.log('blocking');
      }
    };

    // good
    Jedi.prototype.fight = function fight() {
      console.log('fighting');
    };

    Jedi.prototype.block = function block() {
      console.log('blocking');
    };
    ```

  - Methods can return `this` to help with method chaining.

    ```javascript
    // bad
    Jedi.prototype.jump = function() {
      this.jumping = true;
      return true;
    };

    Jedi.prototype.setHeight = function(height) {
      this.height = height;
    };

    var luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20) // => undefined

    // good
    Jedi.prototype.jump = function() {
      this.jumping = true;
      return this;
    };

    Jedi.prototype.setHeight = function(height) {
      this.height = height;
      return this;
    };

    var luke = new Jedi();

    luke.jump()
      .setHeight(20);
    ```


  - It's okay to write a custom toString() method, just make sure it works successfully and causes no side effects.

    ```javascript
    function Jedi(options) {
      options || (options = {});
      this.name = options.name || 'no name';
    }

    Jedi.prototype.getName = function getName() {
      return this.name;
    };

    Jedi.prototype.toString = function toString() {
      return 'Jedi - ' + this.getName();
    };
    ```

**[⬆ back to top](#table-of-contents)**

## License

  (The MIT License)

  Copyright (c) 2014 Airbnb

  Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

  The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

  THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Reference

  - [RisingStack](https://github.com/RisingStack/node-style-guide)

**[⬆ back to top](#table-of-contents)**
