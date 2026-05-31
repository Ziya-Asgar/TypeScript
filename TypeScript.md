# TypeScript

- [TypeScript](#typescript)
  - [Useful Links](#useful-links)
  - [Intro](#intro)
  - [tsconfig](#tsconfig)
    - [Transpiling Files](#transpiling-files)
    - [Some TSConfig Options](#some-tsconfig-options)
  - [Type Annotations and Type Inference](#type-annotations-and-type-inference)
  - [Primitive Types](#primitive-types)
    - [`string`, `number`, and `boolean`](#string-number-and-boolean)
    - [`null` and `undefined`](#null-and-undefined)
      - [`strictNullChecks` off](#strictnullchecks-off)
      - [`strictNullChecks` on](#strictnullchecks-on)
      - [Non-null Assertion Operator (Postfix `!`)](#non-null-assertion-operator-postfix-)
  - [Literal Types](#literal-types)
  - [Union](#union)
  - [Narrowing](#narrowing)
  - [Type Assertion](#type-assertion)
  - [The `satisfies` Operator](#the-satisfies-operator)
  - [Type Predicates](#type-predicates)
  - [`any`](#any)
  - [`unknown`](#unknown)
  - [Arrays](#arrays)
  - [Object Types](#object-types)
    - [Optional Properties](#optional-properties)
    - [The `readonly` Modifier](#the-readonly-modifier)
  - [Classes](#classes)
    - [Access Modifiers](#access-modifiers)
    - [Parameter properties](#parameter-properties)
    - [Readonly modifier](#readonly-modifier)
  - [Type Aliases](#type-aliases)
  - [Functions](#functions)
    - [Parameter Type Annotations](#parameter-type-annotations)
    - [Parameters with Default Values](#parameters-with-default-values)
    - [Return Type Annotations](#return-type-annotations)
    - [Functions Which Return Promises](#functions-which-return-promises)
    - [Function Type Expressions](#function-type-expressions)
    - [Type Aliased Functions](#type-aliased-functions)
    - [Call Signatures](#call-signatures)
    - [Construct Signatures](#construct-signatures)
    - [Function Overloads](#function-overloads)
    - [Other Function-related Types to Know About](#other-function-related-types-to-know-about)
      - [`void`](#void)
      - [`never`](#never)
    - [Rest Parameters and Arguments](#rest-parameters-and-arguments)
    - [Parameter Destructuring](#parameter-destructuring)
  - [Generics](#generics)
  - [Conditional Types](#conditional-types)
  - [Mapped Types](#mapped-types)
  - [Intersection](#intersection)
  - [Interfaces](#interfaces)
    - [Extending Interfaces](#extending-interfaces)
    - [Implementing an Interface](#implementing-an-interface)
    - [Optional Properties in Interfaces](#optional-properties-in-interfaces)
    - [Readonly Properties in Interfaces](#readonly-properties-in-interfaces)
    - [Function Signatures in Interfaces](#function-signatures-in-interfaces)
    - [Dynamic Property Names in Interfaces](#dynamic-property-names-in-interfaces)
  - [Differences Between Type Aliases and Interfaces](#differences-between-type-aliases-and-interfaces)
  - [Tuples](#tuples)
  - [Enums](#enums)
  - [Utility Types](#utility-types)
  - [DOM](#dom)
  - [The `declare` keyword](#the-declare-keyword)
  - [Decorators (Not Ready)](#decorators-not-ready)
    - [Class Decorators](#class-decorators)
    - [Decorator Composition](#decorator-composition)
    - [Decorator Factories](#decorator-factories)
    - [Property Decorators](#property-decorators)
    - [Accessor Decorators](#accessor-decorators)
    - [Method Decorators](#method-decorators)
    - [Parameter Decorators](#parameter-decorators)

---

---

## Useful Links

- [TypeScript Official](https://www.typescriptlang.org/)
- [Book: Exploring TypeScript](https://exploringjs.com/ts/)
- [FreeCodeCamp/Learn TypeScript – A Handbook for Developers](https://www.freecodecamp.org/news/learn-typescript-with-react-handbook/)
- [FreeCodeCamp/The Definitive TypeScript Handbook](https://www.freecodecamp.org/news/the-definitive-typescript-handbook/)
- [Playlist: Typescript Tutorial for Beginners](https://www.youtube.com/playlist?list=PLngoRLGHq3kB9X2UoGzg9DZcTS6xssl3L)
- [Playlist: JavaScript, Typescript, Python, Go & Rust - Zero to Interview Ready](https://www.youtube.com/playlist?list=PLngoRLGHq3kAJ2PDn9T1AegX2ZMyaEydj)
- [Mimo/TypeScript](https://mimo.org/glossary/typescript)
- [Playlist: Type Challenges](https://www.youtube.com/playlist?list=PLOlZuxYbPik180vcJfsAM6xHYLVxrEgHC)
- [Playlist: React TypeScript Tutorial for Beginners](https://www.youtube.com/playlist?list=PLC3y8-rFHvwi1AXijGTKM0BKtHzVC-LSK)
- [The TypeScript Course for JS Devs](https://www.youtube.com/watch?v=K01hLNDdqg4)
- [TypeScript in React - COMPLETE Tutorial (Crash Course)](https://www.youtube.com/watch?v=TPACABQTHvM)
- [All The Typescript You Need to Know For React Development - Learn TS For React in 50 Minutes](https://www.youtube.com/watch?v=665UnOGx3Pg)

---

---

## Intro

The goal of TypeScript is to be a static typechecker for JavaScript programs - in other words, a tool that runs before your code runs (static) and ensures that the types of the program are correct (typechecked).

You’ll see that there are two syntaxes for building types: Interfaces and Types. **You should prefer interface**. Use type when you need specific features.

---

---

## tsconfig

The presence of a tsconfig.json file in a directory indicates that the directory is the root of a TypeScript project. The tsconfig.json file specifies the root files and the compiler options required to compile the project.

If we are starting a TSConfig from scratch, we may want to consider using `tsc --init` to bootstrap or use a TSConfig base. `tsc --init` creates a TSConfig file with some predetermined options.

---

### Transpiling Files

A project is compiled in one of the following ways:

- By invoking `tsc` with no input files, in which case the compiler searches for the tsconfig.json file starting in the current directory and continuing up the parent directory chain.
- By invoking `tsc` with no input files and a `--project` (or just `-p`) command line option that specifies the path of a directory containing a tsconfig.json file, or a path to a valid .json file containing the configurations.

Instead of running `tsc` every time that we'd like to transpile, we can run `tsc --watch`, which would transpile the `.ts` file every time that we save it.

---

### Some TSConfig Options

[TSConfig Reference](https://www.typescriptlang.org/tsconfig/) is helpful to understand the options available in the TSConfig file. Here are short explanations for some of the options:

- `skipLibCheck`. Skips checking the types of `.d.ts` files. This is important for performance, because otherwise all `node_modules` will be checked.
- `target`. The version of JavaScript you're targeting. For example, `es2022`, `esnext`, etc.
- `allowJs`. Allow JavaScript files to be imported inside your project, instead of just `.ts` and `.tsx` files.
- `resolveJsonModule`. Allows importing modules with a `.json` extension, which is a common practice in node projects.
- `moduleDetection`: This option forces TypeScript to consider all files as modules. When TypeScript doesn't see an `import` or `export`, it considers the file to be a script, not a module. Scripts are loaded into the global scope of browsers via the `<script />` tag - so any code we write here is at the same scope as globals like `window` and `document`. Sometimes this causes an error. For example, you might have instatiated variables with the same name in different files. When TypeScript considers both files as scripts and load them to the same - global - scope, you end up having an error due to trying to initate a variable that already exists. If you're in a project where every file is a module, not a script, changing `moduleDetection` to `force` might be helpful.
- `strict`: Enables all strict type checking options.
- `noUncheckedIndexedAccess`: Prevents you from accessing an array or object without first checking if it's defined.
- `lib`: Tells TypeScript what built-in types to include. `dom` and `dom.iterable` give you types for `window`, `document` etc.
- `rootDir` and `outDir`. By default, if we compile index.ts, TypeScript puts the resulting index.js right next to it in the same folder. As our project grows, our folder will become a mess of .ts and .js files mixed together. Setting `"outDir": "./dist"` tells TypeScript to put all the generated 'production' JavaScript into a separate folder called dist. In the same manner, to have all the .ts files together, we usually set `"rooDir": ".src/"`.

---

---

## Type Annotations and Type Inference

When we declare a variable using `const`, `var`, or `let`, we can optionally add a type annotation to explicitly specify the type of the variable:

```ts
let name: string = "some name";
name.toUpperCase();

name.toFixed();
// error
// Property 'toFixed' does not exist on type 'string'

let num: number = 9.92;
num.toFixed();
```

When we don't explicitly annotate the type, TypeScript can infer the type. Type inference in TypeScript is a powerful feature that allows the TypeScript compiler to automatically determine the type of a variable based on the value assigned to it.

```ts
let str = "string";
str.toUpperCase();

str.toFixed();
// error
// Property 'toFixed' does not exist on type 'string'
```

We can also access the type of a property by looking it up by name:

```ts
type AppConfig = {
  username: string;
  layout: string;
};

type Username = AppConfig["username"];
```

In this case, the resolved type of `Username` is `string`.

---

---

## Primitive Types

### `string`, `number`, and `boolean`

JavaScript has various primitive values: string, number, bigint, boolean, symbol, null, or undefined. Each has a corresponding type in TypeScript. Here are some that are used more frequently:

- `string`: Represents text values.
- `number`: Represents numeric values (both integers and floating-point numbers).
- `boolean`: Represents a value that is either `true` or `false`.

```ts
let isLoggedIn: boolean = false;
isLoggedIn = true;
```

---

### `null` and `undefined`

JavaScript has two primitive values used to signal absent or uninitialized value: `null` and `undefined`. TypeScript has two corresponding types by the same names. How these types behave depends on whether we have the `strictNullChecks` option on.

#### `strictNullChecks` off

With `strictNullChecks` off, values that might be `null` or `undefined` can still be accessed normally, and the values `null` and `undefined` can be assigned to a property of any type. This is similar to how languages without null checks (e.g. C#, Java) behave. The lack of checking for these values tends to be a major source of bugs; we always recommend people turn `strictNullChecks` on if it’s practical to do so in their codebase.

```ts
// With strictNullChecks OFF, null and undefined can be assigned to any type
let name: string = "John";
name = null; // Allowed - no compile error
name = undefined; // Allowed - no compile error

let age: number = 25;
age = null; // Allowed
age = undefined; // Allowed

// You can access methods without checking
let message: string = "Hello";
console.log(message.toUpperCase()); // Works fine

// Even if variable might be null
let optionalName: string | null = null;
console.log(optionalName.toUpperCase()); // Runtime error!
// But compiles without errors when strictNullChecks is OFF
```

#### `strictNullChecks` on

With `strictNullChecks` on, when a value is `null` or `undefined`, we will need to test for those values before using methods or properties on that value. Just like checking for `undefined` before using an optional property, we can use **narrowing** to check for values that might be null:

```ts
// With strictNullChecks ON, you must explicitly handle null/undefined values

// This will cause a compile error if strictNullChecks is ON
let name: string = "John";
// name = null;        // Error: Type 'null' is not assignable to type 'string'
// name = undefined;   // Error: Type 'undefined' is not assignable to type 'string'

// You must use union types to allow null/undefined
let optionalName: string | null = null;
let optionalAge: number | undefined = undefined;

// You must check before using
if (optionalName !== null) {
  console.log(optionalName.toUpperCase()); // Safe - TypeScript knows it's a string here
}

// Or use optional chaining (ES2020+)
console.log(optionalName?.toUpperCase()); // Safe - returns undefined if null

// Type narrowing with typeof
function processValue(value: string | null | undefined) {
  if (value === null) {
    return "Got null";
  } else if (value === undefined) {
    return "Got undefined";
  } else {
    // TypeScript now knows value is a string here
    return value.toUpperCase();
  }
}
```

#### Non-null Assertion Operator (Postfix `!`)

TypeScript also has a special syntax for removing `null` and `undefined` from a type without doing any explicit checking. Writing `!` after any expression is effectively a type assertion that the value isn’t `null` or `undefined`:

```ts
function func(x?: number | null) {
  // No error
  console.log(x!.toFixed());
}
```

Just like other type assertions, this doesn’t change the runtime behavior of your code, so it’s important to only use `!` when you know that the value can’t be `null` or `undefined`.

---

---

## Literal Types

We can also have literal types in TypeScript. Literal type is when a variable has a specific value as a type. For example, because `const` won't let to change the value of the below string variable, the value of the variable is a literal type.

```ts
const str = "Specific string";

str = "This won't work";

let str2 = "Any string";
str2 = "This works, because type str2 is string not a specific string value";
```

Here is another way of specifying a literal string type:

```ts
let str: "Specific string" = "Specific string";

str = "This won't work";
```

Here is an example of a literal number type:

```ts
const num = 1;

// This won't work
num = 2;
```

---

---

## Union

A union type is a type formed from two or more other types, representing values that may be any one of those types. We refer to each of these types as the union’s members.

Let’s write a function that can operate on strings or numbers:

```ts
function printId(id: number | string) {
  console.log("Your ID is: " + id);
}
// OK
printId(101);
// OK
printId("202");
// Error
printId({ myID: 22342 });
// Argument of type '{ myID: number; }' is not assignable to parameter of type 'string | number'.
```

The separator of the union members is allowed before the first element, so you could also write this: `| string | number | boolean`.

---

---

## Narrowing

TypeScript will only allow an operation if it is valid for every member of the union. For example, if you have the union `string | number`, you can’t use methods that are only available on string:

```ts
function printId(id: number | string) {
  console.log(id.toUpperCase());
  // Property 'toUpperCase' does not exist on type 'string | number'.
  // Property 'toUpperCase' does not exist on type 'number'.
}
```

The solution is to narrow the union with code, the same as you would in JavaScript without type annotations. Narrowing occurs when TypeScript can deduce a more specific type for a value based on the structure of the code.

Type Guards allow you to narrow down the type of an object within a conditional block. For example, TypeScript knows that only a string value will have a `typeof` value "string":

```ts
function printId(id: number | string) {
  if (typeof id === "string") {
    // In this branch, id is of type 'string'
    console.log(id.toUpperCase());
  } else {
    // Here, id is of type 'number'
    console.log(id);
  }
}
```

`instanceof` is another type guard that could help with narrowing:

```ts
class MyResponse {
  result = "result example";
}
class MyError {
  message = "message example";
}
function example(x: MyResponse | MyError) {
  if (x instanceof MyResponse) {
    console.log(x.message); // Error! Property 'message' does not exist on type 'MyResponse'.
    console.log(x.result); // Okay
  } else {
    // TypeScript knows this must be MyError

    console.log(x.message); // Okay
    console.log(x.result); // Error! Property 'result' does not exist on type 'MyError'.
  }
}
```

The `in` operator checks for the existence of a property on an object.

```ts
type Student = {
  name: string;
  grade: number;
  subject: string;
};

type Professor = {
  name: string;
  subject: string;
};

const student: Student = {
  name: "John",
  grade: 85,
  subject: "Math",
};

const professor: Professor = {
  name: "Smith",
  subject: "Math",
};

function greetSomeone(x: Student | Professor) {
  if ("grade" in x) {
    console.log(`Hi, ${x.name}`);
  } else {
    console.log(`Hi, professor ${x.name}`);
  }
}

greetSomeone(student);
greetSomeone(professor);
```

Another example is to use a function like `Array.isArray`:

```ts
function func(x: string[] | string) {
  if (Array.isArray(x)) {
    console.log(x.join(", "));
  } else {
    console.log(`${x} is a string`);
  }
}

func([1, 2]);
func("Hello");
```

Notice that in the else branch, we don’t need to do anything special - if `x` wasn’t a `string[]`, then it must have been a `string`.

Sometimes you’ll have a union where all the members have something in common. For example, both arrays and strings have a `slice` method. If every member in a union has a property in common, you can use that property without narrowing:

```ts
// Return type is inferred as number[] | string
function getFirstThree(x: number[] | string) {
  return x.slice(0, 3);
}
```

---

---

## Type Assertion

TypeScript allows you to override its inferred types in any way you want to. This is used when you have a better understanding of a variable type than the compiler on its own.

```ts
let value: unknown = "Hello, TypeScript!";

// Using type assertion to treat 'value' as a string
let strLength: number = (value as string).length;

console.log(strLength); // Output: 18
```

Here, value is initially `unknown`, but type assertion (`as string`) allows treating it as a string.

And here’s an alternative way to write type assertion:

```ts
let num = <number>10;
console.log(num); // Output: 10
```

The `<number>` syntax also performs type assertion. This was the original syntax for type assertion. But this created an ambiguity when used in JSX. Therefore it is recommended to use `as` instead.

---

---

## The `satisfies` Operator

The `satisfies` operator tells whether a given type satisfies a particular condition. Let's say, a particular code have an inferred type and we want to avoid changing that type. At the same time, we would like the code to be type checked against an existing type. The `satisfies` operator helps with this. It doesn't assert the type but it takes the existing code into account and still checks if a code satisfies a specific type.

The key detail is that type annotation (`const x: Type`) forces a type, while `satisfies` validates the type without losing the specific inference.

Here is an example:

```ts
type Config = {
  endpoint: string;
  timeout?: number;
};

/* 
// Using Type Annotation
const appConfigAlt: Config = {
  endpoint: "https://api.example.com",
  timeout: 5000,
};

// ERROR: Object is possibly 'undefined'. 
// TS only knows it's a 'Config', and in 'Config', timeout is optional.
console.log(appConfigAlt.timeout.toFixed());  
*/

// Using 'satisfies'
const appConfig = {
  endpoint: "https://api.example.com",
  timeout: 5000,
} satisfies Config;

// Because we used 'satisfies', TS knows for SURE that 'timeout' exists here.
// It doesn't treat it as "possibly undefined" like it would with a standard type annotation.
console.log(appConfig.timeout.toFixed());
```

---

---

## Type Predicates

We’ve worked with existing JavaScript constructs to handle narrowing so far, however sometimes you want more direct control over how types change throughout your code. To define a user-defined type guard, we simply need to define a function whose return type is a type predicate.

Predicates in programming are simply functions that return a boolean to answer a yes/no question. Type predicates are a way to make predicates more useful for type narrowing.

```ts
function isString(value: unknown): value is string {
  return typeof value === "string";
}
```

Here the type predicate is value is string. It is saying three things:

- The function is a predicate. So TypeScript will show an error if you try to return anything other than a Boolean value.
- If it returns `true`, then `value` is of type `string`.
- If it returns `false`, then `value` is not of type `string`.

Here is a more elaborate example:

```ts
function isString(value: unknown): value is string {
  return typeof value === "string";
}

function padLeft(padding: number | string, input: string) {
  if (isString(padding)) {
    return padding + input;
    //   ^
    // string
  }
  return " ".repeat(padding) + input;
  //   ^
  // number
}
```

If you are using TypeScript 5.5 or later, you don't have to write the type predicate as the return type of `isString`. TypeScript does it for you, and code like what you see in the example below works perfectly fine:

```ts
function isString(value: unknown) {
  return typeof value === "string";
}

function padLeft(padding: number | string, input: string) {
  if (isString(padding)) {
    return padding + input;
    //   ^
    // string
  }
  return " ".repeat(padding) + input; // Opps type error here
  //   ^
  // number
}
```

---

---

## `any`

TypeScript also has a special type, `any`, that we can use whenever we don’t want a particular value to cause typechecking errors. Using `any` disables all further type checking, and it is assumed we know the environment better than TypeScript.

```ts
let data: any = "a string";
data = 123;
data = { key: "value" };
```

Avoid using `any` whenever possible. Instead, use explicit types or stricter alternatives like `unknown` (if the type cannot be determined upfront).

When we don’t specify a type, and TypeScript can’t infer it from context, the compiler will typically default to `any`. We usually want to avoid this, though, because `any` isn’t type-checked. We can use the compiler flag `noImplicitAny` to flag any implicit `any` as an error.

---

---

## `unknown`

The `unknown` type represents any value. This is similar to the `any` type, but is safer. While both `any` and `unknown` can hold values of any type, `unknown` requires you to perform type checks before using the value. This ensures greater type safety while still offering flexibility.

```ts
function func(input: unknown): string {
  if (typeof input === "string") {
    return `The value is a string: ${input}`;
  } else if (typeof input === "number") {
    return `The value is a number: ${input}`;
  } else {
    return `The value is of an unknown type`;
  }
}

console.log(func("Hello, TypeScript!")); // The value is a string: Hello, TypeScript!
console.log(func(42)); // The value is a number: 42
console.log(func(true)); // The value is of an unknown type
```

---

---

## Arrays

You can also define arrays with type annotations. To specify the type of an array with numbers, you can use the syntax `number[]`. This syntax works for any type (e.g. `string[]` is an array of strings, and so on).

```ts
let strs: string[] = ["string 1", "string 2", "etc"];
let nums: number[] = [1, 2, 3];
let bools: boolean[] = [true, false];
```

An array can also be defined in this way, using generic types. This is less common:

```ts
let arr: Array<number> = [2, 3, 5, 7, 11];
```

---

---

## Object Types

The special type `object` refers to any value that isn’t a primitive (`string`, `number`, `bigint`, `boolean`, `symbol`, `null`, or `undefined`). This is different from the empty object type `{ }`, and also different from the global type `Object`.

Note that in JavaScript, function values are objects: They have properties, have `Object.prototype` in their prototype chain, are `instanceof Object`, you can call `Object.keys` on them, and so on. For this reason, function types are considered to be objects in TypeScript.

To define an object type, we simply list its properties and their types:

```ts
// The parameter's type annotation is an object type
function func(pt: { x: number; y: number }) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
func({ x: 3, y: 7 });
```

You can use `,` or `;` to separate the properties, and the last separator is optional either way.

---

### Optional Properties

Object types can also specify that some or all of their properties are optional. To do this, we add a `?` after the property name:

```ts
function printName(obj: { first: string; last?: string }) {
  console.log(`${obj.first.toUpperCase()} ${obj.last?.toUpperCase() || ""}`);
}
// Both OK
printName({ first: "Bob" });
printName({ first: "Alice", last: "Alisson" });
```

In JavaScript, if you access a property that doesn’t exist, you’ll get the value `undefined` rather than a runtime error. Because of this, when you read from an optional property, you’ll have to check for `undefined` before using it.

For example, this code causes an error:

```ts
function printName(obj: { first: string; last?: string }) {
  // Error - might crash if 'obj.last' wasn't provided!
  console.log(obj.last.toUpperCase());
}
```

Here is one solution:

```ts
function printName(obj: { first: string; last?: string }) {
  // 'obj.last' is possibly 'undefined'.
  if (obj.last !== undefined) {
    // OK
    console.log(obj.last.toUpperCase());
  }
}
```

Here is another solution:

```ts
function printName(obj: { first: string; last?: string }) {
  // A safe alternative using modern JavaScript syntax:
  console.log(obj.last?.toUpperCase());
}
```

---

### The `readonly` Modifier

We can use `readonly` to make the objects and arrays immutable, ensuring their original state cannot be altered.

For example, if you try to change the name or price of any item in the below object, TypeScript throws an error.

```ts
let vegetables: { readonly name: string; readonly price?: number }[] = [
  { name: "Tomato", price: 2 },
  { name: "Potato", price: 1 },
  { name: "Carrot" },
];

console.log(vegetables[2]); // {name: 'Carrot'}
vegetables[2].price = 3; // Error: Cannot assign to 'price' because it is a read-only property.
```

You can also make the entire array immutable by declaring it as readonly:

```ts
let vegetables: readonly { name: string; price?: number }[] = [
  { name: "Tomato", price: 2 },
  { name: "Potato", price: 1 },
  { name: "Carrot" },
];

vegetables.push({ name: "Onion", price: 3 });
// Error: Cannot assign to 'push' because it is a read-only property

vegetables[0] = { name: "New Vegetable" };
// Error: Index signature in type 'readonly [{ name: string; price?: number | undefined; }]' only permits reading

// Since the objects themselves aren't marked as readonly, this is allowed:
vegetables[0].name = "Modified Tomato";
```

The main error occurs when you try to mutate the array itself (like calling `push`, `pop`, `splice`, etc.) or reassign elements in the array. The `readonly` keyword prevents modification of the array structure, even though the individual objects within it can still be modified (unless they're also marked as `readonly`).

---

---

## Classes

You can add types to properties and method’s arguments within classes:

```ts
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  greet(name: string) {
    return `${this.greeting}, ${name}`;
  }
}

const grt = new Greeter("Hello");
console.log(grt.greet("Ziya"));
```

---

### Access Modifiers

Typescript supports public, private, protected modifiers, which determine the accessibility of a class member.

- A **public** member works the same as plain JavaScript members and is the default modifier.
- A **private** member cannot be accessed from outside of its containing class.
- A **protected** member differ from a private as it can also be accessed within deriving classes.

| Accessible on  | public | protected | private |
| -------------- | ------ | --------- | ------- |
| class          | yes    | yes       | yes     |
| class children | yes    | yes       | no      |
| class instance | yes    | no        | no      |

```ts
class Animal {
  public name: string; // Default modifier - accessible everywhere
  private age: number; // Only accessible within this class
  protected species: string; // Accessible within class and derived classes

  constructor(name: string, age: number, species: string) {
    this.name = name;
    this.age = age;
    this.species = species;
  }

  public getAge(): number {
    return this.age; // Can access private member within same class
  }
}

class Dog extends Animal {
  public breed: string;

  constructor(name: string, age: number, breed: string) {
    super(name, age, "mammal");
    this.breed = breed;
  }

  public showInfo(): void {
    console.log(`Name: ${this.name}`); // Public - OK
    console.log(`Species: ${this.species}`); // Protected - OK (inherited class)
    // console.log(this.age); // Error - private member not accessible in derived class
  }
}

// Usage examples:
const dog = new Dog("Buddy", 3, "Golden Retriever");

console.log(dog.name); // OK - public
console.log(dog.species); // Error - protected member
console.log(dog.age); // Error - private member

dog.showInfo(); // OK - calls protected member from derived class
```

---

### Parameter properties

Parameter properties lets you create and initialise a member in one place. They are declared by prefixing a constructor parameter with a modifier.

```ts
class Spider {
  constructor(name: string) {
    this.name = name;
  }
}

const spdr = new Spider("Test");
console.log(spdr);
```

---

### Readonly modifier

A `readonly` property must be initialised at their declaration or in the constructor.

```ts
class Spider {
  readonly name: string;
  readonly numberOfLegs: number = 8;

  constructor(name: string) {
    this.name = name;
  }
}

const spdr = new Spider("Test");
console.log(spdr);
```

---

---

## Type Aliases

It’s common to want to use the same type more than once and refer to it by a single name. A type alias is exactly that - a name for any type. The syntax for a type alias is:

Here is another way of specifying an object type:

```ts
type coordinates = {
  x: number;
  y: number;
};

function func(pt: coordinates) {
  console.log(`The coordinate's x value is ${pt.x}`);
  console.log(`The coordinate's y value is ${pt.y}`);
}

func({ x: 3, y: 7 });
```

You can actually use a type alias to give a name to any type at all, not just an object type:

```ts
type ID = number | string;

type SingleTypeArr<Type> = Type[];
```

---

---

## Functions

### Parameter Type Annotations

When you declare a function, you can add type annotations after each parameter to declare what types of parameters the function accepts. Parameter type annotations go after the parameter name:

```ts
// Parameter type annotation
function greet(name: string) {
  console.log(`Hello, ${name.toUpperCase()}!`);
}

greet("Ziya");
```

---

### Parameters with Default Values

This how we can define a default value for a parameter:

```ts
function calculateScore(baseScore: number, deductions: number = 0) {
  return baseScore - deductions;
}

console.log(calculateScore(50, 10)); // 40
console.log(calculateScore(50)); // 50
```

---

### Return Type Annotations

You can also add return type annotations. Return type annotations appear after the parameter list:

```ts
function getNumber(): number {
  return Math.floor(Math.random() * 100) + 1;
}

console.log(getNumber());
```

Much like variable type annotations, you usually don’t need a return type annotation because TypeScript will infer the function’s return type based on its return statements.

---

### Functions Which Return Promises

If you want to annotate the return type of a function which returns a promise, you should use the `Promise` type:

```ts
function fetchData(): Promise<string> {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data loaded successfully!");
    }, 1000);
  });
}

fetchData().then((result) => {
  console.log(result);
});
```

---

### Function Type Expressions

If a function's parameter is another function, we can specify a type for that as well:

```ts
function greeter(fn: (a: string) => void) {
  fn("Hello, World");
}

function printToConsole(s: string) {
  console.log(s);
}

greeter(printToConsole);
```

The syntax `(a: string) => void` means “a function with one parameter, named `a`, of type `string`, that doesn’t have a return value”.

---

### Type Aliased Functions

We can use a type alias to name a function type:

```ts
type MathOperation = (a: number, b: number) => number;

const add: MathOperation = (x, y) => x + y;
const mulptiply: MathOperation = (x, y) => x * y;

console.log(add(2, 5)); // 7
console.log(mulptiply(2, 5)); // 10
```

---

### Call Signatures

In JavaScript, functions are objects, so they can have properties. But a plain function type expression like `(name: string) => string` can't describe a property. A call signature lets you describe a function that also has properties. Here's an example:

```ts
// Define a type with a call signature AND a property
type GreeterFunction = {
  description: string; // a property
  (name: string): string; // the call signature (note: uses `:` not `=>`)
};

// Create a function that matches this type
const greet: GreeterFunction = (name) => {
  return `Hello, ${name}!`;
};

greet.description = "A friendly greeter";

// Usage
console.log(greet("Alice")); // "Hello, Alice!"
console.log(greet.description); // "A friendly greeter"
```

Think of it like a function that acts as a logger — it can be called to log a message, but also has a `.logCount` property tracking how many times it's been called.

---

### Construct Signatures

JavaScript functions can also be invoked with the new operator. TypeScript refers to these as constructors because they usually create a new object. You can write a construct signature by adding the `new` keyword in front of a call signature

```ts
// Define a construct signature for a class
type UserConstructor = {
  new (name: string, age: number): User;
};

// The User class
class User {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet() {
    return `Hi, I'm ${this.name}`;
  }
}

// A factory function that accepts any constructor matching UserConstructor
function createUser(ctor: UserConstructor, name: string, age: number): User {
  return new ctor(name, age);
}

// Usage
const user = createUser(User, "Alice", 30);
console.log(user.greet()); // "Hi, I'm Alice"
```

---

### Function Overloads

TypeScript allows you to declare function overloads. Basically, you can have multiple functions with the same name but different parameter types and return type. Consider the following example:

```ts
// Overload signatures
function greet(name: string): string;
function greet(name: string, greeting: string): string;

// Implementation
function greet(name: string, greeting?: string): string {
  if (greeting) {
    return `${greeting}, ${name}!`;
  }
  return `Hello, ${name}!`;
}

// Usage examples
greet("Alice"); // Works - returns "Hello, Alice!"
greet("Bob", "Hi"); // Works - returns "Hi, Bob!"
// greet("Charlie", "Hey", "extra"); // Error! Too many arguments
```

Here is another example with different types of parameters:

```ts
// Overload signatures
function add(a: number, b: number): number;
function add(a: string, b: string): string;

// Implementation
function add(a: number | string, b: number | string): number | string {
  if (typeof a === "number" && typeof b === "number") {
    return a + b;
  }
  return a.toString() + b.toString();
}

// Usage
add(1, 2); // Returns 3 (number)
add("hello", "world"); // Returns "helloworld" (string)
```

---

### Other Function-related Types to Know About

There are some additional types you’ll want to recognize that appear often when working with function types. Like all types, you can use them everywhere, but these are especially relevant in the context of functions.

#### `void`

`void` represents the return value of functions which don’t return a value. It’s the inferred type any time a function doesn’t have any return statements, or doesn’t return any explicit value from those return statements:

```ts
// The inferred return type is void
function logMessage(message: string) {
  console.log(`${message} - posted at ${new Date()}`);
}

logMessage("Hello");
```

Instead of letting TypeScript infer the return value of the function, we can also explicitly indicate the return tyoe to be `void`:

```ts
// This function explicitly states it returns void
function logMessage(message: string): void {
  console.log(`${message} - posted at ${new Date()}`);
}

logMessage("Hello");
```

In JavaScript, a function that doesn’t return any value will implicitly return the value `undefined`. However, `void` and `undefined` are not the same thing in TypeScript.

#### `never`

In TypeScript, `never` is treated as the “no-value” type. You will often see it being used as a dead-end type. For example, some functions never return a value:

```ts
function fail(msg: string): never {
  throw new Error(msg);
}
```

The `never` type represents values which are never observed. In a return type, this means that the function throws an exception or terminates execution of the program.

`never` also appears when TypeScript determines there’s nothing left in a union.

```ts
function fn(x: string | number) {
  if (typeof x === "string") {
    // do something
  } else if (typeof x === "number") {
    // do something else
  } else {
    x; // has type 'never'!
  }
}
```

---

### Rest Parameters and Arguments

In addition to using optional parameters or overloads to make functions that can accept a variety of fixed argument counts, we can also define functions that take an unbounded number of arguments using rest parameters.

A rest parameter appears after all other parameters, and uses the `...` syntax:

```ts
function multiply(n: number, ...m: number[]) {
  return m.map((x) => n * x);
}
// 'a' gets value [10, 20, 30, 40]
const a = multiply(10, 1, 2, 3, 4);
```

Here is another example where we use rest parameters to merge multiple arrays into one:

```ts
function mergeArrays(...arrays: number[][]): number[] {
  return arrays.flat();
}

let combined = mergeArrays([1, 2], [3, 4], [5, 6]);
console.log(combined); // [1, 2, 3, 4, 5, 6]
```

---

### Parameter Destructuring

When we're working with objects, we can destructure the object directly within the function parameters. This is useful when we want to extract specific properties from the object.

```ts
const user = {
  name: "Alice",
  age: 25,
};

function printUser({ name, age }: { name: string; age: number }) {
  console.log(`Name: ${name}, Age: ${age}`);
}

printUser(user);
```

If one function receives an array as a parameter, we can destructure the array directly within the function parameters. This allows us to extract specific elements from the array.

```ts
const values: number[] = [1, 2, 3];

function printValues([value1, value2]: number[]) {
  console.log(`value1: ${value1}, value2: ${value2}`);
}

printValues(values);
```

TypeScript allows us to provide default values for destructured parameters. This is useful when we want to provide values if a property or element is missing.

```ts
function greet(name: string = "Test") {
  console.log(`Hello, ${name}`);
}

greet();
greet("Another Test");
```

---

---

## Generics

In TypeScript, generics are used when we want to describe a correspondence between two values. We do this by declaring a type parameter in the function signature:

```ts
function firstElement<Type>(arr: Type[]): Type | undefined {
  return arr[0];
}
```

By adding a type parameter `Type` to this function and using it in two places, we’ve created a link between the input of the function (the array) and the output (the return value).

We can use multiple type parameters as well. For example, a standalone version of `map` would look like this:

```ts
function map<Input, Output>(
  arr: Input[],
  func: (arg: Input) => Output,
): Output[] {
  return arr.map(func);
}
```

Generics can be used in interfaces to define flexible object structures.

```ts
interface StorageBox<T> {
  content: T;
}

let numberBox: StorageBox<number> = { content: 100 };
let stringBox: StorageBox<string> = { content: "TypeScript" };

console.log(numberBox.content); // Output: 100
console.log(stringBox.content); // Output: "TypeScript"
```

Generics also work in classes, making them more reusable. Here’s an example of a generic queue class:

```ts
class Queue<T> {
  private items: T[] = [];

  enqueue(item: T): void {
    this.items.push(item);
  }

  dequeue(): T | undefined {
    return this.items.shift();
  }
}

let numberQueue = new Queue<number>();
numberQueue.enqueue(10);
numberQueue.enqueue(20);
console.log(numberQueue.dequeue()); // Output: 10

let stringQueue = new Queue<string>();
stringQueue.enqueue("Hello");
stringQueue.enqueue("World");
console.log(stringQueue.dequeue()); // Output: "Hello"
```

Sometimes we want to relate two values, but can only operate on a certain subset of values. In this case, we can use a constraint to limit the kinds of types that a type parameter can accept. Let’s write a function that returns the longer of two values. To do this, we need a `length` property that’s a number. We constrain the type parameter to that type by writing an `extends` clause:

```ts
function longest<Type extends { length: number }>(a: Type, b: Type) {
  if (a.length >= b.length) {
    return a;
  } else {
    return b;
  }
}

console.log(longest([1, 2], [1, 2, 3]));
// longerArray is of type 'number[]'
console.log(longest("short", "longer"));
// longerString is of type 'alice' | 'bob'

console.log(longest(10, 20));
// Error! Numbers don't have a 'length' property
// Argument of type 'number' is not assignable to parameter of type '{ length: number; }'.
```

The `keyof` type operator can be used as a constraint to ensure valid property names. Here’s an example of getting a property value by name:

```ts
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

let user = { name: "Alice", age: 30 };

console.log(getProperty(user, "name")); // Output: "Alice"
console.log(getProperty(user, "age")); // Output: 30
```

JavaScript already has a `typeof` operator you can use in an expression context. TypeScript adds a `typeof` type operator you can use in a **type context** to refer to the type of a variable or property:

```ts
// Create variables
const userName = "Alice";
const userAge = 30;
const isActive = true;

// Use typeof to create types
type NameType = typeof userName; // string
type AgeType = typeof userAge; // number
type IsActiveType = typeof isActive; // boolean

// Now use these types as parameter types
function processUser(name: NameType, age: AgeType, active: IsActiveType) {
  console.log(`Name: ${name}, Age: ${age}, Active: ${active}`);
}

// Usage - TypeScript will check the types
processUser("Bob", 25, false); // Works
// processUser(123, "25", true);      // Error - wrong types
```

TypeScript intentionally limits the sorts of expressions you can use `typeof` on. Specifically, it’s only legal to use `typeof` on identifiers (i.e. variable names) or their properties.

---

---

## Conditional Types

A conditional type describes a type relationship test and selects one of two possible types, depending on the outcome of that test.

```ts
SomeType extends OtherType ? TrueType : FalseType;
```

When the type on the left of the `extends` is assignable to the one on the right, then you’ll get the type in the first branch (the “true” branch); otherwise you’ll get the type in the latter branch (the “false” branch).

The power of conditional types comes from using them with generics.

```ts
// Create a conditional type that checks if something is a function
type IsFunction<T> = T extends (...args: any[]) => any ? true : false;

// Usage examples
type A = IsFunction<() => void>; // true
type B = IsFunction<(x: number) => string>; // true
type C = IsFunction<string>; // false
type D = IsFunction<number>; // false

// Use it in a function
function checkType<T>(value: T): IsFunction<T> {
  return (typeof value === "function") as IsFunction<T>;
}

// Calling the function
checkType(() => console.log("hi")); // returns true
checkType("hello"); // returns false
checkType(42); // returns false
```

Conditional types can be recursive; that is, one, or both, of the branches can themselves be a conditional type:

```ts
type Recursive<T> = T extends string[]
  ? string
  : T extends number[]
    ? number
    : never;

const a: Recursive<string[]> = "10"; // works
const b: Recursive<string> = 10; // Error: Type 'number' is not assignable to t
```

The conditional typing and `infer` keyword in TypeScript allow us to take a type and isolate any piece of it for later use. In the below example, we capture a function's return type into a new type.

```ts
function addNumbers(x: number, y: number): number {
  return x + y;
}

type GetReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

// Get the return types
type AddNumbersReturnType = GetReturnType<typeof addNumbers>; // type will be 'number'
let num: AddNumbersReturnType = 123;
```

The `infer` keyword compliments conditional types and cannot be used outside an `extends` clause.

---

---

## Mapped Types

Using mapped types in a program is especially useful when there is a need for a type to be derived from (and remain in sync with) another type.

Before looking at mapped types, let's talk about index signature. Index signatures are handy for cases when the actual names of the type’s properties are not known, but the type of data they will reference is known:

```ts
type User = {
  name: string;
  preferences: {
    [key: string]: string;
  };
};

const currentUser: User = {
  name: "Foo Bar",
  preferences: {
    lang: "en",
  },
};

const currentLang = currentUser.preferences.lang;
```

In this example, the TypeScript compiler reports that the type of `currentLang` is `string` rather than `any`. This functionality, in conjunction with the `keyof` type operator, is one of the core components that make mapped types possible.

Mapped types are a feature in TypeScript which allow you to map over a union of types to create a new type.

The syntax looks like this:

```ts
type Fruit = "apple" | "banana" | "orange";

type NewType = {
  [F in Fruit]: {
    name: F;
  };
};
/**
 * {
 *   apple: { name: "apple" };
 *   banana: { name: "banana" };
 *   orange: { name: "orange" };
 * }
 */
```

Using the `keyof` type operator with mapped types gives us an ability to create object types from other object types.

```ts
interface Person {
  name: string;
  age: number;
}

type NullablePerson = {
  [P in keyof Person]: Person[P] | null;
};

/**
 * {
 *   name: string | null;
 *   age: number | null;
 * }
 */
```

Sometimes, you'll have a union of things which can't be assigned to the key of an object. For instance, a union of objects:

```ts
type Event =
  | {
      type: "click";
      x: number;
      y: number;
    }
  | {
      type: "hover";
      element: HTMLElement;
    };
```

Here, you can see that `Event` is a union of two objects. If we tried to do `[E in Event]`, we'd get an error:

To get around this, we can use the `as` keyword to tell TypeScript that we want to use the `type` property of each `E` as we iterate over it:

```ts
type EventMap = {
  [E in Event as E["type"]]: (event: E) => void;
};

/**
 * {
 *   click: (event: { type: "click"; x: number; y: number; }) => void;
 *   hover: (event: { type: "hover"; element: HTMLElement; }) => void;
 * }
 */
```

There are two additional modifiers which can be applied during mapping: `readonly` and `?` which affect mutability and optionality respectively.

You can remove or add these modifiers by prefixing with `-` or `+`. If you don’t add a prefix, then `+` is assumed.

---

---

## Intersection

An Intersection Type is a powerful feature in TypeScript that allows you to combine multiple types into one. To define an intersection type, you use the `&` operator to combine two or more types.

```ts
type User = {
  name: string;
  age: number;
};

type Address = {
  city: string;
  country: string;
};

type UserWithAddress = User & Address;

function getUserDetails(user: UserWithAddress): string {
  return `${user.name} (${user.age} years old), lives in ${user.city}, ${user.country}`;
}

const user: UserWithAddress = {
  name: "Alice",
  age: 30,
  city: "New York",
  country: "USA",
};

console.log(getUserDetails(user));
// Output: "Alice (30 years old), lives in New York, USA"
```

---

---

## Interfaces

An interface declaration is another way to name an object type:

```ts
interface User {
  name: string;
  age: number;
}

function getUserInfo(user: User): string {
  return `${user.name} (age: ${user.age})`;
}

const user: User = {
  name: "Alice",
  age: 25,
};

console.log(getUserInfo(user));
// Alice (age: 25)
```

Just like when we use a type alias, the example works just as if we had used an anonymous object type. TypeScript is only concerned with the structure of the value we passed; it only cares that it has the expected properties. Being concerned only with the structure and capabilities of types is why we call TypeScript a structurally typed type system.

---

### Extending Interfaces

```ts
interface Address {
  city: string;
  country: string;
}

interface User extends Address {
  name: string;
  age: number;
}

const user: User = {
  name: "Alice",
  age: 30,
  city: "New York",
  country: "USA",
};
```

An interface can extend multiple interfaces:

```ts
interface A {
  propA: string;
}

interface B {
  propB: number;
}

interface C extends A, B {
  propC: boolean;
}

const obj: C = {
  propA: "Hello",
  propB: 42,
  propC: true,
};
```

---

### Implementing an Interface

The `implements` keyword in TypeScript ensures that a class follows the exact structure (properties and methods) defined by an interface.

```ts
interface HasName {
  name: string;
  getName(): string;
}

class Person implements HasName {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  getName(): string {
    return this.name;
  }
}

const person = new Person("Alice");
console.log(person.getName()); // Alice
```

---

### Optional Properties in Interfaces

Interfaces can define properties as optional using the `?` symbol:

```ts
interface User {
  name: string;
  age?: number; // Optional
}

const user1: User = { name: "User 1" };
const user2: User = { name: "User 2", age: 25 };
```

---

### Readonly Properties in Interfaces

We use the `readonly` modifier to make properties immutable:

```ts
interface User {
  readonly id: number;
  name: string;
}

const user: User = { id: 1, name: "User" };
// user.id = 2; // Error: Cannot assign to 'id' because it is a read-only property.
```

---

### Function Signatures in Interfaces

Interfaces can define function signatures:

```ts
interface Add {
  (a: number, b: number): number;
}

const add: Add = (a, b) => a + b;
console.log(add(5, 3)); // Output: 8
```

---

### Dynamic Property Names in Interfaces

Interfaces can define dynamic property names:

```ts
interface StringDictionary {
  [key: string]: string;
}

const dictionary: StringDictionary = {
  hello: "world",
  name: "User",
};
```

---

---

## Differences Between Type Aliases and Interfaces

Type aliases and interfaces are very similar, and in many cases you can choose between them freely. Almost all features of an interface are available in type, the key distinction is that a type cannot be re-opened to add new properties vs an interface which is always extendable.

```ts
// Interface	Type
// Extending an interface
interface Animal {
  name: string;
}

interface Bear extends Animal {
  honey: boolean;
}

function getBear(): Bear {
  return {
    name: "Yogi",
    honey: true,
  };
}

const bear = getBear();
console.log(bear.name);
console.log(bear.honey);
```

```ts
// Extending a type via intersections
type Animal = {
  name: string;
};

type Bear = Animal & {
  honey: boolean;
};

function getBear(): Bear {
  return {
    name: "Yogi",
    honey: true,
  };
}

const bear = getBear();
console.log(bear.name);
console.log(bear.honey);
```

```ts
// Base interface
interface Person {
  name: string;
}

// Adding more properties to the SAME interface
interface Person {
  age: number;
  email: string;
}

// Now you can use it
const user: Person = {
  name: "User",
  age: 25,
  email: "user@example.com",
};

console.log(user.name); // User
console.log(user.age); // 25
console.log(user.email); // user@example.com
```

A type cannot be changed after being created:

```ts
type Person = {
  name: string;
};

type Person = {
  age: number;
  email: string;
};
// Error: Duplicate identifier 'Window'.
```

---

---

## Tuples

A tuple in TypeScript is a special type of array that has a fixed number of elements, where each element can have a different type. Tuples ensure that the order and types of values remain consistent.

```ts
// A tuple with a string and a number
let user: [string, number] = ["User", 25];

console.log(user[0]); // Output: User
console.log(user[1]); // Output: 25
```

A tuple can have optional elements. Here, the third element (boolean) is optional.

```ts
let person: [string, number, boolean?] = ["Bob", 30];

console.log(person); // Output: ["Bob", 30]
```

A tuple can have read-only properties. The `readonly` keyword prevents modifying tuple values.

```ts
const coordinates: readonly [number, number] = [10, 20];
// coordinates[0] = 50; // Error: Cannot assign to '0' because it is a read-only tuple
```

---

---

## Enums

Tuples define fixed-length arrays with different data types, while enums provide named constants for better readability, making your code more structured and type-safe.

Numeric enums are default enums in TypeScript. By default, TypeScript assigns numeric values starting from 0.

```ts
enum Status {
  Pending, // 0
  InProgress, // 1
  Completed, // 2
}

console.log(Status.Pending); // Output: 0
console.log(Status.Completed); // Output: 2
```

`enum` supports reverse mapping which means we can access the value of a member and also a member name from its value:

```ts
enum Status {
  Pending, // 0
  InProgress, // 1
  Completed, // 2
}

console.log(Status.Pending); // Output: 0
console.log(Status[0]); // Output: Pending
```

We can assign custom number values in enums. Here, custom values are assigned to each status:

```ts
enum OrderStatus {
  Pending = 1,
  Shipped = 5,
  Delivered = 10,
}

console.log(OrderStatus.Shipped); // Output: 5
```

We can assign custom string values in enums:

```ts
enum Direction {
  Up = "UP",
  Down = "DOWN",
}

console.log(Direction.Up); // Output: "UP"
```

Here is an example of using enums in a function:

```ts
enum Status {
  Pending, // 0
  InProgress, // 1
  Completed, // 2
}

function getStatusText(status: Status): string {
  switch (status) {
    case Status.Pending:
      return "Order is pending.";
    case Status.InProgress:
      return "Order is in progress.";
    case Status.Completed:
      return "Order is completed.";
    default:
      return "Unknown status.";
  }
}

console.log(getStatusText(Status.InProgress)); // Output: "Order is in progress."
```

It's important to note that in TypeScript 5.8, a new flag `erasableSyntaxOnly` came about. `erasableSyntaxOnly` marks enums, namespaces and class parameter properties as errors. These pieces of syntax are not considered erasable. 'Erasable' syntax means that the syntax can be deleted without the runtime behaviour being affected. Normal type annotations are erasable. Enums, namespaces and class parameter properties do not obey this rule. This makes it much harder for bundlers to work with them. Node's recent TypeScript support, by default, only supports erasable syntax. So turning on `erasableSyntaxOnly` is a good option.

---

---

## Utility Types

TypeScript provides several utility types to facilitate common type transformations. These utilities are available globally.

`Partial<Type>` constructs a type with all properties of `Type` set to optional.

```ts
interface User {
  name: string;
  age: number;
  email: string;
}

// Original interface
const user1: User = {
  name: "Alice",
  age: 30,
  email: "alice@example.com",
};

// Using Partial - all properties become optional
const user2: Partial<User> = {
  name: "Bob",
  // age and email are optional, so we don't need to provide them
};
```

You can also create a function that accepts partial data:

```ts
interface User {
  name: string;
  age: number;
  email: string;
}

function updateUser(user: Partial<User>) {
  // This function can accept any subset of User properties
  console.log(user);
}

updateUser({ name: "Charlie" }); // Works!
updateUser({ age: 25 }); // Works!
updateUser({}); // Works! (empty object)
```

`Required<Type>` constructs a type consisting of all properties of `Type` set to required. The opposite of `Partial`.

```ts
interface User {
  name?: string;
  age?: number;
  email?: string;
}

// Original interface with optional properties (notice the ?)
const user1: User = {
  name: "Alice",
  // age and email are optional, so we don't need to provide them
};

// Using Required - all properties become required
const user2: Required<User> = {
  name: "Bob",
  age: 30,
  email: "bob@example.com",
  // ALL properties are now REQUIRED
};

// You can also create a function that requires all properties
function createUser(user: Required<User>) {
  // This function MUST receive ALL properties
  console.log(user.name, user.age, user.email);
}

createUser({
  name: "Charlie",
  age: 35,
  email: "charlie@example.com",
}); // Works!

// createUser({ name: "David" }); // ERROR! Missing age and email
```

`Readonly<Type>` constructs a type with all properties of `Type` set to `readonly`, meaning the properties of the constructed type cannot be reassigned.

```ts
interface User {
  name: string;
  age: number;
}

// Original interface
const user: User = {
  name: "Alice",
  age: 30,
};

// This works - we can change the values
user.name = "Bob"; // OK
user.age = 35; // OK

// Using Readonly - properties become read-only
const readonlyUser: Readonly<User> = {
  name: "Charlie",
  age: 40,
};

// This will cause a compile error - cannot reassign
// readonlyUser.name = "David"; // ERROR!
// readonlyUser.age = 45;       // ERROR!

// You can still create a new object with updated values
const newUser: User = {
  ...readonlyUser,
  name: "David", // This creates a NEW object
};
```

`Record<Keys, Type>` constructs an object type whose property keys are `Keys` and whose property values are `Type`.

```ts
// Create an object where keys are strings and values are numbers
type ScoreRecord = Record<string, number>;

const scores: ScoreRecord = {
  Alice: 95,
  Bob: 87,
  Charlie: 92,
};

// You can also use it with specific key types
type StatusRecord = Record<"pending" | "approved" | "rejected", boolean>;

const status: StatusRecord = {
  pending: true,
  approved: false,
  rejected: false,
};

// Access values
console.log(scores["Alice"]); // 95
console.log(status.pending); // true

// You can also create it dynamically
const dynamicRecord: Record<string, string> = {};
dynamicRecord["name"] = "John";
dynamicRecord["city"] = "New York";
```

`Pick<Type, Keys>` constructs a type by picking the set of properties `Keys` (string literal or union of string literals) from `Type`.

```ts
interface User {
  name: string;
  age: number;
  email: string;
  password: string;
  createdAt: Date;
}

// Pick only specific properties from the User interface
type UserBasicInfo = Pick<User, "name" | "email">;

const user: UserBasicInfo = {
  name: "Alice",
  email: "alice@example.com",
};

// This works - we can only use the picked properties
console.log(user.name); // Alice
console.log(user.email); // alice@example.com

// This would cause an error - password and age are not available
// user.age = 30; // ERROR!

// You can also pick a single property
type UserName = Pick<User, "name">;
const userName: UserName = { name: "Bob" };

// Or pick multiple properties
type UserImportant = Pick<User, "name" | "email" | "createdAt">;
```

`Omit<Type, Keys>` constructs a type by picking all properties from `Type` and then removing `Keys` (string literal or union of string literals). The opposite of `Pick`.

```ts
interface User {
  name: string;
  age: number;
  email: string;
  password: string;
  createdAt: Date;
}

// Omit removes specific properties from the User interface
type UserPublicInfo = Omit<User, "password" | "createdAt">;

const user: UserPublicInfo = {
  name: "Alice",
  age: 30,
  email: "alice@example.com",
  // password and createdAt are NOT included
};

// This works - we can use the remaining properties
console.log(user.name); // Alice
console.log(user.age); // 30
console.log(user.email); // alice@example.com

// This would cause an error - password and createdAt are not available
// user.password = "secret"; // ERROR!
// user.createdAt = new Date(); // ERROR!

// You can also omit a single property
type UserNoEmail = Omit<User, "email">;
const userNoEmail: UserNoEmail = {
  name: "Bob",
  age: 25,
  password: "pass123",
  createdAt: new Date(),
};
```

`Exclude<UnionType, ExcludedMembers>` constructs a type by excluding from `UnionType` all union members that are assignable to `ExcludedMembers`.

```ts
// Define a union type
type Status = "pending" | "approved" | "rejected" | "cancelled";

// Exclude some members from the union
type ActiveStatus = Exclude<Status, "rejected" | "cancelled">;

const active: ActiveStatus = "pending"; // OK
const active2: ActiveStatus = "approved"; // OK

// This would cause an error - excluded members are not allowed
// const inactive: ActiveStatus = 'rejected'; // ERROR!
// const inactive2: ActiveStatus = 'cancelled'; // ERROR!
```

`Extract<Type, Union>` constructs a type by extracting from `Type` all union members that are assignable to `Union`.

```ts
type AllDigits = 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9;

// Extract specific members from the union
type EvenDigits = Extract<AllDigits, 2 | 4 | 6 | 8>; // Gets only even numbers

const even: EvenDigits = 2; // OK
const even2: EvenDigits = 6; // OK

// This would cause an error
// const odd: EvenDigits = 3; // ERROR!
// const odd2: EvenDigits = 7; // ERROR!
```

`NonNullable<Type>` constructs a type by excluding `null` and `undefined` from `Type`.

```ts
// Define a type that can be null or undefined
type Name = string | null | undefined;

// Remove null and undefined from the type
type RequiredName = NonNullable<Name>;

const name1: RequiredName = "Alice"; // OK - string
// const name2: RequiredName = null;   // ERROR! Can't be null
// const name3: RequiredName = undefined; // ERROR! Can't be undefined

// You can also use it with more complex types
type User = {
  name: string;
  age: number | null;
  email: string | undefined;
};

type CleanUser = {
  name: string;
  age: NonNullable<User["age"]>; // This will be just number (no null)
  email: NonNullable<User["email"]>; // This will be just string (no undefined)
};

const user: CleanUser = {
  name: "Bob",
  age: 30, // OK - no null
  email: "bob@example.com", // OK - no undefined
};
```

`Parameters<Type>` constructs a tuple type from the types used in the parameters of a function type `Type`. For overloaded functions, this will be the parameters of the last signature.

```ts
// Define a function
function greet(name: string, age: number, isActive: boolean): string {
  return `Hello ${name}, you are ${age} years old and ${isActive ? "active" : "inactive"}`;
}

// Get the parameter types from the function
type GreetParams = Parameters<typeof greet>;

// GreetParams is now: [name: string, age: number, isActive: boolean]
// Which becomes a tuple type: [string, number, boolean]

const params: GreetParams = ["Alice", 25, true];
const result = greet(...params); // "Hello Alice, you are 25 years old and active"

// Example with arrow function
const multiply = (a: number, b: number): number => a * b;
type MultiplyParams = Parameters<typeof multiply>;
// MultiplyParams is: [a: number, b: number]
// Which becomes: [number, number]

const multParams: MultiplyParams = [3, 4];
const product = multiply(...multParams); // 12
```

`ConstructorParameters<Type>` constructs a tuple or array type from the types of a constructor function type. It produces a tuple type with all the parameter types (or the type `never` if `Type` is not a function).

```ts
// Define a class
class User {
  name: string;
  age: number;
  isActive: boolean;

  constructor(name: string, age: number, isActive: boolean) {
    this.name = name;
    this.age = age;
    this.isActive = isActive;
  }
}

// Get the constructor parameter types
type UserConstructorParams = ConstructorParameters<typeof User>;

// UserConstructorParams is now: [name: string, age: number, isActive: boolean]
// Which becomes a tuple type: [string, number, boolean]

// You can use it to create instances
const userParams: UserConstructorParams = ["Alice", 30, true];
const user = new User(...userParams); // Creates new User instance

// Example with arrow function (this won't work as expected since it's not a constructor)
const createPerson = (name: string, age: number) => ({ name, age });
type PersonConstructorParams = ConstructorParameters<typeof createPerson>;
// This would be: never (since createPerson is not a constructor function)
```

`ReturnType<Type>` constructs a type consisting of the return type of function `Type`. For overloaded functions, this will be the return type of the last signature.

```ts
function calculateTotal(price: number, tax: number): number {
  return price + price * tax;
}

type CalculateReturnType = ReturnType<typeof calculateTotal>; // number

const total: CalculateReturnType = calculateTotal(100, 0.1); // 110
```

We can refer to official documentation for other [utility types](https://www.typescriptlang.org/docs/handbook/utility-types.html) that are available.

---

---

## DOM

TypeScript is a typed superset of JavaScript, and it ships type definitions for the DOM API. These definitions are readily available in any default TypeScript project. Of the 20,000+ lines of definitions in lib.dom.d.ts, one stands out among the rest: `HTMLElement`. This type is the backbone for DOM manipulation with TypeScript. It serves as the base interface for every other element interface.

`HTMLElement` interface extends the `Element` interface which extends the `Node` interface. This prototypal extension allows for all `HTMLElement`s to utilize a subset of standard methods.

Here are some HTML elements and their types in TypeScript:

| HTML Element       | TypeScript Type        |
| ------------------ | ---------------------- |
| `<div>` / `<span>` | `HTMLDivElement`       |
| `<button>`         | `HTMLButtonElement`    |
| `<a>`              | `HTMLAnchorElement`    |
| `<ul>` / `<ol>`    | `HTMLUListElement`     |
| `<li>`             | `HTMLLIElement`        |
| `<img>`            | `HTMLImageElement`     |
| `<input>`          | `HTMLInputElement`     |
| `<textarea>`       | `HTMLTextAreaElement`  |
| `<select>`         | `HTMLSelectElement`    |
| `<option>`         | `HTMLOptionElement`    |
| `<form>`           | `HTMLFormElement`      |
| `<label>`          | `HTMLLabelElement`     |
| `<canvas>`         | `HTMLCanvasElement`    |
| `<video>`          | `HTMLVideoElement`     |
| `<audio>`          | `HTMLAudioElement`     |
| `<iframe>`         | `HTMLIFrameElement`    |
| `<table>`          | `HTMLTableElement`     |
| `<tr>`             | `HTMLTableRowElement`  |
| `<td>` / `<th>`    | `HTMLTableCellElement` |

Here is a simple example. The assertion of an element is a best practice in manipulation of DOM with TypeScript:

```ts
const elem = document.createElement("p") as HTMLParagraphElement;

elem.textContent = "This is a paragraph.";
console.log(elem);
```

---

---

## The `declare` keyword

The `declare` keyword tells the compiler that a particular identifier exists and can be referenced in the code. It’s essentially a way to inform TypeScript about objects that are defined elsewhere. Once declared, TypeScript treats those values as fully typed and checks your code against them. The most common use of `declare` is defining global variables that exist at runtime but aren't recognized by TypeScript. The compiler doesn’t translate `declare` statements into JavaScript.

When you use `declare`, you're telling TypeScript: "Trust me, this exists somewhere else in the runtime environment."

```ts
// Inform TypeScript about a global variable defined elsewhere
declare const API_KEY: string;

// Now you can use it without TypeScript errors
console.log(API_KEY);
```

The `declare` keyword works with several TypeScript constructs, and the choice between them matters.

```ts
// Use declare const when the global won't be reassigned
declare const ENV: "development" | "production" | "test";

// Use declare let when the value can change at runtime
declare let currentUser: string | null;

// Use declare var for legacy globals with function-level scoping (rare in modern code)
declare var legacyConfig: Record<string, unknown>;
```

You can also use `declare` to add properties to existing global objects:

```ts
// Add a custom property to the Window interface
declare global {
  interface Window {
    myCustomLibrary: {
      initialize(): void;
      processData(data: unknown): void;
    };
  }
}

// Now TypeScript recognizes this property on the window object
window.myCustomLibrary.initialize();
```

When a library doesn't ship with TypeScript definitions, you can write your own using `declare`. Declaration files use the `.d.ts` extension and contain type information without implementations:

```ts
// file: mylib.d.ts
declare module "my-js-library" {
  export function doSomething(value: string): number;
  export function processData(data: object): void;
  export const VERSION: string;
}
```

Then import and use the library as if it had native TypeScript support:

```ts
import { doSomething, VERSION } from "my-js-library";

console.log(doSomething("test")); // TypeScript knows this returns a number
console.log(VERSION); // TypeScript knows this is a string
```

TypeScript automatically picks up `.d.ts` files that fall within your tsconfig.json `include` paths. A common convention is to create a `types/` folder at the project root for your custom third-party module declaration files. For global declarations, a `globals.d.ts` file in your `src/` folder is a clean approach.

---

---

## Decorators (Not Ready)

A decorator is a programming design pattern in which we wrap something to change its behavior. A decorator is a special kind of declaration that can be attached to a class declaration, method, accessor, property, or parameter. Decorators are a way to decorate members of a class, or a class itself, with extra functionality.

To create our own decorator, we have to create a function with the same name as the decorator. Later, when we use a decorator, we tell TypeScript it should call the decorator function with details about how we used the decorator in our code. For example, if we applied the decorator to a class declaration, the function will receive details about the class. This function must be in scope for your decorator to work.

We add a decorator right before the target of the decorator. The below syntax example shows various decorator types added right before their targets:

```ts
@classDecorator
class Person {
  @propertyDecorator
  public name: string;

  @accessorDecorator
  get fullName() {
    // ...
  }

  @methodDecorator
  printName(@parameterDecorator prefix: string) {
    // ...
  }
}
```

---

### Class Decorators

A Class Decorator is declared just before a class declaration. The class decorator is applied to the constructor of the class and can be used to observe, modify, or replace a class definition.

The parameter(s) passed to the decorator will depend on where the decorator will be used. In the new standard, a class decorator receives two arguments: the value (the class itself) and a context object.

```ts
function decoratorFunc(value: Function, context: ClassDecoratorContext) {
  // console.log(`value: ${value}`);
  console.log(`context: ${context.name}`);
  console.log(`context: ${context.kind}`);
  console.log("calling from the decoratorFunc");
}

@decoratorFunc
class MyClass {
  constructor(public param1: string) {
    console.log(param1);
  }
}

const obj = new MyClass("obj");
```

To replace the constructor, you return a new function/class (in JavaScript/TypeScript, a class is essentially a special kind of function (the constructor function)). If you returned a value in a class decorator, this value will become the new constructor function for the class. This is useful if you want to completely overwrite the class constructor.

Here is an example of replacing a constructor fully. This is for example and not necessarily recommended:

```ts
function decoratorFunc(
  value: Function,
  context: ClassDecoratorContext,
): { new (...args: any[]): {} } {
  console.log(`Replacing the constructor of ${context.name}`);

  return class {
    constructor() {
      console.log("Message from the new constructor");
    }
  };
}

@decoratorFunc
class MyClass {
  constructor() {
    console.log("This doesn't run. It gets replaced");
  }
}

const obj = new MyClass();
```

Here is an example of extending a class constructor:

```ts
function decoratorFunc<T extends { new (...args: any[]): {} }>(
  value: T,
  context: ClassDecoratorContext,
) {
  return class extends value {
    constructor(...args: any[]) {
      super(...args);
      console.log(`Extended the class ${context.name}`);
    }
  };
}

@decoratorFunc
class MyClass {
  constructor(public param1: string) {
    console.log(`calling from the original constructor with param1: ${param1}`);
  }
}

const obj = new MyClass("Hello");
```

The `context` object that a class decorator receives has an `addInitializer` method that could be useful. It allows us to "inject" a function that will run immediately after the object is constructed, but before it is returned to the user.

```ts
function decoratorFunc(value: Function, context: ClassDecoratorContext) {
  context.addInitializer(function (this: any) {
    console.log(`New instance of ${context.name} has been created`);

    this.initializedAt = new Date();
  });
}

@decoratorFunc
class MyClass {
  constructor(public param1: string) {
    console.log(`Constructor for ${this.param1} has run`);
  }
}

const obj = new MyClass("Hello");
```

### Decorator Composition

Multiple decorators can be applied to a declaration, for example on a single line or on multiple lines:

```ts
function decoratorA(value: Function, context: ClassDecoratorContext) {
  console.log("decorator A");
}

function decoratorB(value: Function, context: ClassDecoratorContext) {
  console.log("decorator B");
}

function decoratorC(value: Function, context: ClassDecoratorContext) {
  console.log("decorator C");
}

@decoratorA
@decoratorB
@decoratorC
class MyClass {
  constructor() {
    console.log("MyClass instance created!");
  }
}

const obj = new MyClass();
// Output:
// decorator C
// decorator B
// decorator A
// "MyClass instance created"
```

---

### Decorator Factories

Sometimes you will need to pass additional options to the decorator when applying it, and for that, you have to use decorator factories. Decorator factories are functions that return another function. They receive this name because they are not the decorator implementation itself. Instead, they return another function responsible for the implementation of the decorator and act as a wrapper function. They are useful in making decorators customizable, by allowing the client code to pass options to the decorators when using them.

```ts
const decoratorA = (someBoolean: boolean) => {
  return (value: Function, context: ClassDecoratorContext) => {
    if (someBoolean) {
      console.log(`someBoolean: ${someBoolean}`);
    }
  };
};

@decoratorA(true)
class MyClass {
  constructor() {
    console.log("MyClass instance created");
  }
}

const obj = new MyClass();
```

Note that you are required to pass all the parameters expected by the decorator factory.

---

### Property Decorators

A Property Decorator is declared just before a property declaration.

```ts
function decoratorFunc(value: undefined, context: ClassFieldDecoratorContext) {
  console.log(`Decorating property: ${String(context.name)}`);
}

class User {
  @decoratorFunc
  public username: string = "John";

  @decoratorFunc
  public email: string = "john@example.com";
}

const user = new User();
```

---

### Accessor Decorators

An Accessor Decorator is declared just before an accessor declaration. It can be used to observe, modify, or replace an accessor’s definitions.

---

### Method Decorators

A Method Decorator is declared just before a method declaration.

### Parameter Decorators

A Parameter Decorator is declared just before a parameter declaration.

---

---
