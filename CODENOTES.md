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
