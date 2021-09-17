<h1 align="center">TypeScript for Humans</h1>
<h3 align="center">Kick starter guide to writing TypeScript</h3>
<div align="center">One of the most practical materials to start implementing TypeScript in no time. (⚠️ Repo is in progress)<br><br>
<!--   <p>
    <a name="stars"><img src="https://img.shields.io/github/stars/sadanandpai/typescript-for-humans?style=for-the-badge"></a>
    <a name="forks"><img src="https://img.shields.io/github/forks/sadanandpai/typescript-for-humans?logoColor=green&style=for-the-badge"></a>
    <a name="contributions"><img src="https://img.shields.io/github/contributors/sadanandpai/typescript-for-humans?logoColor=green&style=for-the-badge"></a>
    <a name="license"><img src="https://img.shields.io/github/license/sadanandpai/typescript-for-humans?style=for-the-badge"></a>
  </p> -->
  Show your support by giving a ⭐ to this repo
</div>

---

### Table of Contents

- [What is TypeScript](#1-What-is-TypeScript)
- [Working of TypeScript](#2-Working-of-TypeScript)
- [Difference between JavaScript and TypeScript](#3-Difference-between-JavaScript-and-TypeScript)
- [Type System](#4-Type-System)
- [Declaring primitives](#5-Declaring-primitives)
- [Type literals](#6-Type-literals)
- [Any and Unknown](#7-Any-and-Unknown)
- [Objects](#8-Objects)
- [Object property modifiers](#9-Object-property-modifiers)
- [Type aliases](#10-Type-aliases)
- [Arrays](#11-Arrays)
- [Tuples](#12-Tuples)
- [Enums](#13-Enums)
- ℹ️ More coming soon

### 1. What is TypeScript

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

### 6. Type literals

- A type that represents a single value and nothing else
- Type literal narrowed version of a type

```ts
let myBoolean: false; // myBoolean has type false and not 'boolean'
let myNum: 100 = 100; // myNum has type '100' and not 'number'
const myStr = "hello"; // myStr has type 'hello' and not 'string'
```

👉&nbsp;&nbsp;&nbsp;TypeScript knows that once a primitive is assigned with const its value will never change, it infers the most narrow type it can for that variable

<br>

### 7. Any and Unknown

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

if (typeof myVar === "number") {
  // confirm before usage, unlike 'any'
  const myVarInc = 1 + myVar;
} else if (typeof myVar === "string") {
  const myVarSmall = myVar.toLowerCase(); // allowed to call string methods as we know myVar is of string type
}

myVar = "string"; // myVar is now 'string' type and not 'unknown' anymore
```

👉&nbsp;&nbsp;&nbsp;Any is best suited for migration projects from JavaScript to TypeScript or as a temporary measure<br>
👉&nbsp;&nbsp;&nbsp;Unknown can be used in the scenarios where you definitely do not know the type and may not know even in future

<br>

### 8. Objects

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
const obj: {  // object structure is explictly declared also know as 'object literal'
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
  [key: string]: boolean; // Index Signature indicates object can have any string type key with any value to it
};

obj = { key1: 100 };
obj = { key1: 100, key2: false };
obj = { key1: 100, greeting: true };
obj = { key1: 100, 10: true }; // as all the keys in object are stored as string 10 is considered as string '10'
```

👉&nbsp;&nbsp;&nbsp;Index Signature `[key: string]: boolean;` where 'key' is just used for semantic purpose

<br>

### 9. Object property modifiers

- Property declared as an optional one in object, may or may not have that key in the value
- Optional property on an object can created with the symbol '?'

```ts
let obj: {
  key1: number;
  key2?: string; // ? indicates, it is an optional property on the object
};

obj = { key1: 100 };
obj = { key1: 100, key2: "Optional key value" };
obj = { key1: 100, greeting: true };
obj = { key1: 100, 10: true }; // as all the keys in object are stored as string 10 is considered as string '10'
```

- Property declared as a readonly in an object, will follow the rules of 'const' keyword
- Readonly property on an object can created with the prefix readonly

```ts
const obj: {
  key1: number;
  readonly key2: string;
} = { key1: 100, key2: "Optional key value" };

obj.key2 = "Hello"; // key2 is readonly and not allowed to be reassigned
```

👉&nbsp;&nbsp;&nbsp;Index Signature `[key: string]: boolean;` where 'key' is just used for semantic purpose

<br>

### 10. Type aliases

- Type alias is a user defined type which can be type literal or a type

```ts
type Age = number; // Age is an alias for number
let age: Age;
age = 100;

type Point = {  // Point alias for object of type { x: number, y: number }
  x: number;
  y: number;
};

const coordinate: Point = {
  x: 100,
  y: 100,
};
```

- Type alias will be useful and powerful when used as the union of different types

```ts
type ID = number | string; // ID alias indicates the type can be either number or string

let userId: ID;
userId = 11;
userId = "11";

type Color = "red" | "blue" | "green"; // Color alias indicates the type can be one of the values

let color: Color;
color = "red";
color = "yellow"; // ERROR: other string values are not allowed
```

👉&nbsp;&nbsp;&nbsp;type aliases are block-scoped

<br>

### 11. Arrays

- Array has two types syntaxes: T[] and Array<T>
- The general rule of thumb is to keep arrays homogeneous.

```ts
let array: string[]; // array of strings only
// let array: Array<string>;
const array = [1, 2, "helo"]; // type infered array of 'number' and 'string'
```

- When array is declared empty, it makes the array type as 'any' and the type narrows down depending on the value type pushed into the array. This is known as 'Gradual typing'

```ts
const array = []; // array has 'any' type
array.push(1); // array has 'number[]' type
array.push("hello"); // array has (string | number)[] type
```

👉&nbsp;&nbsp;&nbsp;Though an empty array type widens when values are added, TypeScript will assign it a final type that can’t be expanded anymore, once it leaves the scope it was defined in.

<br>

### 12. Tuples

- Tuples are arrays having have fixed lengths, where the values at each index have types

```ts
let tuple: [string, number];
tuple = ["id", 1];
tuple = ["id", "one"]; // ERROR
```

- Tuples can have optional slots denoted by '?'

```ts
type Attribute = [string, string?]; // Equivalent to ([string] | [string, string])
const atrributes1: Attribute = ["class", "container"];
const atrributes2: Attribute = ["disabled"];
```

👉&nbsp;&nbsp;&nbsp;Tuple can be readonly as well with the modifier 'readonly' (`let tuple: readonly [number] = [5];`)

<br>

### 13. Enums

- Enums allows for describing a value which could be one of a set of possible named constants
- Enum properties when not assigned will have incremental numeric integer values starting from 0

```ts
enum Agreement {
  No, // 0
  Yes, // 1
}
hasUserAgreed = Agreement.Yes;

enum Direction {
  Up = 1,
  Down, // 2
  Left, // 3
  Right, // 4
}
direction: Direction = Direction.Down;
```

- Enums can also be string, computed values or heterogeneous mix as well

```ts
enum Color {
  Blue = 1,
  Red = '2',
  White = '25'+ '5', // computed value
}

const colorName = Color[255]; // reverse lookup
```

- Enums can be declared as 'const' which will not allow reverse lookups, and also doesn’t generate any JavaScript code instead inlines the enum member’s value.

```ts
const enum Language { 
  English = 1,
  French = 2,
  Russian
}

const language = Lanugage.French; // language will be assigned with value 2 in compile time rather than run time
```

👉&nbsp;&nbsp;&nbsp;String Enums are useful. But numeric Enums have problems and leak bugs. So the usage of Enums are not recommended in general unless it is String Enums
  
ℹ️ More coming soon
