# Typescript Lesson 5
#learn/typescript

4 April 2024 Wednesday

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

