# TypeScript for humans

### Table of Contents

* [TypeScript?](#1)
* [Working of TypeScript](#2)
* [Type system](#3)


### 1
### TypeScript

- TypeScript is JavaScript with syntax for types
- TypeScript is a superset of JavaScript i.e any JavaScript code is a TypeScript (not vice-versa)
- TypeScript is a language which compiles and gives JavaScript as output

### 2
### Working of TypeScript

- TypeScript compiles the code JavaScript
  - TypeScript converts the code to AST (Abstract Syntax Tree)
  - AST is checked by typechecker
  - AST is then converted to JavaScript code

TypeChecker is a special program that verifies that your code is typesafe
Type safety means using types to prevent programs from doing invalid/unexpected things

### 3
### Type system

A set of rules that a typechecker uses to assign types to your program
2 kinds of type systems are present on TypeScript
- Explicit type system
- Infered type system
