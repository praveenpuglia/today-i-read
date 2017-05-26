# You Will Now Know JS

So? Is JavaScript Compiled or Interpreted?

## Scopes
```js
var foo = "bar";
function bar() {
  var foo = "baz";
}
function baz(foo) {
  foo = "bam";
  bam = "yay";
}
```

## Function Declaration Vs Function Expression
```js
var foo = function bar() {
  var foo = "baz";
  function baz(foo) {
    foo = bar;
    foo;
  }
  baz();
};
foo();
bar();

```

## IIFE
```js
var foo = "something";
(function(global, $, undefined){
  var foo = "whatever";
})(window, jQuery, );

console.log(foo);
```

## Which IIFE?
```js
(function notDouglas(){
  ...
})();

(function douglas(){
  ...
}());
```

## Hoisting - Variables & Functions
```js
var a = b();
var c = d();
a;
c;

function b() {
  return c;
}

var d = function() {
  return b();
};
```

## Functions get hoisted before variables. Proof.
```js
foo();

var foo = ":D";

function foo() {
  console.log("bar");
}

function foo() {
  console.log("foo");
}
```

## Mutual Recursion
```js
function a() {
  b();
}

function b() {
  a();
}
```

## Can you solve this?
```js
a(1);

function a(foo) {
  if( foo > 20 ) return foo;
  return b(foo + 2);
}
function b(foo) {
  return c(foo) + 1;
}
function c(foo) {
  return a(foo * 2);
}
```

## Default & Implicit Binding
```js
var foo = "hello";

function bar() {
  console.log(this.foo);
}
bar(); // value? // what was this?

var obj = {
  foo: "world",
  bar: bar
}

obj.bar(); // value? // what was this?
```

## Explicit Binding
```js
function getName() {
  return this.name;
}

var name = "Praveen";
getName(); // value?

var obj = {
  name: "Explicitly Praveen"
}

getName.call(obj); // value?
```

## What's `this`?
```js
function getName(){
  return this.name;
}

var originalFn = getName;
var object1 = { name: "Praveen" };
var object2 = { name : "Puglia" };

getName = function() {
  originalFn.call(object1)
}

getName();
getName.call(object2);
```
## The `new` keyword. 
### What do you know about it already? 

## Example of Inheritance 
```js
function Person(who) {
  this.me = who;
}
Person.prototype.guessWho = function(){
  return `I am ${this.me}`;
};

// Subclass.. sort of.
function Techie(who) {
  Person.call(this, who);
}

// Inherit
Techie.prototype = Object.create(Person.prototype);

// Extend
Techie.prototype.sayHello = function() {
  console.log(`${this.guessWho()} and NO! I won't fix your printer`);
};

var dexter = new Techie("Dexter");
t1.sayHello();
```

## Let's do better
```js
var Person = {
  init: function(who) {
    this.me = who;
  },
  guessWho: function(){
    return `I am ${this.me}`;
  }
}

var Techie = Object.create(Person);
Techie.sayHello = function(){
  console.log(`${this.guessWho()} and NO! I won't fix your printer`);
};

var dexter = Object.create(Techie);
dexter.init("Dexter");
dexter.sayHello();
```




