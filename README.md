# TypeScript for Humans

### Table of Contents

* [TypeScript](#1-TypeScript)
* [Working of TypeScript](#2-Working-of-TypeScript)
* Difference between JavaScript and TypeScript
* [Type System](#3-Type-System)


### 1. TypeScript

- TypeScript is JavaScript with syntax for types
- TypeScript is a superset of JavaScript i.e any JavaScript code is a TypeScript (not vice-versa)
- TypeScript is a language which compiles and gives JavaScript as output

👉&nbsp;&nbsp;&nbsp;As TypeScript is a superset, existing JS codebase can be gradually migrated to TS without requiring a complete migration at once.

### 2. Working of TypeScript

- TypeScript compiles the code JavaScript
  - TypeScript converts the code to AST (Abstract Syntax Tree)
  - AST is checked by typechecker
  - AST is then converted to JavaScript code

TypeChecker is a special program that verifies that your code is typesafe
Type safety means using types to prevent programs from doing invalid/unexpected things

👉&nbsp;&nbsp;&nbsp;Browsers cannot understand the typescript code. So TypeScript code has to be converted to JavaScript to run in browser or other JavaScript host platforms.

### 3. Type System

A set of rules that a typechecker uses to assign types to your program
2 kinds of type systems are present on TypeScript
- Explicit type system
  - Explicitly annotate the types. Ex: const value: number = 10;
- Infered type system
  - Let TypeScript decide the type by assigned value. Ex: const value = 10;

👉&nbsp;&nbsp;&nbsp;Best practice is to let TypeScript infer types as it can, keeping explicitly typed code to a minimum whenver needed.
