---
date: 2023-12-26
tags:
  - typescript
---
[link](https://stackoverflow.com/questions/55377365/what-does-keyof-typeof-mean-in-typescript)

To understand the `keyof typeof` usage in TypeScript, first you need to understand what are **literal types** and **union of literal types**. So, I'll explain these concepts first and then explain `keyof` and `typeof` individually in detail. After that, I'll come back to `enum` to answer what is asked in the question. It's a long answer but examples are easy to understand.

---

## Literal types

Literal types in TypeScript are more specific types of `string`, `number` or `boolean`. For example, `"Hello World"` is a `string`, but a `string` is not `"Hello World"`. `"Hello World"` is a more specific type of type `string`, so it is a literal type.

A literal type can be declared as following:

```javascript
type Greeting = "Hello"
```

This means that the object of type `Greeting` can have only a `string` value `"Hello"` and no other `string` value or any other value of any other type as shown in the following code:

```javascript
let greeting: Greeting
greeting = "Hello" // OK
greeting = "Hi"    // Error: Type '"Hi"' is not assignable to type '"Hello"'
```

Literal types are not useful on their own, however when combined with union types, type aliases and type guards they become powerful.

Following is an example of **union of literal types**:

```javascript
type Greeting = "Hello" | "Hi" | "Welcome"
```

Now the object of type `Greeting` can have the value either `"Hello"`, `"Hi"` or `"Welcome"`.

```javascript
let greeting: Greeting
greeting = "Hello"       // OK
greeting = "Hi"          // OK
greeting = "Welcome"     // OK
greeting = "GoodEvening" // Error: Type '"GoodEvening"' is not assignable to type 'Greeting'
```

---

## `keyof` only

`keyof` of some type `T` gives you a new type that is a **union of literal types** and these literal types are the names of the properties of `T`. The resulting type is a subtype of string.

For example, consider the following `interface`:

```typescript
interface Person {
    name: string
    age: number
    location: string
}
```

Using the `keyof` operator on the type `Person` will give you a new type as shown in the following code:

```typescript
type SomeNewType = keyof Person
```

This `SomeNewType` is a union of literal types (`"name" | "age" | "location"`) that is made from the properties of type `Person`.

Now you can create objects of type `SomeNewType`:

```javascript
let newTypeObject: SomeNewType
newTypeObject = "name"           // OK
newTypeObject = "age"            // OK
newTypeObject = "location"       // OK
newTypeObject = "anyOtherValue"  // Error...
```

---

## `keyof typeof` together on an object

As you might already know, the `typeof` operator gives you the type of an object. In the above example of `Person` interface, we already knew the type, so we just had to use the `keyof` operator on type `Person`.

But what to do when we don't know the type of an object or we just have a value and not a type of that value like the following?

```javascript
const bmw = { name: "BMW", power: "1000hp" }
```

This is where we use `keyof typeof` together.

The `typeof bmw` gives you the type: `{ name: string, power: string }`

And then `keyof` operator gives you the literal type union as shown in the following code:

```javascript
type CarLiteralType = keyof typeof bmw

let carPropertyLiteral: CarLiteralType
carPropertyLiteral = "name"       // OK
carPropertyLiteral = "power"      // OK
carPropertyLiteral = "anyOther"   // Error...
```

---

## `keyof typeof` on an `enum`

In TypeScript, enums are used as _types at compile-time_ to achieve type-safety for the constants but they are treated as _objects at runtime_. This is because, they are converted to plain objects once the TypeScript code is compiled to JavaScript. So, the explanation of the objects above is applicable here too. The example given by OP in the question is:

```javascript
enum ColorsEnum {
    white = '#ffffff',
    black = '#000000',
}
```

Here `ColorsEnum` exists as an object at runtime, not as a type. So, we need to invoke `keyof typeof` operators together as shown in the following code:

```javascript
type Colors = keyof typeof ColorsEnum

let colorLiteral: Colors
colorLiteral = "white"  // OK
colorLiteral = "black"  // OK
colorLiteral = "red"    // Error...
```


