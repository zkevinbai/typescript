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

