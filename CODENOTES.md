# Aantekeningen

## You Don't Know JS: Scope & Closures
### Chapter 1: What is Scope

One of the most fundamental paradigms of nearly all programming languages is the ability to store values in variables, and later retrieve or modify those values. In fact, the ability to store values and pull values out of variables is what gives a program state.

But where are variables stored and how does a program find them when it needs them?

there is a set of rules for storing and finding those variables. That set of rules is called scope.

##### Compiler theory

Compiler = Het vertalen of omzetten wordt compilatie of compileren genoemd. Met compiler wordt voornamelijk een programma bedoeld dat een programma in een hogere programmeertaal vertaalt naar een lagere programmeertaal, meestal assembleertaal of machinecode. De voornaamste reden om broncode te compileren is dan ook het maken van uitvoerbare code.

**Three steps of compilation**

1.Tokenizing/Lexing:
breaking up a string of characters into meaningful (to the language) chunks, called tokens.

2.Parsing:
taking a stream (array) of tokens and turning it into a tree of nested elements, which collectively represent the grammatical structure of the program. This tree is called an "AST" (Abstract Syntax Tree).

3.Code-Generation:
the process of taking an AST and turning it into executable code. This part varies greatly depending on the language, the platform it's targeting, etc.\

Note : The JavaScript engine is vastly more complex than just those three steps, as are most other language compilers

##### Understanding Scope

## You Don't Know JS: Scope & Closures
### chapter 1 : Types
>a type is an intrinsic, built-in set of characteristics that >uniquely identifies the behavior of a particular value and >distinguishes it from other values, both to the engine and >to the developer.

42 = Number
"42" = String
Two values with different types.

JavaScript defines seven built-in types:
* null
* undefined
* boolean
* number
* string
* object
* symbol -- added in ES6!

typeof inspects the type of a given value.

Functions are referred to as callabale objects (subtype of objects).
The function object has a **length**, the parameters.
Example function a(b,c) = length 2. b and c = 2.

Arrays are not a subtype and just objects.

Variables dont have types because they hold values and only values have types!

Example :
``` javascript
var a = 42;
typeof a; // "number"

a = true;
typeof a; // "boolean"
``` 

**undefined vs "undeclared"**

var a;

a; // undefined
b; // ReferenceError: b is not defined/undeclared

If you want to check variable in the global use (window.variable)

### chapter 2 : Values
Basic values/building blocks :
* Arrays
* Stings
* numbers

**Arrays**

A array is just a container for another type of value, from string to number to object to even another array (which is how you get multidimensional arrays).

Generally, it's not a great idea to add string keys/properties to arrays. Use objects for holding values in keys/properties, and save arrays for strictly numerically indexed values.

**Strings**

JavaScript strings are immutable, while arrays are quite mutable.

Mutable = Changeable.

Another workaround (aka hack) is to convert the string into an array, perform the desired operation, then convert it back to a string.

``` javascript
var c = a
	// split `a` into an array of characters
	.split( "" )
	// reverse the array of characters
	.reverse()
	// join the array of characters back to a string
	.join( "" );

c; // "oof"
```

 **Numbers**

Specify how many fractional decimal places you want :
``` javascript
var a = 42.59;

a.toFixed( 0 ); // "43"
a.toFixed( 1 ); // "42.6"
a.toFixed( 2 ); // "42.59"
a.toFixed( 3 ); // "42.590"
a.toFixed( 4 ); // "42.5900"
```

numbers include several special values, like NaN (supposedly "Not a Number", but really more appropriately "invalid number"); +Infinity and -Infinity; and -0.

Simple scalar primitives (strings, numbers, etc.) are assigned/passed by value-copy, but compound values (objects, etc.) are assigned/passed by reference-copy. References are not like references/pointers in other languages -- they're never pointed at other variables/references, only at the underlying values.

var a = new Array( 3 ); gives a.length = 3;
very confusing.It implies that there are 3 undifined values in this array when in fact the slots dont exist.

### chapter 3 : Natives
Here's a list of the most commonly used natives:

* String()
* Number()
* Boolean()
* Array()
* Object()
* Function()
* RegExp()
* Date()
 * Error()
* Symbol() -- added in ES6!

These Natives are built-in functions.

Values that are typeof "object" (such as an array) are additionally tagged with an internal [[Class]] property (think of this more as an internal classification rather than related to classes from traditional class-oriented coding). This property cannot be accessed directly, but can generally be revealed indirectly by borrowing the default Object.prototype.toString(..) method called against the value.

In general, there's basically no reason to use the object form directly. It's better to just let the boxing happen implicitly where necessary. In other words, never do things like new String("abc"), new Number(42), etc -- always prefer using the literal primitive values "abc" and 42.

``` javascript
var a = "abc";
var b = new String( a );
var c = Object( a );

typeof a; // "string"
typeof b; // "object"
typeof c; // "object"

b instanceof String; // true
c instanceof String; // true
```

Object.prototype.toString.call( b ); // "[object String]"
Object.prototype.toString.call( c ); // "[object String]"

**Review**

JavaScript provides object wrappers around primitive values, known as natives (String, Number, Boolean, etc). These object wrappers give the values access to behaviors appropriate for each object subtype (String#trim() and Array#concat(..)).

If you have a simple scalar primitive value like "abc" and you access its length property or some String.prototype method, JS automatically "boxes" the value (wraps it in its respective object wrapper) so that the property/method accesses can be fulfilled.

### Chapter 4 : Coercion

Coercion = Dwingen

Converting a value from one type to another is often called "type casting," when done explicitly, and "coercion" when done implicitly (forced by the rules of how a value is used).

There is implicit coercion and explicit coercion.

Explicit = when it is obvious from looking at the code that a type conversion is intentionally occurring.

Implicit = when the type conversion will occur as a less obvious side effect of some other intentional operation.

f any non-number value is used in a way that requires it to be a number, such as a mathematical operation, the ES5 spec defines the ToNumber abstract operation in section 9.3.

For example, true becomes 1 and false becomes 0. undefined becomes NaN, but (curiously) null becomes 0.

But the values **1** and **0** are not the same as **true** and **false**. Numbers are numbers and booleans are booleans. You can coerce 1 to true and 0 to false but you can also coerce it vice versa, but they are **not** the same.

All of JavaScript's values can be divided into two categories:

1. values that will become false if coerced to boolean
2. everything else (which will obviously become true)

**Explicit coercion**
``` javascript
var a = 42;
var b = String( a );

var c = "3.14";
var d = Number( c );

b; // "42"
d; // 3.14
```

putting **+** before something can make it a number.
**Example :**
var d = new Date( "Mon, 18 Aug 2014 08:53:06 CDT" );

+d; // 1408369986000

**Review**

In this chapter, we turned our attention to how JavaScript type conversions happen, called coercion, which can be characterized as either explicit or implicit.

Coercion gets a bad rap, but it's actually quite useful in many cases. An important task for the responsible JS developer is to take the time to learn all the ins and outs of coercion to decide which parts will help improve their code, and which parts they really should avoid.

Explicit coercion is code which is obvious that the intent is to convert a value from one type to another. The benefit is improvement in readability and maintainability of code by reducing confusion.

Implicit coercion is coercion that is "hidden" as a side-effect of some other operation, where it's not as obvious that the type conversion will occur. While it may seem that implicit coercion is the opposite of explicit and is thus bad (and indeed, many think so!), actually implicit coercion is also about improving the readability of code.

Especially for implicit, coercion must be used responsibly and consciously. Know why you're writing the code you're writing, and how it works. Strive to write code that others will easily be able to learn from and understand as well.

### Chapter 5 : Grammar

The grammar for JavaScript is a structured way to describe how the syntax (operators, keywords, etc.) fits together into well-formed, valid programs.

Every expression in JS can be evaluated down to a single, specific value result. For example:

``` javascript
var a = 3 * 6;
var b = a;
b;
```

In this snippet, 3 * 6 is an expression (evaluates to the value 18). But a on the second line is also an expression, as is b on the third line. The a and b expressions both evaluate to the values stored in those variables at that moment, which also happens to be 18.

Moreover, each of the three lines is a statement containing expressions.




## Aantekeningen les
### Les 2

LHS = Left_Hand_Side
RHS = Right_Hand_Side

Variables leven in een scope.
Bijvoorbeeld : functie scope, de variable b leeft in de function scope, deze variable b is niet bereikbaar buiten function foo.

Function foo(){
  var b= "b";
}

de variable d leeft globale function scope van window, in het gehele window bereikbaar.

var d="d";

Scopes worden afgelopen naar boven toe.

### Les 5

``` javascript
var clowns = [] // literal array
var clown = {   // literal object
  name: 'Pipo',    
  shoeSize: 80,  
  laugh: function(){
    console.log('ik heet ' + this.name + ' whoehahaah')
    }
  }             // literal object
  ```
