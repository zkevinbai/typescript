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