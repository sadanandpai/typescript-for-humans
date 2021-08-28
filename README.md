# TypeScript for Humans

### Table of Contents

- [TypeScript](#1-TypeScript)
- [Working of TypeScript](#2-Working-of-TypeScript)
- [Difference between JavaScript and TypeScript](#3-Difference-between-JavaScript-and-TypeScript)
- [Type System](#4-Type-System)
- [Declaring primitives](#5-Declaring-primitives)
- [Any and Unknown](#6-Any-and-Unknown)
- [Objects](#6-Objects)

### 1. TypeScript

- TypeScript is JavaScript with syntax for types
- TypeScript is a superset of JavaScript i.e any JavaScript code is a TypeScript (not vice-versa)
- TypeScript is a language which compiles and gives JavaScript as output

👉&nbsp;&nbsp;&nbsp;As TypeScript is a superset, existing JS codebase can be gradually migrated to TS without requiring a complete migration at once

<br>

### 2. Working of TypeScript

- TypeScript compiles the code JavaScript
  - TypeScript converts the code to AST (Abstract Syntax Tree)
  - AST is checked by typechecker
  - AST is then converted to JavaScript code

TypeChecker is a special program that verifies that your code is typesafe
Type safety means using types to prevent programs from doing invalid/unexpected things

👉&nbsp;&nbsp;&nbsp;Browsers cannot understand the typescript code. So TypeScript code has to be converted to JavaScript to run in browser or other JavaScript host platforms

<br>

### 3. Difference between JavaScript and TypeScript

| Feature              | Syntax           | Description      |
| -------------------- | ---------------- | ---------------- |
| type binding         | dynamic          | static           |
| auto type conversion | yes              | no (mostly)      |
| type check           | runtime          | compile          |
| error detection      | runtime (mostly) | compile (mostly) |

👉&nbsp;&nbsp;&nbsp;Adding [//@ts-check](https://www.typescriptlang.org/docs/handbook/intro-to-js-ts.html) in your JS file helps editor to detect errors and show type hints

<br>

### 4. Type System

A set of rules that a typechecker uses to assign types to your program
2 kinds of type systems are present on TypeScript

- Explicit type system
  - Explicitly annotate the types. Ex: const value: number = 10;
- Infered type system
  - Let TypeScript decide the type by assigned value. Ex: const value = 10;

👉&nbsp;&nbsp;&nbsp;Best practice is to let TypeScript infer types as it can, keeping explicitly typed code to a minimum whenver needed

<br>

### 5. Declaring primitives

```ts
let myNum: number; // myNum has the type 'number' & can hold only number value
myNum = 10;
myNum = 45.98;

let myStr: string; // myStr has the type 'string' & can hold only string value
myStr = "TypeScript";
myStr = `sdafsfda`;

let myBool: boolean; // myBool has the type 'boolean' & can hold only boolean value
myBool = true;
myBool = 10 < 1;

let myUndefined: undefined; // myUndefined has the type 'undefined' & can hold only undefined value
myUndefined = undefined;

let myNull: null; // myNull has the type 'null' & can hold only null value
myNull = null;

let myBigint: bigint; // myBigint has the type 'bigint' & can hold only bigint value
myBigint = 1234n;

let mySymbol: symbol; // mySymbol has the type 'symbol' & can hold only symbol value
mySymbol = Symbol("a");
```

👉&nbsp;&nbsp;&nbsp;It is best to use "const" and assign the value to the variable wherever reassignment is not needed

<br>

### 6. Any and Unknown

- any
  - 'any' can be used as a type of variable when we do not have information of the type the variable has
  - 'any' is a type that can assigned to any variable
  - It can be considered as a supertype (parent) of all types i.e 'any' typed variable can behave like all the types we know in TypeScript
  - Any should be used as the last resort and must be avoided in almost all the cases as it makes TypeScript purposeless

```ts
let myVar: any = someUnknownReturnTypeFunction();
myvar.someFunction(); // no restriction as myVar is of type any
myVar = myVar + 10;
myVar = "myVar can be a string also";
```

- unknown
  - 'unknown' can be used as a type of variable when we do not have information of the type the variable has
  - 'unknown' is a type that can assigned to any variable, but that variable can be used only after confirmation of its type
  - Variable assigned with unknown type can have a definite type when it is assinged with definite type value which is not the case with 'any'

```ts
let myVar: unknown = someRandomFunctionFunction();

if (typeof myVar === "number") {  // confirm before usage, unlike 'any'
  const myVarInc = 1 + myVar;
} else if (typeof myVar === "string") {
  const myVarSmall = myVar.toLowerCase(); // allowed to call string methods as we know myVar is of string type
}

myVar = "string"; // myVar is now 'string' type and not 'unknown' anymore
```

👉&nbsp;&nbsp;&nbsp;Any is best suited for migration projects from JavaScript to TypeScript or as a temporary measure<br>
👉&nbsp;&nbsp;&nbsp;Unknown can be used in the scenarios where you definitely do not know the type and may not know even in future

<br>

### 7. Objects

- Objects in TypeScript are JavaScript object structures which can be explicitly or inference typed
- Object can have definite shape and the type structure declaration may look like

```ts
{
    key1: string;
    key2: number;
    key3: boolean;
    ...
}
```

- Object declared with 'Definite Assignment' will not allow accessing or assigning non existing keys

```ts
const obj: {  // object structure is explictly declared
  key: "value";
};

obj = {
  key: "hello",
};

/** Or object structure is infered as { key: string } when assigned directly */
// const obj = {
//   key: "hello",
// };

obj.key;
obj.someProperty; // ERROR: not allowed as it is not present on object type structure
obj.key2 = "new key value"; // ERROR: not allowed as it is not present on object type structure
```

- The object type to which allows any which key access can be created using 'Index Signature' and 'optional key' if needed

```ts
let obj: {
  key1: number;
  key2?: string; // ? indicates, it is an optional property on the object
  [key: string]: boolean; // Index Signature indicates object can have any string type key with any value to it
};

obj = { key1: 100 };
obj = { key1: 100, key2: "Optional key value" };
obj = { key1: 100, greeting: true };
obj = { key1: 100, 10: true }; // as all the keys in object are stored as string 10 is considered as string '10'
```

👉&nbsp;&nbsp;&nbsp;Index Signature can also be written as `[myKey: string]: any;` where 'myKey' is just used as semantic text
