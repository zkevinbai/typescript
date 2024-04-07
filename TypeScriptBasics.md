# Typescript Basics
#learn/typescript

6 April 2024 Saturday
[Execute Program](https://www.executeprogram.com/courses/typescript-basics)

# Typescript Lesson 1
#learn/typescript

26 March 2024 Tuesday

## Typescript Basics

* You don't need any previous experience with statically typed languages to take this course. However, we do assume that you know some basic JavaScript concepts. (You can also look them up as you go; there aren't many!) Here's a list of concepts that we use but don't explain:

  * null and undefined.
  * Variable definitions with var, let, and const.
  * Conditionals (if) and ternary conditionals (a ? y : b).
  * Regular functions: function f() { ... }.
  * Arrow functions: const f = () => { ... }.
  * Loops, using for or map.
  * Some common array methods like push and pop.

* Unlike JavaScript, variables in TypeScript have static types. Types come after a `:`
```ts
let sum: number = 1 + 1;sum;RESULT:2

let anything: string = 'any' + 'thing';
anything;

RESULT:
'anything'
```
* the above compiled because the types matched

```ts
let sum: number = 'any' + 'thing';sum;RESULT:type error: Type 'string' is not assignable to type 'number'.
```
* the above fails to compile because string cannot be assigned to the number type

Typescript Rules
1. Types always have to match.
2. Every variable has a type.
3. Every value we assign must match the variable's type.

## Operators

Operators like + and * can only be used on types that make sense. For example, we can add numbers with + and multiply with *. We can also use + to concatenate strings. However, we can't use * on strings. That's a type error.


```
'2' * '2';RESULT:type error: The left-hand side of an arithmetic operation must be of type 'any', 'number', 'bigint' or an enum type.
```
* this complies fine with Javascript’s dynamic compilation, but it doesn’t work with typescript

## Functions

A function takes arguments, which have types. Then the function returns something, which also has a type. The types are marked with colons `:`, as they were for simple variables.

```tsfunction double(x: number): number {  return 2 * x;}double(2);RESULT:4
```
* functions interface works like this
* parentheses after the function name, in this case double, contain the input variable
  * semicolon tells you the input variable’s type
* colon after the input tells you what the function should output

I worked with typescript at Palantir for 2 years and never understood it until today

```js
# javascript
const add1 = (n) => n + 1
```

```ts
# typescript
const add1 = (n: number): number => n + 1;
```

What you lose in simplicity you gain in features, the ts version tells you what the function will accept, and what it will return.  Even if this function was terribly named or renamed, the interface will always be clear.

```ts
function addOrSubtract (num : number, shouldAdd: boolean) : number {
  if (shouldAdd === true) {
    return num + 1
  } else {
    return num - 1
  }
}
```

# Typescript Lesson 2
#learn/typescript

31 March 2024 Sunday

Array
* Array types are marked with []. An array of numbers is number[].
* multitype arrays exist, but they aren’t prevalent

```
let numbers: number[] = [1, 2, 3];numbers[1];RESULT:2
```

Return Type Inference
* TS can infer types

```function two() {  return 1 + 1;}two();RESULT:2
```


## Syntax Errors vs Type Errors

* In JavaScript, any code with valid syntax will run. In TypeScript, code must have valid syntax and must type check. Only then will it run.
  * JavaScript: syntax check -> execution.
  * TypeScript: syntax check -> type check -> execution.
* Syntax error means you are using the language wrong
  * if you have the wrong syntax, the type checker will never run

# Typescript Lesson 3
#learn/typescript

1 April 2024 Monday

## Typescript Syntax is Consistent

a variable can be an array of strings, we can also make arrays of any type.
* array syntax is `something[]`

```
const arrayOfStrings: string[] = ['hello', 'world'];
arrayOfStrings;RESULT:['hello', 'world']
```

```
const arrayOfArraysOfStrings: (string[])[] = [['hello'], ['world']];
arrayOfArraysOfStrings;RESULT:[['hello'], ['world']]
```

`(string[])[]` is the same thing as `string[][]`

Every type works everywhere
* as a variable
* as a function argument or return type
* inside an array
* as an object property

## Tuples

Typescript supports arrays of fixed length
* `[number, number]` is a tuple of length 2 with 2 numbers exactly
  * not one, not three, not zero

Every element of an array must be the same type, tuples can have mixed types such as `[number, string]`

## Generic Arrays
`Array<number>` is the same as `number[]`

`Array<>` is referred to as a generic
* it can be filled with anything, but it must be filled by a type

`Array<Arrray<number>>` is the same as `number[][]`

## Generic Functions

```
function first<T>(elements: Array<T>): T {  return elements[0];}first<boolean>([true, false]);RESULT:true
```
* this generic function takes both a type and elements as inputs
* the type is the type of the elements and also the return type

Compiling steps
1. first gets filled with the boolean type
2. the input elements receive the boolean type
3. the input is validated as a boolean array
4. the return receives the boolean type

Generics work with any class
* Javascript is a dynamic language and allows us to do the same thing
* Typescript generics allow us to be dynamic while guaranteeing that all types match

```function last<T>(elements: Array<T>): T {  return elements[elements.length - 1];}
let results: [string, number] = [  last<string>(['a', 'b', 'c']),  last<number>([1, 2, 3]),];
results;RESULT:['c', 3]
```

Generics also work  when the results are assigned to an inferred variable

```function first<T>(elements: Array<T>): T {  return elements[0];}let n = first<number>([1, 2]);let n2 = n;n2;RESULT:1
```
* in the above example, n and n2 can only become number types so typescript allows us to write them without declaring their types

Type parameters should be UpperCamelCased so they can be easily identified, `Element` is a preferred keyword

```
function identity<Element>(Input: Element): Element {
  return Input
}
```

## Generic Function Inference

Generics are capable of inferring types 
* Typescript has automatic type inference

```
function length<T>(elements: T[]): number {  return elements.length;}
>[  length([1, 2]),  length(['a']),];RESULT:[2, 1]
```

# Typescript Lesson 4
#learn/typescript

3 April 2024 Wednesday

## Type Keyword

We can declare names for types using the `type` keyword, much like declaring a variable using `let`, user defined types are UpperCamelCased by convention

```
>
type MyStringType = string;
let s: MyStringType = 'hello';
s;

RESULT:
'hello'
```
* in this example, we assigned the string type to MyStringType

Each TS program is a valid JS program, after the typescript compiler runs, everything is javascript

The declaration type MyNumberType = number only contains TypeScript syntax. There's no JavaScript there! After the TypeScript compiler runs, we're left with an empty JavaScript program. Our system then runs that empty JavaScript, which gives us undefined.

```type MyNumberType = number;RESULT:undefined
```

The fact that the TypeScript compiler throws the types away is important. Most notably, it means that there's no way to inspect types at runtime. Types are only used during type checking, then they're thrown away.  This is called “type erasure”, types are only used for type checking and then erased from the compiled output.

## Object Types
In JavaScript, `myObject.someProperty` will return undefined if `someProperty` doesn't exist. This has caused an errors in production applications. The most common symptom is the "undefined is not a function" error when we do `myObject.someProperty()`.

TypeScript's object types let us catch this type of error at compile time. No more finding these bugs because they fail in production!

An object type specifies each property's name and type.
* object types require that all properties are present, and that all properties match the property types in the type definition
```
type User = {
  email: string
  admin: boolean
};

let amir: User = {
  email: 'amir@example.com',
  admin: true,
};
amir.admin;
RESULT:
true
```

```
let cindy: User = {email: 'cindy@example.com'};
cindy.email;

RESULT:
type error: Property 'admin' is missing in type '{ email: string; }' but required in type 'User'.
```

Object type syntax is similar to literal object syntax, but expressions are not allowed in types
* `1 + 1` is not allowed 

```
type User = {email: string, admin: true || false};RESULT:syntax error: on line 1: ';' expected.
```

Apart from expressions, object types can be very complex, they can even be other objects
```
type Reservation = {
  user: {
    email: string
    admin: boolean
  }
  roomNumber: number
};
```


## Generic Object Types

The same way we can have an generic Array type with an empty pocket `Array<T>`, its possible to have the same empty pocket with types

```
type Pants<T> = {
  left: T
  right: T
};
```

generic objects can have more than one type parameter

```
type Pants<T1, T2> = {
  left: T1
  right: T2
};
```


# Typescript Lesson 5
#learn/typescript

4 April 2024 Thursday

# Literal Object Types

Sometimes we don’t need to reuse a object type, and we can put the type directly in a function’s signature

```ts
> function extractEmail(user: {email: string}): string {
	return user.email;
}

extractEmail({email: 'amir@example.com'})

RESULT:
'amir@example.com'
```

We can use Javascript destructuring along with Typescript type syntax

Here's an example of a function that takes an object with a name property and returns its name, without destructuring.

```ts
function userName(user: {name: string}): string {  return user.name;}userName({name: 'Amir'});RESULT:'Amir'
```

Now, let's shorten this by using JavaScript destructuring, which "grabs" name out of the argument. Destructuring and object arguments sometimes look strange together, but remember that the type is to the right of the : symbol.
```ts
function userName({name}: {name: string}): string {  return name;}userName({name: 'Amir'});RESULT:'Amir'
```
* This function expects an object with a property of `name` as input, and that name should be of the string type

## Object Narrowing

We can assign object types to smaller object types

```ts
type User = {  email: string  admin: boolean};let amir: User = {  email: 'amir@example.com',  admin: true,};
type HasEmail = {
  email: string
};
let amirEmail: HasEmail = amir;
```
* the smaller object loses knowledge of where it came from
* amirEmail has no clue about the admin property

An object’s structure determines its type
* you don’t need to specify that `HasEmail` is a child of `User`
* they both share an email property, so Typescript automatically knows they are related

Narrowing can be very useful. For example, our system might have a sendEmail method. If it takes a User, then we'll need a full user to call it.

However, a sendEmail that takes a {email: string} is more flexible. We can pass it a user, or we can pass it just an {email: string} to send an email to an address not associated with a user.

```ts
type User = {email: string, admin: boolean};

let amir: User = {email: 'amir@example.com', admin: true};

function sendEmail({email}: {email: string}): string {
  return `Emailing ${email}`;
}

[
  sendEmail(amir),
  sendEmail({email: 'betty@example.com'}),
];
RESULT:
['Emailing amir@example.com', 'Emailing betty@example.com']  
```

Typescript is structurally typed, not nominally typed
* structural typing is also known as duck typing, if it looks like a duck, swims like a duck, and quacks like a duck, it probably is a duck
* structural typing means we only care about the properties we are assessing, we don’t care if the the type’s name is user or HasEmail, and we don’t care if the object has extra properties

## Function Types

`(n: number) => number`
* a function that takes a number and returns a number

```ts
function add1(n: number): number {  return n + 1;}
const myAdd1: (n: number) => number = add1;myAdd1(3);RESULT:4

type addingOne = (num: number) => number
const myOtherAddOne: addingOne = add1
myOtherAddOne(4)

RESULT:5
```

* you can type functions with or without a type variable 
* position is the only thing that matters when typing variables, you can have different names for the variable in your function and in your function type

In a function definition, we give the arguments names. However, these names aren't part of the type. Only their position matters. We might name an argument s in a function type, but text when defining the function. That's fine and the code will still type check.

```ts
function downcase(text: string): string {  return text.toLowerCase();}type DowncaseFunction = (s: string) => string;const myDowncase: DowncaseFunction = downcase;myDowncase('HELLO');RESULT:'hello’
```

Note that types can only be defined with arrow syntax


```ts

```

# Typescript Lesson 6
#learn/typescript

5 April 2024 Friday

## Type Unions

An "or" type, `Type1 | Type2`, is called a union type.
* this means either type is valid

```ts
function isNumber(arg: string | number): boolean {  return typeof arg === 'number';}
```

Type mixing is not allowed
```ts
function getClevelandZipCode(): string | number {  return 44106;}let zip: number = getClevelandZipCode();zip;RESULT:type error: Type 'string | number' is not assignable to type 'number'.
Type 'string' is not assignable to type 'number'.
```
* in this example, the code errors out because getClevelandZipCode could return a string and a string cannot become a number type

you can union as many types as you want, ex `string | boolean | number`

## Generic Function Types

```ts
function firstElement<T>(elements: Array<T>): T {  return elements[0];}type First<T> = (elements: Array<T>) => T;
const firstString: First<string> = first;

>
firstString(['a', 'b']);
RESULT:
'a'

>
firstString([1, 2]);
RESULT:
type error: Type 'number' is not assignable to type 'string'.
```
* `First` is a type that takes an array of types and returns a type
* `firstElement` is a function that takes an array of types and returns a type
* `firstString` is a type that takes the `firstElement` function and narrows its scope to only take strings

## Literal Types

Every concrete number and string is also a type
* `1` can be a type, that type would not be able to hold `2` 

```ts 
let one: 1 = 2;one;RESULT:type error: Type '2' is not assignable to type '1'.
```

This becomes useful in real life in a scenario like a sort function

```ts
const sort2(nunbers: number[], direction: 'asc' | 'desc'): number[] {
  const sortable = numbers.slice()

	sortable.sort()

	if (direction === 'desc') {
		sortable.sort().reverse()
	}

	return sortable
}
```

When we have more than 2 values, literal types become really valuable

```ts 
type DatabaseType = 'mysql' | 'postgres' | 'oracle';
let dbType: DatabaseType = 'mysql';
dbType;
```
* With this type constraint in place, a user is immediately told if they try to use our library with an unsupported database. It will also tell them if they have a typo in the database name. They don't even have to run the application to see a failure. It can't run at all because it contains type errors.

`type: boolean` is essentially just `type: true | false`

## Conditional Narrowing

```ts
type User = {  name: string};	function nameOrLength(userOrUsers: User | User[]) {  if (Array.isArray(userOrUsers)) {    // Inside this side of the if, userOrUsers' type is User[].    return userOrUsers.length;  } else {    // Inside this side of the if, userOrUsers' type is User.    return userOrUsers.name;  }}
```

The answer is that TypeScript can see our if (Array.isArray(userOrUsers)) check. If Array.isArray is true, then the type can only be User[], not User. The TypeScript compiler knows what Array.isArray means when used in a conditional.

# Typescript Lesson 7
#learn/typescript

6 April 2024 Saturday

## Undefined in Arrays

accessing indices that don’t exist will cause TS to return undefined

```ts
const numbers = [1, 2, 3];const n = numbers[100];const isUndefined = n === undefined ? 'yes' : 'no';isUndefined;RESULT:'yes'
```

## Nullability

in javascript any variable can be null or undefined
* in typescript `undefined` has its own special type, nothing else can be undefined, not even null

because undefined has its own special type, we must use its type or a type union to actually use it

```ts
let numberMaybe: number | undefined = undefined;
numberMaybe;
```

TypeScript's `--strictNullChecks` option allows the compiler to flag variables that are not explicitly declared as nullable


