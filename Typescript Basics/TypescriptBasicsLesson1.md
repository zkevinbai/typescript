# Typescript Basics Lesson 1
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

