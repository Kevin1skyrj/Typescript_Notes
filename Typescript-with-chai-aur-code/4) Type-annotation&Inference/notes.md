# Lecture 4 - Type Annotation & Type Inference

## Type Inference

TypeScript can automatically determine the type of a variable based on its value.

### Example

```ts
let drink = "Tea";
```

TypeScript automatically infers:

```ts
let drink: string;
```

Hovering over the variable in VS Code will show:

```ts
let drink: string
```

### Example

```ts
let cups = 10;
```

TypeScript infers:

```ts
let cups: number;
```

---

## Type Inference with Expressions

```ts
let cups = Math.random() > 0.5 ? 10 : 5;
```

TypeScript infers:

```ts
let cups: number
```

### Mixed Types

```ts
let cups = Math.random() > 0.5 ? 10 : "5";
```

TypeScript infers:

```ts
let cups: string | number
```

This is called a **Union Type**.

---

## Type Annotation

Type Annotation means explicitly specifying a type.

### Syntax

```ts
let variableName: type = value;
```

### Example

```ts
let teaFlavor: string = "Masala Tea";
```

Here:

```ts
:string
```

is called a **Type Annotation**.

---

## Reassigning Values

### Valid

```ts
let teaFlavor: string = "Masala Tea";

teaFlavor = "Ginger Tea";
```

Both values are strings.

---

### Invalid

```ts
let teaFlavor: string = "Masala Tea";

teaFlavor = 2;
```

Error:

```text
Type 'number' is not assignable to type 'string'
```

---

# Common Type Error

The most common TypeScript error:

```text
Type 'X' is not assignable to type 'Y'
```

### Example

```ts
let channelName = "Chai Aur Code";

channelName = 101;
```

Error:

```text
Type 'number' is not assignable to type 'string'
```

### Meaning

A variable was declared as one type but later assigned a different type.

---

# TypeScript Error Categories

## 1. Syntax Errors

Errors related to invalid syntax.

### Example

```ts
let let drink = "Tea";
```

Invalid syntax.

---

## 2. Type Errors

Errors related to type mismatches.

### Example

```ts
let drink: string = "Tea";

drink = 100;
```

Error:

```text
Type 'number' is not assignable to type 'string'
```

---

# Primitive Types in TypeScript

## String

```ts
let teaName: string = "Masala Tea";
```

---

## Number

```ts
let teaOrder: number = 2;
```

---

## Boolean

```ts
let isTeaReady: boolean = true;
```

---

# When to Use Annotation vs Inference

## Prefer Inference

```ts
let drink = "Tea";
let price = 20;
let isAvailable = true;
```

TypeScript already understands the types.

---

## Use Annotation When Needed

```ts
let teaFlavor: string = "Masala Tea";
```

Useful when:

- Defining APIs
- Function parameters
- Function return types
- Public interfaces
- Complex data structures

---

# Interview Questions

## What is Type Inference?

TypeScript automatically determines the type of a variable based on its assigned value.

### Example

```ts
let name = "Rajat";
```

TypeScript infers:

```ts
string
```

---

## What is Type Annotation?

Explicitly specifying a type using `:`.

### Example

```ts
let name: string = "Rajat";
```

---

## Which is preferred: Annotation or Inference?

Generally, Type Inference is preferred because TypeScript can infer most primitive types automatically.

---

## What does this error mean?

```text
Type 'number' is not assignable to type 'string'
```

A value of one type is being assigned to a variable expecting another type.

---

## What are the basic primitive types in TypeScript?

```ts
string
number
boolean
null
undefined
```

---

# Quick Revision

- Type Inference = TypeScript automatically detects types.
- Type Annotation = Developer explicitly specifies types.
- `:` is used for annotations.
- Most common error:

```text
Type 'X' is not assignable to type 'Y'
```

- Primitive Types:
  - string
  - number
  - boolean
  - null
  - undefined

- Prefer inference for simple variables.
- Use annotations when clarity is needed.