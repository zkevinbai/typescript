# Typescript Basics Lesson 2
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




