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

