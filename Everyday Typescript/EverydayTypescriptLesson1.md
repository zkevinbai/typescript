# Everyday Typescript Lesson 1
#learn/typescript/everyday

[Execute Program](https://www.executeprogram.com/courses/everyday-typescript)

7 April 2024 Sunday, 8 April 2024 Monday

## Type Intersections

* We can define types that must match with two other types
* `T1 & T2`  means must match with all properties from `T1` and from `T2`
* We can always narrow an intersection back to one of its parts

```ts
type HasEmail = {
  email: string
};
type CanBeAdmin = {
  admin: boolean
};
type User = HasEmail & CanBeAdmin;

let amir: User = {
  email: 'amir@example.com',
  admin: true,
};

function extractEmail({email}: HasEmail): string {
  return email;
}
extractEmail(amir);
RESULT:
'amir@example.com'

function extractAdmin(hasEmail: HasEmail): boolean {
  return hasEmail.admin;
}
extractAdmin(amir);
RESULT:
type error: Property 'admin' does not exist on type 'HasEmail'.
```
* the third example fails because we are only narrowing out the hasEmail property, which means TS does not recognize the `amir` object as having an admin property

## Impossible Conditions

Typescript can only use the keyword `if` to type narrow if the if condition is possible in the first place

```ts
let s;
if (1 === 0) {
  s = 'it worked';
}
s;
RESULT:
type error: This comparison appears to be unintentional because the types '1' and '0' have no overlap.


```
* The TS compiler is not reading into values, only types
* the 1 type can never hold any other type

```ts
type User = {
  username: string
};
const amir: User = {username: 'amir'};

type Album = {
  albumName: string
};
const kindOfBlue: Album = {albumName: 'Kind of Blue'};

let s;
if (amir === kindOfBlue) {
  s = 'it worked';
}
s;
RESULT:
type error: This comparison appears to be unintentional because the types 'User' and 'Album' have no overlap.
```
* impossible narrowing occurs for literal types and complex types

```ts
const zero: number = 0;const one: number = 1;	let s;if (zero === one) {  s = 'they are equal';} else {  s = 'they are not equal';}s;RESULT:'they are not equal'let s;if ('' + 'a' === 'b') {  s = 'they are equal';} else {  s = 'they are not equal';}s;RESULT:'they are not equal'
```
* seemingly impossible comparisons are fine so long as they are the same type and could in theory have the same value
* the variable zero can be reassigned to 1, so zero could equal one

## Pick and Omit

`Pick` type allows us to pick one or more properties from another object, creating a new object type with only those properties

```ts
type User = {
  name: string
  email: string
  age: number
};

type NameOnly = Pick<User, 'name'>;

const amir: NameOnly = {name: 'Amir'};
amir;
RESULT:
{name: 'Amir'}
```
 


```ts
type User = {
  name: string
  email: string
  age: number
};

type NameAndEmail = Pick<User, 'name' | 'email'>;

const amir: NameAndEmail = {name: 'Amir'};
amir;
RESULT:
type error: Property 'email' is missing in type '{ name: string; }' but required in type 'NameAndEmail'.
```
* need to pass in a union type to pick multiple properties, this is because in TS generic types must take a fixed number of type parameters

The usage of pick allows us to avoid redefining sub types, an example would be if we were building a JSON web application API, and we already had large complex types for the concepts like user, thread, and comment.

Individual API will only need to include small pieces of those objects, pick allows us to only use a certain amount of the interface.

`Omit` is the opposite of pick, omit creates a new type with all properties of the parent except the ones we specify.

```ts
type User = {
  name: string
  email: string
  age: number
};

// These two types are equivalent!
type NameOnly1 = Pick<User, 'name'>;
type NameOnly2 = Omit<User, 'email' | 'age'>;

const amir1: {name: string} = {name: 'Amir'};
const amir2: NameOnly1 = amir1;
const amir3: NameOnly2 = amir1;
amir3;
RESULT:
{name: 'Amir'}
```
 
## Functions as Arguments

JS functions can be assigned to variables, stored in arrays and objects, and passed as function arguments.  JS has first-class functions because functions in JS have no restrictions

```ts
type TakesNumberReturnsNumber = (x: number) => number;
const add1: (x: number) => number = x => x + 1;
const aFunction: TakesNumberReturnsNumber = add1;

aFunction(1);
RESULT:
2

type TakesNumberReturnsNumber = (x: number) => number;
const add1: (x: number) => number = x => x + 1;
const arrayOfFunctions: TakesNumberReturnsNumber[] = [add1];
const aFunction: TakesNumberReturnsNumber = arrayOfFunctions[0];

aFunction(2);
RESULT:
3
```

We can pass functions to another function

```ts
function callFunction(f: (x: number) => number) {
  return f(10);
}
callFunction(
  x => x + 1
);
```

* Everything in TypeScript has to have a type, so what's the return type of our callFunction function? The compiler reasons about it like this:
  * callFunction returns f(x), so callFunction's return type must match f's return type.
  * f's return type is number, as shown in its overall type (x: number) => number.
  * So callFunction's return type is also number.

the compiler and computer don't care about how confusing something is. They only care about whether it follows the rules
* ` () => (f: () => number) => () => (f: () => number) => number`
* it's important to make the code readable, not just valid!

hello darkness my old friend