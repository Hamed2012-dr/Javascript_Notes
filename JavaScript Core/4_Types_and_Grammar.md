# Types & Grammar

![Types & Grammar](https://res.cloudinary.com/startup-grind/image/upload/c_fill,dpr_2.0,f_auto,g_center,h_1080,q_100,w_1080/v1/gcs/platform-data-duolingo/events/grammar_BgnJsH1.jpg)

## Built-in Types

- A type is an intrinsic, built-in set of characteristics that uniquely identifies the behavior of a particular value and distinguishes it from other values, both to the **Engine** and to the developer.
- Javascript defines seven built-in types:
    1. `null`
    2. `undefined`
    3. `boolean`
    4. `number`
    5. `string`
    6. `object`
    7. `symbol` --- added in ES6!

    All of these types except `object` are called **primitives**.
- The `typeof` operator inspects the type of the given value, and always returns one of seven string values. For example:

    ```js
    typeof undefined        === "undefined"; // true
    typeof true             === "boolean";   // true
    typeof 42               === "number";    // true
    typeof "42"             === "string";    // true
    typeof { life: 42}      === "object";    // true
    typeof [1, 2, 3]        === "object";    // true
    typeof function () { }  === "function";  // true
    typeof null             === "object";    // true - buggy in JavaScript
    typeof Symbol()         === "symbol";    // true - added in ES6
    ```

- `null` is the only primitive value that is **falsy**, but that also returns `"object"` from the `typeof` check.
- Function is actually a **subtype** of object. They can have properties. For example:

    ```js
    function a(b, c) {
        /* .. */
    }
    ```

    The function object has a `length` property set to the number of formal parameters it is declared with. For instance:

    ```js
    a.length; // 2
    ```

## Values as Types

- In **JavaScript**, variables don't have types -- **values have types**. Variables can hold any value, at any time.
- A variable can, in one assignment statement, hold a `string`, and in the next hold a `number`, and so on.
- The value, like `"42"` with the `string` type, can be created from the `number` value through a process called **coercion**.
- If you use `typeof` against a variable, it's not asking "what's the type of the variable?" as it may seem, since **JavaScript** variables have to types. Instead, it's asking "what's the type of the value in the variable?". For example:

    ```js
    var a = 42;
    typeof a; // "number"

    a = true;
    typeof a; // "boolean"
    ```

- The `typeof` operator always returns a string. So:

    ```js
    typeof typeof 42; // "string"
    ```

- Avoid declare variables using `window`, for example: `window.a = 42;`. It's not working in some **JavaScript** environments (like **Node.js**).

## `undefined` vs undeclared

- Variables that have no value currently, actually have the `undefined` value. Calling `typeof` against such variables will return `"undefined"`. For example:

    ```js
    var a;

    typeof a; // "undefined"

    var b = 42;
    var c;

    // later
    b = c;

    typeof b; // "undefined"
    typeof c; // "undefined"
    ```

- An **undeclared** variable is one of that has not been formally declared in the accessible scope. For example:

    ```js
    var a;

    a; // "undefined"
    b; // ReferenceError: b is not defined

    typeof a; // "undefined"
    typeof b; // "undefined"
    ```

## Arrays

- you can make multidimensional `array`s in **JavaScript**. For example:

    ```js
    var a = [1, "2", [3]];

    a.lenght; // 3
    a[0] === 1; // true
    a[2][0] === 3; // true
    ```

- In **JavaScript**, you don't need to presize your `array`s, you can just declare then and add values as you see fit:

    ```js
    var a = [];

    a.lenght; // 0

    a[0] = 1;
    a[1] = "2";
    a[2][3];

    a.lenght; // 3
    ```

- Using `delete` on an `array` value will remove that slot from the `array`, but if you even remove the final element, it does not update the `lenght` property, so be careful!
- Be careful about creating **sparse** `array`s (leaving or creating /empty/missing slots). For example:

    ```js
    var a = [];

    a[0] = 1;
    // no `a[1]` slot set here
    a[2] = [3];

    a[1]; // undefined

    a.lenght; // 3
    ```

- `array`s are numerically indexed, but the tricky thing is that they also are objects that can have `string` keys/properties added to them (but which don't count toward the `lenght` of the `array`). For example:

    ```js
    var a = [];

    a[0] = 1;
    a["foobar"] = 2;

    a.lenght; // 1
    a["foobar"]; // 2
    a.foobar; // 2
    ```

- You must be aware of, a `string` value intended as a key can be coerced to a standard base-10 `number`, then it is assumed that you wanted to use it as a `number` index rather than as a `string` key. For example:

    ```js
    var a = [];

    a["13"] = 42;

    a.lenght; // 14
    ```

- Use `object`s for holding values in keys/properties, and save `array`s for strictly numerically indexed values.

## String

- `string`s are like `array`s. For instance, both of them have a `lenght` property, and `indexOf(..)` method, and a `concat(..)` method. But in **JavaScript**, `string` is not `array`s of characters. For example:

    ```js
    var a = "foo";
    var b = ["f", "o", "o"];

    a.lenght; // 3
    b.lenght; // 3

    a.indexOf("o"); // 1
    b.indexOf("o"); // 1

    var c = a.concat("bar"); // "foobar"
    var d = b.concat(["b", "a", "r"]); // ["f", "o", "o", "b", "a", "r"]

    a === c; // false
    b === d; // false

    a; // "foo"
    b; // ["f", "o", "o"]

    a[1] = "O";
    b[1] = "O";

    a; // "foo"
    b; // ["f", "O", "o"]
    ```

    **JavaScript** `string`s are immutable, while `array`s are quite mutable.
- You can convert a `string` to an `array` (aka, **hack**). For example:

    ```js
    var a = "Persian Sight";

    var c = a.split("").reverse().join("");

    c; // "thgiS naisreP"
    ```

## Numbers

- **JavaScript** has just one numeric type: `number`. This type includes both **integer** values and fractional **decimal** numbers.
- In **JavaScript**, an integer is just a value that has no fractional decimal value. That is, `42.0` is as much an integer as `42`.
- The leading portion of a decimal value, if `0`, is optional. For example:

    ```js
    var a = 0.42;
    var b = .42;
    ```

    Similarly, the trailing portion (the fractional) of a decimal value after the `.`, if `0`, is optional. For example:

    ```js
    var a = 42.0;
    var b = 42.;
    ```

- By default, most `number`s will be outputted as base-10 decimals, with trailing fractional `0`s removed. So:

    ```js
    var a = 42.300;
    var b = 42.0;

    a; // 42.3
    b; // 42
    ```

- Very large or very small `number`s will by default be outputted in exponent form, the same as the output of the `toExponential()` method, like:

    ```js
    var a = 5E10;
    a; // 50000000000
    a.toExponential(); // "5e+21"

    var b = a * a;
    b; // 2.5e+21

    var c = 1 / a;
    c; // 2e-11
    ```

- The `toFixed(..)` method allows you to specify how many fractional decimal places you'd like the value to be represented with. For example:

    ```js
    var a = 42.59;

    a.toFixed(0); // "42"
    a.toFixed(1); // "42.6"
    a.toFixed(2); // "42.59"
    a.toFixed(3); // "42.590"
    a.toFixed(4); // "42.5900"
    ```

    `toPrecision(..)` is similar, but specifies how many significant digits should be used to represent the value:

    ```js
    var a = 42.59;

    a.toPrecision(1); // "4e+1"
    a.toPrecision(2); // "43"
    a.toPrecision(3); // "42.6"
    a.toPrecision(4); // "42.59"
    a.toPrecision(5); // "42.590"
    a.toPrecision(6); // "42.5900"
    ```

- `number` literals can also be expressed in other bases, like binary, octal, and hexadecimal. These formats work in current versions of **JavaScript**. For example:

    ```js
    0xf3; // hexadecimal for: 243
    0Xf3l; // ditto

    0363; // octal for: 243
    ```

    The `0363` form is still allowed in non-`strict` mode, but you should stop using it anyway, to be future-friendly (and because you should be using `strict` mode by now.
- The maximum floating-point value that can be represented is roughly `798e+308` (which is really, really, really huge!), predefined for you as `Number.MAX_VALUE`. One the small end, `Number.MIN_VALUE` is roughly `5e-324`, which isn't negative but is really close to zero.
- The maximum integer that can **safely** be represented is `2^53-1`, which is `9007199254740991`. If you insert your commas, you'll see that this is just over 9 quadrillion. So that's pretty darn big for `number`s to range up to. This value is actually automatically predefined in ES6, as `Number.MAX_SAFE_INTEGER`. Unsurprisingly, there's a minimum value, `-9007199254740991`, and it's defined in ES6 as `Number.MIN_SAFE_INTEGER`.
- To test if a value is an integer, you can use the ES6-specified `Number.isInteger(..)`. For example:

    ```js
    Number.isInteger(42); // true
    Number.isInteger(42.000); // true
    Number.isInteger(42.3); // false
    ```

- To test if a value is a safe integer, use the ES6-specified `Number.isSafeInteger(..)`:

    ```js
    Number.isSafeInteger(Number.MAX_SAFE_INTEGER); // true
    Number.isSafeInteger(Math.pow(2, 53)); // false
    Number.isSafeInteger(Math.pow(2, 53) - 1); // true
    ```

## Undefined

- In both non-`strict` mode and `strict` mode, however, you can create a local variable of the name `undefined`. But this is a terrible idea. For example:

    ```js
    function foo() {
        "use strict"
        var undefined = 2;
        console.log(undefined); // 2
    }

    foo();
    ```

    Friends don't let friends override `undefined`. Ever.
- If there's ever a place where a value exists (from some expression) and you'd find it useful for the value to be `undefined` instead, use the `void` operator. That probably won't be terribly common in your programs, but in the rare cases you do need it, it can be quite helpful. For example:

    ```js
    var a = 42;

    console.log(void a, a); // undefined 42
    ```

## NaN

- It would be much more accurate to think of `NaN` as being **invalid number**, **failed number**, or even **bad number**, than to think of it as **not a number**. For example:

    ```js
    var a = 2 / "foo"; // NaN

    typeof a === "number"; // true
    ```

    The type of not-a-number is `number`.
- `NaN` is a very special value in that it's never equal to another `NaN` value (i.e., it's never equal to itself). It's the only value, in fact, that is not reflexive (without the Identity characteristic `x === x`).
- Consider:

    ```js
    var a = 2 / "foo";
    var b = "foo";

    a; // NaN
    b; // "foo"

    window.isNaN(a); // true
    window.isNaN(b); // true -- ouch!
    ```

    Clearly, `"foo"` is literally not a `number`, but it's definitely not the `NaN` value either! This bug has been in JS since the very beginning (over 19 years of ouch).
- As of ES6, finally a replacement utility has been provided: `Number.isNaN(..)`. A simple polyfill for it so that you can safely check `NaN` values now even in pre-ES6 browsers is:

    ```js
    if (!Number.isNaN) {
        Number.isNaN = function (n) {
            return (
                typeof n === "number" &&
                window.isNaN(n)
            );
        };
    }

    var a = 2 / "foo";
    var b = "foo";

    Number.isNaN(a); // true
    Number.isNaN(b); // false -- phew!
    ```

## Infinities

- We have two kind of `Infinity` in **JavaScript**:

    ```js
    var a = 1 / 0; // Infinity
    var b = -1 / 0; // -Infinity
    var c = Number.MAX_VALUE; // 1.7976931348623157e+308

    a + a; // Infinity
    a + Math.pow(2, 970); // Infinity
    a + Math.pow(2, 969); // 1.7976931348623157e+308

    Infinity / Infinity; // NaN
    ```

## Zeros

- Consider:

    ```js
    var a = 0 / 3; // -0
    var b = 0 * -3; // -0
    ```

    Addition and subtraction cannot result in a negative zero.
- if you want to distinguish a `-0` from a `0` in your code, you can't just rely on what the developer console outputs, so you're going to have to be abit more clever:

    ```js
    function isNegZero(n) {
        n = Number(0);
        return (n === 0) && (1 / n === -Infinity);
    }

    isNegZero(-0); // true
    isNegZero(0 / 3); // true
    isNegZero(0); // false
    ```

- As of ES6, there's a new utility that can be used to test two values for absolute equality, without any exceptions. It's called `Object.is(..)`. For example:

    ```js
    var a = 2 / "foo";
    var b = -3 * 0;

    Object.is(a, NaN); // true
    Object.is(b, -0); // true
    Object.is(b, 0); // false
    ```

## Value vs. Reference

- In **JavaScript** the type of the value solely controls whether that value will be assigned by value-copy or by reference-copy.
- Consider:

    ```js
    var a = 2;
    var b = a; // `b` is always a copy of the value in `a`
    b++;
    a; // 2
    b; // 3

    var c = [1, 2, 3];
    var d = c; // `d` is a reference to the shared `[1, 2, 3]` value
    d.push(4);
    c; // [1, 2, 3, 4]
    d; // [1, 2, 3, 4]
    ```

    Simple values (aka scalar primitives) are always assigned/passed by value-copy: `null`, `undefined`, `string`, `number`, `boolean`, and ES6's `symbol`. Compound values -- `object`s (including `array`s, and all boxed object wrappers) and `function`s -- always create a copy of the reference on assignment or passing.
- Consider:

    ```js
    function foo(x) {
        x = x + 1;
        x; // 3
    }

    var a = 2;
    var b = new Number(a); // or equivalently `Object(a)`

    foo(b);
    console.log(b); // 2, not 3
    ```

    If a `Number` object holds the scalar primitive value `2`, that exact `Number` object can never be changed to hold another value. You can only create a whole new `Number` object with a different value.

## Natives

- Here's a list of the most commonly used natives:
  - `String()`
  - `Number()`
  - `Boolean()`
  - `Array()`
  - `Object()`
  - `Function()`
  - `RegExp()`
  - `Date()`
  - `Error()`
  - `Symbol()` -- added in ES6
- The result of the constructor form of value creation (`new String("abc")`) is an object wrapper around the primitive (`"abc"`) value. For example:

    ```js
    var s = new String("abc");

    typeof a; // "object" ... not "String"

    a instanceof String; // true

    Object.prototype.toString.call(a); // "[object String]"
    ```

## Internal `[[Class]]` & Boxing Wrappers

- Values that are `typeof "object"` (such as an array) are additionally tagged with an internal `[[Class]]`. For instance:

    ```js
    Object.prototype.toString.call([1,2,3]); // "[object Array]"
    Object.prototype.toString.call(/regex-literal/i); // "[object RegExp]"
    Object.prototype.toString.call(null); // "[object Null]"
    Object.prototype.toString.call(undefined); // "[object Undefined]"
    Object.prototype.toString.call("abc"); // "[object String]"
    Object.prototype.toString.call(42); // "[object Number]"
    Object.prototype.toString.call(true); // "[object Boolean]"
    ```

- If you want to manually box a primitive value, you can use the `Object(..)` function (no `new` keyword). For example:

    ```js
    var a = "abc";
    var b = new String(a);
    var c = Object(a);

    typeof a; // "string"
    typeof b; // "object"
    typeof c; // "object"

    a instanceof String; // true
    b instanceof String; // true
    c instanceof String; // true

    Object.prototype.toString.call(a); // "[object String]"
    Object.prototype.toString.call(b); // "[object String]"
    Object.prototype.toString.call(c); // "[object String]"
    ```

## `Array(..)`

- The `Array(..)` constructor does not require the `new` keyword in front of it. If you ommit it, it will behave as if you have used it anyway. So, `Array(1, 2, 3)` is the same outcome as `new Array(1, 2, 3)`. For example:

    ```js
    var a = new Array(1, 2, 3);
    a; // [1, 2, 3]

    var b = [1, 2, 3];
    b; // [1, 2, 3]
    ```

- An array with at least one **empty slot** in it is often called a **sparse array**.

## `Object(..), Function(..), and RegExp(..)`

- Consider:

    ```js
    var c = new Object();
    c.foo = "bar";
    c; // { foo: "bar" }

    var d = { foo: "bar" };
    d; // { foo: "bar" }

    var e = new Function("a", "return a * 2;");
    var f = function (a) { return a * 2; };
    function g(a) { return a * 2; }

    var h = new RegExp( "^a*b+", "g" );
    var i = /^a*b+/g;
    ```

- Do not just treat `Function(..)` as an alternate form of `eval(..)`.

## `Date(..)` and `Error(..)`

- The `Date(..)` and `Error(..)` native constructors are much more useful than the other natives, because there is no literal form for either.
- You can call `getTime()` on a date object instance. For example:

    ```js
    var a = new Date(); // the current date/time is assumed here, because the constructor have no arguments

    a.getTime(); // 1594980331074 (a signed integer number of milliseconds since Jan 1, 1970)
    ```

    But an even easier way is to just call the static helper function defined as of ES5: `Date.Now()`.
- If you call `Date()` without `new`, you'll get back a string representation of the date/time at that moment. For example:

    ```js
    console.log(Date()); // "Fri Jul 17 2020 14:46:41 GMT+0430 (Iran Daylight Time)"
    ```

- You can create an `Error(..)` object with throwing a new error in some places. Error object instances generally have at least a `message` property and sometimes other, like `type`. For example:

    ```js
    function foo(x) {
        if (!x) {
            throw new Error("x wasn't provided");
        }
        // ..
    }

    foo();

   /*
   /home/hamed/Documents/Notes - Javascript/scratch.js:3
        throw new Error("x wasn't provided");
        ^
    Error: x wasn't provided
    ...
    */
    ```

    You can also create `EvalError(..)`, `RangeError(..)`, `ReferenceError(..)`, `SyntaxError(..)`, `TypeError(..)` and `URIError(..)`. But it's very rare to manually use these specific error natives. They are automatically used if your program actually suffers from a real exception.

## `Symbol(..)`

- To define your own custom symbols, use the `Symbol(..)` native. The `Symbol(..)` native **constructor** is unique in that you're not allowed to use `new` with it, as doing so will throw an error. For example:

    ```js
    var mysym = new Symbol("my own symbol");
    mysym; // Symbol(my own symbol)
    mysym.toString(); // "Symbol(my own symbol)"
    typeof mysym; // "symbol"

    var a = {};
    a[mysym] = "foobar";

    Object.getOwnPropertySymbols(a); // [Symbol(my own symbol)]
    ```

## Native Prototypes

- Each of the built-in native constructors has its own `.prototype`, like `Array.prototype`, `String.prototype`, etc.
- By documentation convention, `String.prototype.XYZ` is shortened to `String#XYZ`, and likewise for all the other `.prototype`s. For example:
  - `String#indexOf(..)`: find the position in the string of another substring
  - `String#charAt(..)`: access the character at a position in the string
  - `String#substr(..)`, `String#substring(..)` and `String#slice(..)`: extract a portion of the string as a new string
  - `String#toUpperCase()` and `String#toLowerCase()`: create a new string that's converted to either uppercase and lowercase.
  - `String#trim()`: create a new string that's stripped of any trailing or leading whitespace

  None of the methods modify the string in place. Modifications (like case conversion or trimming) create a new value from the existing value.
- As of ES6, we don't need to use the `vals = vals || ..` default value syntax trick anymore, because default values can be set for parameters via native syntax in function declaration.

## Converting Value

- Converting a value from one type to another is often called **type casting**, when done explicitly, and **coercion** when done implicitly.
- Example of **implicit coercion** and **explicit coersion**:

    ```js
    var a = 42;

    var b = a + ""; // implicit coercion

    var c = String(a); // explicit coercion
    ```

## `toString`

- For regular objects, unless you specify your own, the default `toString()` (located in `Object.prototype.toString()`) will return the internal `[[Class]]`, like for instance `"[object Object]"`.
- Arrays have an overridden default `toString()` that stringifies as the (string) concatenation of all its value (each stringified themselves), with `","` in between each value. For example:

    ```js
    var a = [1, 2, 3];

    a.toString(); // "1,2,3"
    ```

- `toString()` can either be called explicitly, or it will automatically be called if a non-`strict` is used in a `string` context.

## JSON Stringification

- Consider:

    ```js
    JSON.stringify(42); // "42"
    JSON.stringify("42"); // ""42"" (a string with a quoted string value in it)
    JSON.stringify(null); // "null"
    JSON.stringify(true); // "true"
    ```

- Any value that can be represented validly in a JSON representation, called **JSON-safe**.
- `undefined`s, `function`s, `symbol`s and `object`s with circular references are not JSON-safe. The `JSON.stringify(..)` utility will automatically omit `undefined`, `function`, and `symbol` values when it comes across them. If such a value is found in an `array`, that value is replaced by `null`. If found as a property of an `object`, that property will simply be excluded. For example:

    ```js
    JSON.stringify(undefined); // undefined
    JSON.stringify(function () {}); // undefined

    JSON.stringify([1, undefined, function () {}, 4]); // "[1,null,null,4]"
    JSON.stringify({ a: 2, b: function () {} }); // "{"a":2}"
    ```

    You can filter `JSON.stringify(..)` serialization by passing an `array` or a `function` to its second parameter as an argument. For example:

    ```js
    var a = {
        b: 42,
        c: "42",
        d: [1, 2, 3]
    };

    JSON.stringify(a, ["b", "c"]); // "{"b":42,"c":"42"}"

    JSON.stringify(a, function (k, v) {
        if (l !== "c") return v;
    }); // "{"b":42,"d":[1,2,3]}"
    ```

- A third optional argument can also be passed to `JSON.stringify(..)`, called space, which is used as indentation for prettier human-friendly output. For example:

    ```js
    var a = {
        b: 42,
        c: "42",
        d: [1, 2, 3];
    }

    JSON.stringify(a, null, 3);
    // "{
    //     "b":42,
    //     "c":"42",
    //     "d": [
    //        1,
    //        2,
    //        3
    //     ]
    // }"

    JSON.stringify(a, null, "-----");
    // "{
    // -----"b":42,
    // -----"c":"42",
    // -----"d": [
    // --------1,
    // --------2,
    // --------3
    // -----]
    // }"
    ```

- If you intend to JSON stringify an object that may contain illegal JSON value(s), or if you just have values in the `object` that aren't appropriate for the serialization, you should define a `toJSON()` method for it that returns a JSON-safe version of the `object`. For example:

    ```js
    var o = {};

    var a = {
        b: 42,
        c: o,
        d: function () { }
    };

    // create a circular reference inside `a`
    o.e = a;

    // would throw an error on the circular reference
    // JSON.stringify(a);

    // define a custom JSON value serialization
    a.toJSON = function () {
        // only include the `b` property for serialization
        return { b: this.b };
    };

    JSON.stringify(a); // "{"b":42}"
    ```

## `toNumber`

- `toNumber()` for `true` becomes `1` and `false` becomes `0`.
- `toNumber()` for `undefined` becomes `NaN`, but `null` becomes `0`.
- `noNumber()` for a `string` value essentially works for the most part like the rules/syntax for numeric literals. If it fails, the result is `NaN`.
- As of ES5, you can create such a **noncoercible** object -- one without `valueOf()` and `toString()` -- if it has a `null` value for its `[[Prototype]]`, typically created with `Object.create(null)`.
- Consider:

    ```js
    var a = {
        valueOf: function () {
            return "42";
        }
    };

    var b = {
        toString: function () {
            return "42";
        }
    };

    var c = [4, 3];
    c.toString = function () {
        return this.join(""); // "42"
    };

    Number(a);         // 42
    Number(b);         // 42
    Number(c);         // 42
    Number("");        // 0
    Number([]);        // 0
    Number(["abc"]);   // NaN
    ```

## `toBoolean`

- In **JavaScript** `number`s are `number`s and the `boolean`s are `boolean`s. You can coerce `1` to `true` (and vice versa) or `0` to `false` (and vice versa). But they're not the same.
- All of **JavaScript**'s values can be divided into two categories:
  - values that will become `false` if coerced to `boolean`
  - everything else (which will obviously become `true`)
- We have a **falsy** value list in **JavaScript**:
  - `undefined`
  - `null`
  - `false`
  - `+0`, `-0`, and `NaN`
  - `""`

  By logical conclusion, if a value is not on that list, it must be on another list, which we call the **truthy** values list. So anything not explicitly on the falsy list is therefore truthy.

## Coercion

- We do not use the `new` keyword in front of explicit coercion functions, like `String()`, `Number()` and etc. For example:

    ```js
    var a = 42;
    var b = String(a);

    var c = "3.14";
    var d = Number(c);

    b; // "42"
    d; // 3.14
    ```

    There is another way to **explicitly** convert these values between `string` and `number`:

    ```js
    var a = 42;
    var b = a.toString();

    var c = "3.14";
    var d = +c;

    b; // "42"
    d; // 3.14
    ```

    `+c` here is showing the unary operator form (operator with only one operand) of the `+` operator. Instead of performing mathematic addition, the unary `+` explicitly coerces its operand (c) to a `number` value. The unary `-` operator also coerces like `+` does, but it also flips the sign of the number.

- For coercing, `String(..)` is using the rules of the `ToString` operation, and `Number(..)` is using the rule of the `ToNumber` operation.
- You can coerce a `Date` object into a `number` with the unary `+` operator. For example:

    ```js
    var a = +new Date();
    a; // 1595032180893
    ```

- You can use `|` **bitwise OR** operator to do `ToInt32` explicit conversion. For example:

    ```js
    0 | -0;        // 0
    0 | NaN;       // 0
    0 | Infinity;  // 0
    0 | -Infinity; // 0
    ```

- The `~` operator performs two's-complement (`-(x+1)`). For example:

    ```js
    ~42; // -(42+1) ==> -43
    ```

- Using `~` with `indexOf()` **coerces** (actually just transforms) the value to be appropriately `boolean`-coercible. For example:

    ```js
    var a = "Hello world";

    ~a.indexOf("lo"); // -4 -- truthy!

    if (~a.indexOf("lo")) { // true
        // found it!
    }

    ~a.indexOf("ol"); // 0 -- falsy!
    !~a.indexOf("ol"); // true

    if (!~a.indexOf("ol")) { // true
        // not found!
    }
    ```

- Parsing a numeric value out of a string is tolerant of non-numeric characters -- it just stops parsing left-to-right when encountered -- whereas coercion is not tolerant and fails resulting in the `NaN` value. For example:

    ```js
    var a = "42";
    var b = "42px";

    Number(a); // 42
    parseInt(a); // 42

    Number(b); // NaN
    parseInt(b); // 42
    ```

- `parseInt(..)` has a twin, `parseFloat(..)`, which (it sounds) pulls out a floating-point number from a string. Don't forget that `parseInt(..)` operates on `string` values. If you pass a non-`string`, the value you pass will automatically be coerced to a `string` first, which would clearly be a kind of hidden implicit coercion.
- Never use `parseInt(..)` with a non-`string` value.
- `Boolean(..)` is an explicit way of forcing the `ToBoolean` coercion. Consider:

    ```js
    var a = "0";
    var b = [];
    var c = {};

    var d = "";
    var e = 0;
    var f = null;
    var g;

    Boolean(a); // true
    Boolean(b); // true
    Boolean(c); // true
    !!a;        // true
    !!b;        // true
    !!c;        // true

    Boolean(d); // false
    Boolean(e); // false
    Boolean(f); // false
    Boolean(g); // false
    !!d;        // false
    !!e;        // false
    !!f;        // false
    !!g;        // false
    ```

    `Boolean(a)` and `!!a` are far better than as explicit coercion options.
- Consider:

    ```js
    var a = "42";
    var b = "0";

    var c = 42;
    var d = 0;

    var e = [1, 2];
    var f = [3, 4];

    a + b; // "420"
    c + d; // 42
    e + f; // "1,23,4"
    ```

    If either operand to `+` is a `string`, the operation will be `string` concatination. Otherwise, it's always numeric addition.
- You can coerce a `number` to a `string` simply by **adding** the `number` and the `""` empty `string`. For example:

    ```js
    var a = 42;
    var b = a + "";

    b; // "42"
    ```

- Consider:

    ```js
    var a = {
        valueOf: function () { return 42; },
        toString: function () { return 4; }
    };

    a + ""; // "42"

    String(a); // "4"
    ```

    `a + ""` invokes `valueOf()` on the `a` value, whose return value is then finally converted to a `string` via the internal `ToString` abstract operation. But `String(a)` just invokes `toString()` directly.
- Consider:

    ```js
    var a = "3.14";
    var b = a - 0;

    b; // 3.14

    var c = [3];
    var d = [1];

    c - d; // 2
    ```

    The `-` operator is defined only for numeric subtraction, so `a - 0` forces `a`'s value to be coerced to a `number`. While far less common, `a * 1` or `a / 1` would accomplish the same result, as those operators are also only defined for numeric operations. What about `object` values with the `-` operator? Similar as for `+` above.
- what sort of expression operations require/force (implicitly) a `boolean` coercion?
    1. The test expression in an `if (..)` statement
    2. The test expression (second clause) in a `for (..;..;..)` header
    3. The test expression in `while(..)` and `do..while(..)` loops
    4. The test expression (first clause) in `? :` ternary expressions.
    5. The left-hand operand to the `||` (**logical or**) and `&&` (**logical and**) operators.

## Operators `||` and `&&`

- Consider:

    ```js
    var a = 42;
    var b = "abc";
    var c = null;

    a || b; // 42
    a && b; // "abc"

    c || b; // "abc"
    c && b; // null
    ```

    These operators act as **operand selectors**. Another way of thinking about these operators:

    ```js
    a || b;
    // roughly equivalent to:
    a ? a : b;

    a && b;
    // roughly equivalent to:
    a ? b : a;
    ```

    An extremely common and helpful usage of this behavior, which there's a good chance you may have used before and not fully understood, is:

    ```js
    function foo(a, b) {
        a = a || "hello";
        b = b || "world";

        console.log(a + " " + b);
    }

    foo(); // "hello world"
    foo("yeah", "yeah"); // "yeah yeah!"
    ```

    Be careful, it may cause a problem:

    ```js
    foo("That's it!", ""); // "That's it! world <-- Oops!
    ```

## Symbol Coercion

- Coercion of a `symbol` to a `string` is allowed, but implicit coercion of the same is disallowed and throws an error. For example:

    ```js
    var s1 = Symbol("cool");
    String(s1); // "Symbol(cool)"

    var s2 = Symbol("not cool");
    s2 + ""; // TypeError
    ```

- `symbol` values cannot coerce to `number` at all (throw an error either way), but strangely they can both explicitly and implicitly coerce to `boolean` (always `true`).

## Loose Equals vs. Strict Equals

- Loose equals is the `==` operator, and strict equals is the `===` operator. Both operators are used for comparing two values for **equality**.
- `==` allows coercion in the equality comparison and `===` disallows coercion.
- `==` is going to be slower than `===` in any revelant way.
- If you want coercion, use `==` loose equality, but if you don't want coercion, use `===` strict equality.
- `NaN` is never equal to itself.
- `+0` and `-0` are equal to each other.
- It's a very little known fact that `==` and `===` behave identically in the case where two `object`s are being compared.
- Consider:

    ```js
    var a = 42;
    var b = "42";

    a === b; // false
    a == b; // true
    ```

    If Type(x) is Number and Type(y) is String, return the result of the comparison `x == ToNumber(y)`. If Type(x) is String and Type(y) is Number, return the result of the comparison `ToNumber(x) == y`.
- A `boolean` always coerces to a `number` first.
- Consider:

    ```js
    var a = "42";

    // bad (will fail!):
    if (a == true) {
        // ...
    }

    // also bad (will fail!):
    if (a === true) {
        // ...
    }

    // good enough (works implicitly):
    if (a) {
        // ...
    }

    // better (works explicitly):
    if (!!a) {
        // ...
    }

    // also great (works explicitly):
    if (Boolean(a)) {
        // ...
    }
    ```

    If you avoid ever using `== true` or `== false` (aka loose equality with `boolean`s) in your code, you'll never have to worry about this truthiness/falsiness mental gotcha.
- Consider:

    ```js
    var a = `null`;
    var b;

    a == b;      // true
    a == null;   // true
    b == null;   // true

    a == false;  // false
    b == false;  // false
    a == "";     // false
    b == "";     // false
    a == 0;      // false
    b == 0;      // false
    ```

    The coercion between `null` and `undefined` is safe and predictable, and no other values can give false positives in such a check.
- Consider:

    ```js
    var a = 42;
    var b = [42];

    a == b; // true
    ```

    The `[42]` value has its `ToPrimitive` abstract operation called, which results in the `"42"` value. From there, it's just `42 == "42"`, which as we've already covered becomes `42 == 42`, so `a` and `b` are found to be coercively equal.
- The `null` and `undefined` values cannot be boxed -- they have no object wrapper equivalent -- so `Object(null)` is just like `Object()` in that both just produce a normal object.
- `NaN` can be boxed to its `Number` object wrapper equivalent, but when `==` causes an unboxing, the `NaN == NaN` comparison fails because `Nan` is never equal to itself.
- If either side of the comparison can have `true` or `false` values, don't ever, EVER use `==`.
- If either side of the comparison can have `[]`, `""`, or `0` values,
seriously consider not using `==`.

## Statements & Expressions

- Statements are sentences, expressions are phrases, and operators are conjunctions/punctuation.
- Consider:

    ```js
    var a = 3 * 6;
    var b = a;
    b;
    ```

    In this snippet, `3 * 6` is an expression (evaluates to the value `18`). But `a` one the second line is also an expression, as is `b` on the third line. `var a = 3 * 6` and `var b = a` are called **declaration statements** because they each declare a variable (and optionally assign a value to it). The `a = 3 * 6` and `b = a` assignments (minus the `var`s) are called **assignment expressions**. The third line `b` is a expression statement.
- The `++` increment operator and the `--` decrement operator are both unary operators, which can be used in either a postfix (**after**) position or prefix (**before**) position. For example:

    ```js
    var a = 42;

    a++; // 42
    a; // 43

    ++a; // 44
    a; // 44
    ```

- Consider:

    ```js
    var a = 42, b
    b = (a++, a);

    a; // 43
    b; // 43
    ```

    The expression `a++, a` means that the second `a` statement expression gets evaluated after the after side effects of the first `a++` statement expression, which means it returns the `43` value for assignment to `b`.
- Consider:

    ```js
    var obj = {
        a: 42
    };

    obj.a; // 42
    delete obj.a; // true
    obj.a; // undefined
    ```

    Nonexistent properties, or properties that exist and are configurable will return `true` from the `delete` operator. Otherwise the result will be `false` or an error.

## Contextual Rules

- Consider:

    ```js
    function foo() {
        // `bar` labeled-block
        bar: {
            console.log("Hello");
            break bar;
            console.log("never runs");
        }
        console.log("World");
    }

    foo();
    // Hello
    // World
    ```

    Labeled loops/blocks are extremely uncommon, and often frowned upon. It's best to avoid them if possible.
- Consider:

    ```js
    function getData() {
        // ..
        return {
            a: 42,
            b: "foo"
        };
    }

    var { a, b } = getData();

    console.log(a, b); // 42 "foo"
    ```

    `var { a , b } = ..` is a form of ES6 destructing assignment, which is roughly equivalent to:

    ```js
    var res = getData();
    var a = res.a;
    var b = res.b;
    ```

## `else if` And Optional Blocks

- `if` and `else` statements are allowed to omit the `{}` around their attached block if they only contain a single statement. For example:

    ```js
    if (a) something(a);
    ```

    So `else if` is `else {} if {}`, thus `else` brackets can be removed, because it's a single statement.

## Operator Precedence

- Consider:

    ```js
    var a = 5;
    var b = (a++, a);

    console.log(`a: ${a}`);
    console.log(`a: ${b}`);
    ```

    Here `()` have precedence so it will execute first, then the value will assign to `b`.
- The `&&` is more precedent than `||`, and `||` is more precedent than `? :`. Conider:

    ```js
    var a = 42;
    var b = "foo";
    var c = false;

    var d = a && b || c ? c || b ? a : c && b : a;
    ```

    Its like this:

    ```js
    (a && b || c) ? (c || b) ? a : (c && b) : a;
    ```

    So answer is `42`. Another example:

    ```js
    true ? false : true ? true : true; // false
    true ? false : (true ? true : true); // false
    (true ? false : true) ? true : true; // true
    ```

- Use operator precedence/associativity where it leads to shorter and cleaner code, but use `()` manual grouping in places where it helps create clarity and reduce confusion.

## Short Circuited

- With `a && b`, `b` is not evaluated if `a` is falsy, because the result of the `&&` operand is already certain, so there's no point to bothering to check `b`. Likewise, with `a || b`, if `a` is thruthy, the result of operand is already certain, so there's no reason to check `b`. For example:

    ```js
    var a = true;
    var b = true;

    // `a` is true, so there's no reason to check `b`
    if (a || b) {
        console.log("Works!");
    }
    ```

## Automatic Semicolons

- ASI (**A**utomatic **S**emicolon **I**nsertion) is when **JavaScript** assumes a `;` in certain places in your **JavaScript** program even if you didn't put one there.
- It's important to note that ASI will only take effect in the presence of a newline (aka line break). Semicolons are not inserted in the middle of a line.
- If the **JavaScript** parser parses a line where a parser error would occur (a missing expected `;`), and it can reasonably insert one, it does so.
- Consider:

    ```js
    var a = 42, b
    c;
    ```

    Here **JavaScript** assumes instead that there's an implied `;` (at the new line) after `b`. Thus, `c;` is left as a standalone expression statement.
- The other major case where ASI kicks in is with the `break`, `continue`, `return`, and (ES6) `yield` keywords. For example:

    ```js
    function foo(a) {
        if (!a) return
        a *= 2;
        // ..
    }
    ```

- Most, but not all, semicolons are optional, but the two `;`s in the `for (..) ..` loop header are required.
- Use semicolons wherever you know they are **required**, and limit your assumptions about ASI to a minimum.

## Errors

- ES5's `strict` mode defines even more early errors. For example, in `strict` mode, function parameter names cannot be duplicated:

    ```js
    function foo(a, b, c) { } // just fine
    function foo(a, b, c) {"use strict"} // Error!
    ```

    Another `strict` mode early errors is an object literal having more than one property of the same name. For example:

    ```js
    (function () {
        "use strict"

        var a = {
            b: 42,
            b: 43
        }; // Error!
    })();
    ```

    Semantically speaking, such errors aren't technically syntax errors but more grammar errors -- the above snippets are syntactically valid. But since there is no `GrammerError` type, some browsers use `SyntaxError` instead.
- Consider:

    ```js
    function foo(a) {
        a = 42;
        console.log(arguments[0]);
    }

    foo(2); // 42 (linked)
    foo(); // undefined (not linked)
    ```

    If you pass an argument, the `arguments` slot and the named parameter are linked to always have the same value. If you ommit the argument, no such linkage occurs.
- Never refer to a named parameter and its corresponding `arguments` slot at the same time. For example:

    ```js
    function foo(a) {
        console.log(a + arguments[1]); // safe!
    }

    foo(10, 32); // 42
    ```

## `try..finally`

- Consider:

    ```js
    function foo() {
        try {
            return 42;
        }
        finally {
            console.log("Hello");
        }

        console.log("never runs");
    }

    console.log(foo());
    // Hello
    // 42
    ```

    The `return 42` runs right away, which sets up the completion value from the `foo()` call. The action completes the `try` clause and the `finally` clause immediately runs next. Only then is the `foo()` function complete, so that its completion value is returned back for the `console.log(..)` statement to use.

    The exact same behavior is true of a `throw` inside `try`:

    ```js
    function foo() {
        try {
            throw 42;
        }
        finally {
            console.log("Hello");
        }

        console.log("never runs");
    }

    console.log(foo());
    // Hello
    // Uncaught Exception: 42
    ```

- If an exception is thrown (accidentally or intentionally) inside a `finally` clause, it will override as the primary completion of that function. If a previous `return` in the `try` block had set a completion value for the function, that value will be abandoned. For example:

    ```js
    function foo() {
        try {
            return 42;
        }
        finally {
            throw "Oops!";
        }

        console.log("never runs");
    }

    console.log(foo());
    // Uncaught Exception: Oops!
    ```

    It shouldn't be surprising that other nonlinear control statements like `continue` and `break` exhibit similar behavior to `return` and `throw`:

    ```js
    for (var i = 0; i < 10; i++) {
        try {
            continue;
        }
        finally {
            console.log(i);
        }
    }
    // 0 1 2 3 4 5 6 7 8 9
    ```

- A `return` inside a `finally` has the special ability to override a previous `return` from the `try` or `catch` clause, but only if `return` is explicitly called:

    ```js
    function foo() {
        try {
            return 42;
        }
        finally {
            // no `return ..` here, so no override
        }
    }

    function bar() {
        try {
            return 42;
        }
        finally {
            // override previous `return 42`
            return;
        }
    }

    function baz() {
        try {
            return 42;
        }
        finally {
            // override previous `return 42`
            return "Hello";
        }
    }

    foo(); // 42
    bar(); // undefined
    baz(); // "Hello"
    ```

- Inside a `finally` block the omission of `return` does not act like an overriding `return undefined`. It just lets the previous `return` stand.
- Using a `finally` + labeled `break` to effectively cancel a `return` is doing your best to create the most confusing code possible.

## `switch`

- Consider:

    ```js
    switch (a) {
        case 2:
            // do something
            break;
        case 42:
            // do something
            break;
        default:
            // fallback to here
    }
    ```

    The matching that occurs between the `a` expression and each `case` expression is identical to the `===` algorithm.
- You can use logical operators like `&&` or `||` in your expression. But this can bite you. For example:

    ```js
    var a = "hello world";
    var b = 10;

    switch (true) {
        case (a || b == 10):
            // never gets here
            break;
        default:
            console.log("Oops");
    }
    // Oops
    ```

    Since the result of `(a || b == 10)` is `"hello world"` and not `true`, the strict match fails. You can fix this by force the expression to be a `true` or `false`, like this: `!!(a || b == 10):`.

## ECMAScript

- The offical name of the language is ECMAScript.
- **JavaScript** is the common tradename of the language, of course, but more appropriately, **JavaScript** is basically the browser implementation of the spec.

## Host Objects

- Some behavior variations with host objects to be aware of can include:
  - not having access to normal `object` built-ins like `toString()`
  - not being overwritable
  - having certain predefined read-only properties
  - having methods that cannot be `this`-overriden to other objects
  - and more...

## `<script>`

- All scripts can intract together with `global` object (`window` in browser).
- Consider:

    ```js
    <script>foo();</script>

    <script>
        function foo() { .. }
    </script>
    ```

    This snippet have problem, because `foo()` is not declared yet. You can declared it in another separate code and put it in `<script>` first to call it. For example:

    ```js
    <script>
        function foo() { .. }
    </script>

    <script>foo();</script>
    ```

- HTML-style or X(HT)ML-style comments around inline code is deprecated and doesn't work, so don't do it. For example:

    ```js
    <script>
    <!--
    alert( "Hello" );
    //-->
    </script>

    <script>
    <!--//--><![CDATA[//><!--
    alert( "World" );
    //--><!]]>
    </script>
    ```

## Reserved Words

- Prior to ES5, the reserved words also could not be property names or keys in object literals, but that restriction no longer exists. So, this is not allowed:

    ```js
    var import = "42";
    ```

    But this is allowed:

    ```js
    var obj = { import: "42" };
    console.log(obj.import); // "42"
    ```

- Consider:

    ```js
    function addAll() {
        var sum = 0;
        for (var i = 0; i < arguments.length; i++) {
            sum += arguments[i];
        }
        return sum;
    }

    var nums = [];
    for (var i = 1; i < 100000; i++) {
        nums.push(i);
    }

    addAll(2, 4, 6); // 12
    addAll.apply(null, nums); // should be: 499950000
    ```

    In some **JavaScript** engines, you'll get the correct answer, but in others (like Safari 6.x), you'll get the error: **"RangeError: Maximum call stack size exceeded"**.
- Examples of some limits known to exist:
  - Maximum number of characters allowed in a string literal (not just a string value)
  - Size (bytes) of data that can be sent in arguments to a function call (aka stack size)
  - Number of parameters in a function declaration
  - Maximum depth of non-optimized call stack (i.e., with recursion): how long a chain of function calls from one to the other can be
  - number of seconds a **JavaScript** program can run continuously blocking the browser
  - maximum length allowed for a variable name
