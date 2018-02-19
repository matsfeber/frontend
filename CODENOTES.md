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
var a = 42;
typeof a; // "number"

a = true;
typeof a; // "boolean"

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

>var c = a
	>// split `a` into an array of characters
	>.split( "" )
	>// reverse the array of characters
	>.reverse()
	>// join the array of characters back to a string
	.join( "" );

>c; // "oof"

 **Numbers**
Specify how many fractional decimal places you want :
var a = 42.59;

a.toFixed( 0 ); // "43"
a.toFixed( 1 ); // "42.6"
a.toFixed( 2 ); // "42.59"
a.toFixed( 3 ); // "42.590"
a.toFixed( 4 ); // "42.5900"

numbers include several special values, like NaN (supposedly "Not a Number", but really more appropriately "invalid number"); +Infinity and -Infinity; and -0.

Simple scalar primitives (strings, numbers, etc.) are assigned/passed by value-copy, but compound values (objects, etc.) are assigned/passed by reference-copy. References are not like references/pointers in other languages -- they're never pointed at other variables/references, only at the underlying values.

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
