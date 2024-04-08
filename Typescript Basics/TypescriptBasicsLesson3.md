# Typescript Basics Lesson 3
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


