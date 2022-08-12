# Functions: Continued

## Learning Goals

- Define a function using a function declaration
- Define `hoisting`
- Define `function expression`
- Define `anonymous function`
- Define a function using a function expression
- Define an IIFE: `Immediately-Invoked Function Expression`

## Introduction

This lesson dives deeper into some more advanced concepts related to JavaScript 
functions and other ways to define them.

## Review Function Declaration

As we learned in the previous lesson, one ofthe most common way to define functions is 
with a **function declaration**:

```js
function razzle() {
  console.log("You've been razzled!");
}
```

The word `razzle` becomes a _pointer_ to some stored, potential,
not-yet-actually-run bit of work (the function). We use the _pointer_ to _call_
or _invoke_ the function. We _call_ the function by adding `()` after the
_pointer_.

```js
function razzle() {
  console.log("You've been razzled!");
}
razzle();
//=> "You've been razzled!"
```

Functions can be passed arguments, given default arguments, etc. Here's a
brief code synopsis:

```js
function razzle(lawyer = "Billy", target = "'em") {
  console.log(`${lawyer} razzle-dazzles ${target}!`);
}
razzle(); //=> Billy razzle-dazzles 'em!
razzle("Methuselah", "T'challah"); //=> Methuselah razzle-dazzles T'challah!
```

Interestingly, you can write function declarations _after_ you call them:

```js
razzle(); //=> "You've been razzled!"
function razzle() {
  console.log("You've been razzled!");
}
```

But why? Variables aren't able to be looked up before they're declared. What 
makes functions different?

## Define `Hoisting`

JavaScript's ability to call functions _before_ they appear in the code is
called _hoisting_. For hoisting to work, **the function must be defined using a
function declaration**.

Does this mean there are other ways to define functions? Yes. We'll cover a few 
in this lesson. 

## Define `Function Expression`

We've learned that programming languages feature _expressions_: arrangements of
constants, variables, and symbols that, when interpreted by the language,
produce a _value_. To review, open up your browser console and type in these
examples:

```js
1 + 1; //=> 2
"Razzle " + "dazzle!"; //=> "Razzle dazzle!"
```

The examples above are expressions that return _primitive values_, but
JavaScript also has _function expressions_ that look like this:

```js
function() {
  console.log("Yet more razzling");
}
```

The _value_ returned by this expression is the function itself. Go ahead and
enter the above into the browser console; you should see the following:

```js
Uncaught SyntaxError: Function statements require a function name
```

The problem is that, when the function expression appears by itself as shown
above, **JavaScript does not recognize it as a function expression**; it instead
interprets it as a function declaration that's missing its name. One way to tell
the JavaScript engine that it's a function expression is to use the
`grouping operator ()` to wrap the entire thing:

```js
(function () {
  console.log("Yet more razzling");
});
```

Recall that the grouping operator is usually used in arithmetic operations to
tell the JavaScript engine to evaluate the value that's inside it first. It's
serving a similar purpose in this case: it's telling JavaScript to interpret
what's inside the parentheses as a _value_. With the grouping operator in place,
the JavaScript engine recognizes our function as a function expression. Enter
the function into your console again, this time using the grouping operator. You
should see the following:

```js
ƒ () {
  console.log("Yet more razzling");
}
```

JavaScript now correctly shows us the return value of our function expression: a
_function_ (indicated by the `ƒ ()`) storing the work of logging our message.

## Define `Anonymous Function`

An **anonymous function** is, quite simply, a function that doesn't have a name:

```js
function() {
  console.log("Yet more razzling");
}
```

Unlike a function declaration, there's no function name in front of the `()`.
Note, however, that if we don't assign a name to the function, we have no way to
call it. We lose access to our function immediately after it's created. So how
can we invoke an anonymous function? One way is to assign it to a variable.

## Define a Function Using a Function Expression

We can solve the problem of accessing an anonymous function by declaring a variable 
and assigning the function as its value. Recall that any expression can be assigned 
to a variable; this includes function expressions:

```js
const fn = function () {
  console.log("Yet more razzling");
};
```

The code above defines our function using a function expression. If we ask
JavaScript what's in `fn`, it tells us:

```js
fn; //=> ƒ () { console.log("Yet more razzling") }
```

Here, `fn` is a _pointer_ to the stored block of work that hasn't yet been
invoked. Just as with **function declaration**, to actually do the work, we need
to _invoke_ or _call_ the function. We do this by adding `()` to the end of our
"pointer", the variable name:

```js
const fn = function () {
  console.log("Yet more razzling");
}; //=> undefined
fn; //=> ƒ () { console.log("Yet more razzling") }
fn(); // "Yet more razzling"
```

Also as with a function declaration, if we need to pass arguments to the
function, we would include those in the parentheses when we call the function.

We now know how to define a function as a function expression. Very importantly,
**_function expressions are not hoisted_**. The same is true for any variable
assignment: if we assign a `String` or the result of an arithmetic expression to
a variable, those assignments are not hoisted either.

## Define an IIFE: Immediately-Invoked Function Expression

Another way to invoke an anonymous function is by creating what's known as an
`immediately-invoked function expression (IIFE)`.

As a thought experiment, consider what happens here:

```js
(function (baseNumber) {
  return baseNumber + 3;
})(2); //=> ???
```

We recognize the first `()` as the grouping operator that tells the JavaScript
engine to interpret the contents as a value — in this case, a function
expression. What this means is that, in the IIFE statement, the value returned
by the first set of parentheses is an anonymous function, which can be invoked
(immediately).

The second `()` are the `()` of function invocation. When we put them
immediately after the first set of parentheses, we're invoking the function that
those parentheses return immediately after defining it. Try it out in the
browser console:

```js
(function (baseNumber) {
  return baseNumber + 3;
})(2); //=> 5
```

Interestingly, any variables, functions, `Array`s, etc. that are defined
_inside_ of the function expression's body _can't_ be seen _outside_ of the
IIFE. To see this, check the value of `baseNumber` in the console. It's like
opening up a micro-dimension, a bubble-universe, doing all the work you could
ever want to do there, and then closing the space-time rift.

## Conclusion

In this lesson, we've covered more ways to define and invoke functions. Before we carry on to more advanced concepts, let's practice what we've already learned with a lab.

## Resources

- [Wikipedia — First-class function][wiki]
- [StackOverflow — What is meant by 'first class object'?][stackoverflow]
- [Helephant — Functions are first class objects in javascript (Wayback Machine)][helephant]
- [2ality — Expressions versus statements in JavaScript][2ality]
- [MDN — Functions][mdn-fn]
- [MDN — Statements and declarations][mdn]

[wiki]: https://en.wikipedia.org/wiki/First-class_function
[stackoverflow]: https://stackoverflow.com/questions/705173/what-is-meant-by-first-class-object
[helephant]: https://web.archive.org/web/20170606141950/http://helephant.com/2008/08/19/functions-are-first-class-objects-in-javascript/
[2ality]: http://2ality.com/2012/09/expressions-vs-statements.html
[mdn]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements
[mdn-fn]: https://developer.mozilla.org/en-US/docs/web/JavaScript/Reference/Operators/function
