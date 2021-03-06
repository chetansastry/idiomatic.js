# Principles of Writing Consistent, Idiomatic JavaScript


## All code in any code-base should look like a single person typed it, no matter how many people contributed.

> ### "Arguments over style are pointless. There should be a style guide, and you should follow it"
>_Rebecca_ _Murphey_

&nbsp;

> ### "Part of being a good steward to a successful project is realizing that writing code for yourself is a Bad Idea™. If thousands of people are using your code, then write your code for maximum clarity, not your personal preference of how to get clever within the spec."
>_Idan_ _Gazit_


## Important, Non-Idiomatic Stuff:

### Code Quality Tools, Resources & References

 * [JavaScript Plugin](http://docs.codehaus.org/display/SONAR/JavaScript+Plugin) for [Sonar](http://www.sonarsource.org/)
 * [Plato](https://github.com/jsoverson/plato)
 * [jsPerf](http://jsperf.com/)
 * [jsFiddle](http://jsfiddle.net/)
 * [jsbin](http://jsbin.com/)
 * [JavaScript Lint (JSL)](http://javascriptlint.com/)
 * [jshint](http://jshint.com/)
 * [jslint](http://jslint.org/)

## Get Smart

### [Annotated ECMAScript 5.1](http://es5.github.com/)
### [EcmaScript Language Specification, 5.1 Edition](http://ecma-international.org/ecma-262/5.1/)

The following should be considered 1) incomplete, and 2) *REQUIRED READING*. I don't always agree with the style written by the authors below, but one thing is certain: They are consistent. Furthermore, these are authorities on the language.

 * [Baseline For Front End Developers](http://rmurphey.com/blog/2012/04/12/a-baseline-for-front-end-developers/)
 * [Eloquent JavaScript](http://eloquentjavascript.net/)
 * [JavaScript, JavaScript](http://javascriptweblog.wordpress.com/)
 * [Adventures in JavaScript Development](http://rmurphey.com/)
 * [Perfection Kills](http://perfectionkills.com/)
 * [Douglas Crockford's Wrrrld Wide Web](http://www.crockford.com)
 * [JS Assessment](https://github.com/rmurphey/js-assessment)
 * [Leveraging Code Quality Tools by Anton Kovalyov](http://anton.kovalyov.net/slides/gothamjs/)




### Build & Deployment Process

Projects should always attempt to include some generic means by which source can be linted, tested and compressed in preparation for production use. For this task, [grunt](https://github.com/gruntjs/grunt) by Ben Alman is second to none and has officially replaced the "kits/" directory of this repo.




### Test Facility

Projects _must_ include some form of unit, reference, implementation or functional testing. Use case demos DO NOT QUALIFY as "tests". The following is a list of test frameworks, none of which are endorsed more than the other.

 * [QUnit](http://github.com/jquery/qunit)
 * [Jasmine](https://github.com/pivotal/jasmine)
 * [Vows](https://github.com/cloudhead/vows)
 * [Mocha](https://github.com/visionmedia/mocha)
 * [Hiro](http://hirojs.com/)
 * [JsTestDriver](https://code.google.com/p/js-test-driver/)
 * [Buster.js](http://busterjs.org/)
 * [Sinon.js](http://sinonjs.org/)

## Table of Contents

 * [Whitespace](#whitespace)
 * [Beautiful Syntax](#spacing)
 * [Type Checking](#type)
 * [Conditional Evaluation](#cond)
 * [Practical Style](#practical)
 * [Naming](#naming)
 * [Misc](#misc)
 * [Comments](#comments)
 * [One Language Code](#language)



------------------------------------------------


## Preface

The following sections outline a _reasonable_ style guide for modern JavaScript development and are not meant to be prescriptive. The most important take-away is the **law of code style consistency**. Whatever you choose as the style for your project should be considered law. Link to this document as a statement of your project's commitment to code style consistency, readability and maintainability.





## Idiomatic Style Manifesto


1. <a name="whitespace">Whitespace</a>
  - Indent with tabs, align with spaces.
      - Use tabs to indent your code.
      - Use spaces only to align documentation, so that they stay lined up irrespective of tab sizes.
      - Never mix tabs and spaces.
  - If your editor supports it, always work with the "show invisibles" setting turned on. The benefits of this practice are:
      - Enforced consistency
      - Eliminating end of line whitespace
      - Eliminating blank line whitespace
      - Commits and diffs that are easier to read


2. <a name="spacing">Beautiful Syntax</a>

    A. Parens, Braces, Linebreaks

    ```javascript

    // if/else/for/while/try always have spaces, braces and span multiple lines
    // this encourages readability

    // 2.A.1.1
    // Examples of really cramped syntax

    if(condition) doSomething();

    while(condition) iterating++;

    for(var i=0;i<100;i++) someIterativeFn();


    // 2.A.1.1
    // Use whitespace to promote readability

    if (condition) {
      // statements
    }

    while (condition) {
      // statements
    }

    for (var i = 0; i < 100; i++) {
      // statements
    }

    // Even better:

    var i,
      length = 100;

    for (i = 0; i < length; i++) {
      // statements
    }

    // Or...

    var i = 0,
      length = 100;

    for (; i < length; i++) {
      // statements
    }

    var prop;

    for (prop in object) {
      // statements
    }


    if (true) {
      // statements
    } else {
      // statements
    }
    ```


    B. Assignments, Declarations, Functions ( Named, Expression, Constructor )

    ```javascript

    // 2.B.1.1
    // Variables
    var foo = "bar",
      num = 1,
      undef;

    // Literal notations:
    var array = [],
      object = {};


    // 2.B.1.2
    // Using only one `var` per scope (function) promotes readability
    // and keeps your declaration list free of clutter (also saves a few keystrokes)

    // Bad
    var foo = "";
    var bar = "";
    var qux;

    // Good
    var foo = "",
      bar = "",
      quux;

    // or..
    var // Comment on these
    foo = "",
    bar = "",
    quux;

    // 2.B.1.3
    // var statements should always be in the beginning of their respective scope (function).
    // Same goes for const and let from ECMAScript 6.

    // Bad
    function foo() {

      // some statements here

      var bar = "",
        qux;
    }

    // Good
    function foo() {
      var bar = "",
        qux;

      // all statements after the variables declarations.
    }
    ```

    ```javascript

    // 2.B.2.1
    // Named Function Declaration
    function foo(arg1, argN) {

    }

    // Usage
    foo(arg1, argN);


    // 2.B.2.2
    // Named Function Declaration
    function square(number) {
      return number * number;
    }

    // Usage
    square(10);

    // Really contrived continuation passing style
    function square(number, callback) {
      callback(number * number);
    }

    square(10, function(square) {
      // callback statements
    });


    // 2.B.2.3
    // Function Expression
    var square = function(number) {
      // Return something valuable and relevant
      return number * number;
    };

    // Function Expression with Identifier
    // This preferred form has the added value of being
    // able to call itself and have an identity in stack traces:
    var factorial = function factorial(number) {
      if (number < 2) {
        return 1;
      }

      return number * factorial(number - 1);
    };


    // 2.B.2.4
    // Constructor Declaration
    function FooBar(options) {

      this.options = options;
    }

    // Usage
    var fooBar = new FooBar({ a: "alpha" });

    fooBar.options;
    // { a: "alpha" }

    ```


    C. Consistency Always Wins

    In sections 2.A-2.C, the whitespace rules are set forth as a recommendation with a simpler, higher purpose: consistency.
    It's important to note that formatting preferences, such as "inner whitespace" should be considered optional, but only one style should exist across the entire source of your project.

    ```javascript

    // 2.D.1.1

    if (condition) {
      // statements
    }

    while (condition) {
      // statements
    }

    for (var i = 0; i < 100; i++) {
      // statements
    }

    if (true) {
      // statements
    } else {
      // statements
    }

    ```

    D. Quotes

    Use only single quotes for strings for the sake of consistency. 

    F. End of Lines and Empty Lines

    Whitespace can ruin diffs and make changesets impossible to read. Consider incorporating a pre-commit hook that removes end-of-line whitespace and blanks spaces on empty lines automatically.

3. <a name="type">Type Checking (Courtesy jQuery Core Style Guidelines and Underscore.js)</a>

    A. Actual Types

    String:

        _.isString(variable)

    Number:

        _.isNumber(variable)

    Boolean:

        _.isBoolean(variable)

    Object:

        _.isObject(variable)

    Array:

        _.isArray(arrayLikeObject)

    Node:

        elem.nodeType === 1

    null:

        _.isNull(variable)

    null or undefined:

        _.isNull(variable) || _.isUndefined(variable)

    undefined:

      Global Variables:

        typeof variable === "undefined"

      Local Variables and properties:

        _.isUndefined(variable)
        _.isUndefined(object.prop)

    B. Coerced Types

    Avoid implicit type coercion. Use only `===` and `!==` for comparison. Prefer `parseInt(value, 10)` or `parseFloat(value)` to unary + or - operators.


4. <a name="cond">Conditional Evaluation</a>

    ```javascript

    // 4.1.1
    // When only evaluating that an array has length,
    // instead of this:
    if (array.length > 0) ...

    // ...evaluate truthiness, like this:
    if (array.length) ...


    // 4.1.2
    // When only evaluating that an array is empty,
    // instead of this:
    if (array.length === 0) ...

    // ...evaluate truthiness, like this:
    if (!array.length) ...


    // 4.1.3
    // When only evaluating that a string is not empty,
    // instead of this:
    if (string !== "") ...

    // ...evaluate truthiness, like this:
    if (string) ...


    // 4.1.4
    // When only evaluating that a string _is_ empty,
    // instead of this:
    if (string === "") ...

    // ...evaluate falsy-ness, like this:
    if (!string) ...


    // 4.1.5
    // When only evaluating that a reference is true,
    // instead of this:
    if (foo === true) ...

    // ...evaluate like you mean it, take advantage of built in capabilities:
    if (foo) ...


    // 4.1.6
    // When evaluating that a reference is false,
    // instead of this:
    if (foo === false) ...

    // ...use negation to coerce a true evaluation
    if (!foo) ...

    // ...Be careful, this will also match: 0, "", null, undefined, NaN
    // If you _MUST_ test for a boolean false, then use
    if (foo === false) ...


    ```
    ALWAYS evaluate for the best, most accurate result - the above is a guideline, not a dogma.

5. <a name="practical">Practical Style</a>

    ```javascript

    // 5.1.1
    // A Practical Module

    define('path/to/module', ['path/to/dep1', 'path/to/dep2'], function(dep1, dep2) {

      var data = "secret";

      // Other things might happen here

      // expose our module to the global object
      return {
        // This is some boolean property
        bool: true,
        // Some string value
        string: "a string",
        // An array property
        array: [ 1, 2, 3, 4 ],
        // An object property
        object: {
          lang: "en-Us"
        },
        getData: function() {
          // get the current value of `data`
          return data;
        },
        setData: function(value) {
          // set the value of `data` and return it
          return (data = value);
        }
      };

    });

    ```

    ```javascript

    // 5.2.1
    // A Practical Constructor

    define('path/to/module', ['path/to/dep1', 'path/to/dep2'], function(dep1, dep2) {

      function Ctor(foo) {

        this.foo = foo;

      }

      Ctor.prototype.getFoo = function() {
        return this.foo;
      };

      Ctor.prototype.setFoo = function(val) {
        return (this.foo = val);
      };

      // expose our constructor to the global object
      return Ctor;

    });

    ```



6. <a name="naming">Naming</a>



    A. You are not a human code compiler/compressor, so don't try to be one.

    The following code is an example of egregious naming:

    ```javascript

    // 6.A.1.1
    // Example of code with poor names

    function q(s) {
      return document.querySelectorAll(s);
    }
    var i,a=[],els=q("#foo");
    for(i=0;i<els.length;i++){a.push(els[i]);}
    ```

    Without a doubt, you've written code like this - hopefully that ends today.

    Here's the same piece of logic, but with kinder, more thoughtful naming (and a readable structure):

    ```javascript

    // 6.A.2.1
    // Example of code with improved names

    function query(selector) {
      return document.querySelectorAll(selector);
    }

    var idx = 0,
      elements = [],
      matches = query("#foo"),
      length = matches.length;

    for (; idx < length; idx++) {
      elements.push(matches[ idx ]);
    }

    ```

    A few additional naming pointers:

    ```javascript

    // 6.A.3.1
    // Naming strings

    `dog` is a string


    // 6.A.3.2
    // Naming arrays

    `dogs` is an array of `dog` strings


    // 6.A.3.3
    // Naming functions, objects, instances, etc

    camelCase; function and var declarations


    // 6.A.3.4
    // Naming constructors, prototypes, etc.

    PascalCase; constructor function


    // 6.A.3.5
    // From the Google Closure Library Style Guide

    functionNamesLikeThis;
    variableNamesLikeThis;
    ConstructorNamesLikeThis;
    EnumNamesLikeThis;
    methodNamesLikeThis;
    SYMBOLIC_CONSTANTS_LIKE_THIS;

    ```

    B. Faces of `this`

    Beyond the generally well known use cases of `call` and `apply`, always prefer `_.bind(fn, this)`, for creating `BoundFunction` definitions for later invocation. Only resort to aliasing when no preferable option is available.

    ```javascript
    // 6.B.2

    // eg. lodash/underscore, _.bind()
    function Device(opts) {

      this.value = null;

      stream.read(opts.path, _.bind(function(data) {

        this.value = data;

      }, this));

      setInterval(_.bind(function() {

        this.emit("event");

      }, this), opts.freq || 100);
    }

    ```

    As a last resort, create an alias to `this` using `self` as an Identifier. This is extremely bug prone and should be avoided whenever possible.

    ```javascript

    // 6.B.3

    function Device(opts) {
      var self = this;

      this.value = null;

      stream.read(opts.path, function( data) {

        self.value = data;

      });

      setInterval(function() {

        self.emit("event");

      }, opts.freq || 100);
    }

    ```


    C. Use `thisArg`

    Several Array methods of underscore.js support `thisArg` signature, which should be used whenever possible

    ```javascript

    // 6.C.1

    var obj;

    obj = { f: "foo", b: "bar", q: "qux" };

    _.forEach(_.keys(obj), function(key) {

      // |this| now refers to `obj`

      console.log(this[ key ]);

    }, obj ); // <-- the last arg is `thisArg`

    // Prints...

    // "foo"
    // "bar"
    // "qux"

    ```

7. <a name="misc">Misc</a>

    This section will serve to illustrate ideas and concepts that should not be considered dogma, but instead exists to encourage questioning practices in an attempt to find better ways to do common JavaScript programming tasks.

    A. Early returns promote code readability with negligible performance difference

    ```javascript

    // 7.B.1.1
    // Bad:
    function returnLate(foo) {
      var ret;

      if (foo) {
        ret = "foo";
      } else {
        ret = "quux";
      }
      return ret;
    }

    // Good:

    function returnEarly(foo) {

      if (foo) {
        return "foo";
      }
      return "quux";
    }

    ```

8. <a name="comments">Comments</a>

    #### Single line above the code that is subject
    #### Multiline is good
    #### JSDoc style is good, but requires a significant time investment


9. <a name="language">One Language Code</a>

    Programs should be written in one language, whatever that language may be, as dictated by the maintainer or maintainers.


----------


<a rel="license" href="http://creativecommons.org/licenses/by/3.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by/3.0/80x15.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Principles of Writing Consistent, Idiomatic JavaScript</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/rwldrn/idiomatic.js" property="cc:attributionName" rel="cc:attributionURL">Rick Waldron and Contributors</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/3.0/deed.en_US">Creative Commons Attribution 3.0 Unported License</a>.<br />Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/rwldrn/idiomatic.js" rel="dct:source">github.com/rwldrn/idiomatic.js</a>.
