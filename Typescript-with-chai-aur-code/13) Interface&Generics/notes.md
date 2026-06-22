# Lecture 13 - Interfaces & Generics in TypeScript

## Topics Covered

### Interfaces
- What is an Interface?
- Object Shape Definition
- Optional Properties
- Readonly Properties
- Function Interfaces
- Method Signatures
- Index Signatures
- Interface Merging
- Interface Extension

### Generics
- Generic Functions
- Multiple Generic Types
- Generic Interfaces
- Generic API Responses
- Real-world Use Cases

---

# Interfaces

An Interface defines the structure (shape) of an object.

It specifies:

- What properties exist
- Their types
- Optional properties
- Methods

Interfaces do **not generate JavaScript code**.

---

## Basic Interface

```ts
interface Tea {
  flavor: string;
  price: number;
}
```

---

## Usage

```ts
const masalaTea: Tea = {
  flavor: "Masala",
  price: 30,
};
```

---

## Invalid

```ts
const tea: Tea = {
  flavor: "Masala",
};
```

❌ Error

```text
Property 'price' is missing
```

---

# Interface vs Type

### Interface

```ts
interface Tea {
  flavor: string;
}
```

---

### Type Alias

```ts
type Tea = {
  flavor: string;
};
```

---

## Interview Point

Both can define object shapes.

However:

- Interfaces are preferred for object contracts.
- Types are preferred for unions, intersections, utility types.

---

# Optional Properties

Use `?`

```ts
interface Tea {
  flavor: string;
  milk?: boolean;
}
```

---

## Valid

```ts
const tea: Tea = {
  flavor: "Masala",
};
```

---

## Also Valid

```ts
const tea: Tea = {
  flavor: "Masala",
  milk: true,
};
```

---

# Readonly Properties

Cannot be modified after assignment.

## Example

```ts
interface TeaShop {
  readonly id: number;
  name: string;
}
```

---

## Usage

```ts
const shop: TeaShop = {
  id: 1,
  name: "ChaiCode Cafe",
};
```

---

## Invalid

```ts
shop.id = 2;
```

❌ Error

---

# Function Interfaces

Interfaces can describe function structures.

---

## Example

```ts
interface DiscountCalculator {
  (
    price: number
  ): number;
}
```

---

## Implementation

```ts
const applyDiscount:
  DiscountCalculator =
  (price) => {
    return price * 0.5;
  };
```

---

# Why Use Function Interfaces?

Provides a strict contract:

```ts
Input → number
Output → number
```

---

# Method Signatures

Interfaces can define methods.

---

## Example

```ts
interface TeaMachine {
  start(): void;
  stop(): void;
}
```

---

# Implementation

```ts
const machine: TeaMachine = {
  start() {
    console.log("Started");
  },

  stop() {
    console.log("Stopped");
  },
};
```

---

# Real World Example

Camera APIs:

```ts
interface Camera {
  open(): void;
  capture(): File;
  close(): void;
}
```

Any implementation must provide all methods.

---

# Index Signatures

Used when object keys are dynamic.

---

## Example

```ts
interface TeaRatings {
  [flavor: string]: number;
}
```

---

## Usage

```ts
const ratings: TeaRatings = {
  Masala: 4.5,
  Ginger: 4.7,
  Lemon: 4.2,
};
```

---

# Invalid

```ts
const ratings: TeaRatings = {
  Masala: "Excellent",
};
```

❌ Error

Expected:

```ts
number
```

---

# Why Index Signatures?

Useful when:

- Keys are unknown
- Dynamic objects
- Dictionaries
- API maps

---

# Interface Merging

One of the biggest differences from Type Aliases.

---

## First Declaration

```ts
interface User {
  name: string;
}
```

---

## Second Declaration

```ts
interface User {
  age: number;
}
```

---

## Final Result

TypeScript merges them.

```ts
interface User {
  name: string;
  age: number;
}
```

---

## Usage

```ts
const user: User = {
  name: "Rajat",
  age: 21,
};
```

---

# Why Interface Merging Matters?

Libraries often extend existing interfaces.

This feature is heavily used in:

- Express.js
- Next.js
- React ecosystem
- Authentication libraries

---

# Interface Extension

Interfaces can extend other interfaces.

---

## Example

```ts
interface A {
  a: string;
}
```

---

```ts
interface B {
  b: string;
}
```

---

```ts
interface C
  extends A, B {}
```

---

## Result

```ts
interface C {
  a: string;
  b: string;
}
```

---

# Generics

Generics allow reusable type-safe code.

---

## Problem Without Generics

```ts
function wrapString(
  item: string
): string[] {
  return [item];
}
```

Only works for strings.

---

# Generic Function

```ts
function wrapInArray<T>(
  item: T
): T[] {
  return [item];
}
```

---

## Usage

### String

```ts
wrapInArray(
  "Masala"
);
```

Returns:

```ts
string[]
```

---

### Number

```ts
wrapInArray(
  42
);
```

Returns:

```ts
number[]
```

---

### Object

```ts
wrapInArray({
  flavor: "Ginger",
});
```

Returns:

```ts
{
  flavor: string;
}[]
```

---

# Understanding T

```ts
<T>
```

is just a placeholder.

It could be:

```ts
<T>
<U>
<K>
<V>
```

Any valid name works.

---

# Multiple Generic Types

## Example

```ts
function pair<
  A,
  B
>(
  a: A,
  b: B
): [A, B] {

  return [a, b];
}
```

---

## Usage

```ts
pair(
  "Masala",
  42
);
```

Result:

```ts
[string, number]
```

---

# Generic Interfaces

Interfaces can also use generics.

---

## Example

```ts
interface Box<T> {
  content: T;
}
```

---

# Number Box

```ts
const numberBox:
  Box<number> = {

  content: 10,
};
```

---

# String Box

```ts
const stringBox:
  Box<string> = {

  content: "Tea",
};
```

---

## Invalid

```ts
const box:
  Box<number> = {

  content: "Tea",
};
```

❌ Error

Expected:

```ts
number
```

---

# Generic API Response

Very common in React applications.

---

## Interface

```ts
interface ApiResponse<T> {
  status: number;
  data: T;
}
```

---

# Usage

```ts
interface TeaData {
  flavor: string;
}
```

---

```ts
const response:
  ApiResponse<TeaData> = {

  status: 200,

  data: {
    flavor: "Masala",
  },
};
```

---

# Why Generics Are Powerful

Without Generics:

```ts
ApiResponseString
ApiResponseNumber
ApiResponseUser
ApiResponseProduct
```

Many interfaces.

---

With Generics:

```ts
ApiResponse<T>
```

One reusable interface.

---

# Real-World Generic Usage

You will see Generics everywhere in:

- React Hooks
- React Query
- Axios
- Prisma
- Drizzle ORM
- Redux Toolkit
- Zustand
- TanStack Query

---

## Example

```ts
useState<string>()
```

---

```ts
useRef<HTMLInputElement>()
```

---

```ts
AxiosResponse<User>()
```

---

# Interview Questions

## What is an Interface?

A blueprint that defines the structure of an object.

---

## Difference Between Interface and Type?

### Interface

Best for:

```ts
Objects
Classes
Contracts
```

---

### Type

Best for:

```ts
Union Types
Intersection Types
Utility Types
```

---

## What is Interface Merging?

Multiple interface declarations with the same name automatically combine.

---

## Can Interfaces Extend Other Interfaces?

Yes.

```ts
interface C
  extends A, B {}
```

---

## What is a Generic?

A reusable type placeholder.

---

## Why Use Generics?

To create reusable and type-safe code.

---

## What Does `<T>` Mean?

A generic type parameter.

---

## Can Generics Be Used With Interfaces?

Yes.

```ts
interface Box<T> {}
```

---

## Real-World Generic Example?

```ts
ApiResponse<T>
```

```ts
useState<T>()
```

```ts
AxiosResponse<T>()
```

---

# Quick Revision

### Interface

```ts
interface User {}
```

---

### Optional Property

```ts
name?: string
```

---

### Readonly Property

```ts
readonly id
```

---

### Function Interface

```ts
(price: number) => number
```

---

### Method Signature

```ts
start(): void
```

---

### Index Signature

```ts
[key: string]: number
```

---

### Interface Merging

```ts
interface User {}
interface User {}
```

---

### Interface Extension

```ts
extends
```

---

### Generic Function

```ts
function fn<T>()
```

---

### Generic Interface

```ts
interface Box<T>
```

---

### Generic API Response

```ts
ApiResponse<T>
```

---

## 🔥 Interview Focus (Very Important)

### Interfaces

1. Interface vs Type
2. Optional Properties
3. Readonly Properties
4. Function Interfaces
5. Index Signatures
6. Interface Extension
7. Interface Merging ⭐

### Generics

8. Generic Functions
9. Multiple Generic Parameters
10. Generic Interfaces
11. Generic API Responses
12. React Generic Examples (`useState<T>`)
13. Why Generics Improve Reusability

---

## ⭐ Must Remember

If an interviewer asks:

> "What is the biggest advantage of Interface over Type?"

Answer:

```text
Interface Merging
```

If asked:

> "Where do you use Generics in React?"

Answer:

```ts
useState<T>()
useRef<T>()
AxiosResponse<T>()
```

These are among the most commonly asked TypeScript interview questions. :contentReference[oaicite:0]{index=0}