# Lecture 10 - Functions in TypeScript

## Topics Covered

- Function Parameters
- Parameter Type Annotation
- Return Types
- Union Return Types
- Void Functions
- Optional Parameters
- Default Parameters
- Return Type Inference
- Object Parameters
- Complex Function Signatures

---

# Function Parameters

In TypeScript, parameters should have explicit types.

### Syntax

```ts
function functionName(
  parameter: type
) {}
```

---

## Example

```ts
function makeTea(
  type: string,
  cups: number
) {
  console.log(
    `Making ${cups} cups of ${type}`
  );
}
```

---

## Calling Function

```ts
makeTea("Masala Tea", 2);
```

✅ Valid

---

## Invalid

```ts
makeTea("Masala Tea", "2");
```

❌ Error

```text
Argument of type 'string'
is not assignable to parameter
of type 'number'
```

---

# Why Parameter Types Matter

Benefits:

- Better autocomplete
- Early error detection
- Better readability
- Safer code

---

# Return Types

Functions can explicitly define what type they return.

### Syntax

```ts
function fn(): ReturnType {
  return value;
}
```

---

## Example

```ts
function getTeaPrice(): number {
  return 25;
}
```

---

### Invalid

```ts
function getTeaPrice(): number {
  return "25";
}
```

❌ Error

Because the function promises to return a number.

---

# Why Return Types Matter

Without return types:

```ts
function getTeaPrice() {
  return 25;
}
```

TypeScript infers:

```ts
number
```

But explicit return types make code easier to understand and maintain.

---

# Return Type Inference

TypeScript can automatically infer return types.

### Example

```ts
function getTeaPrice() {
  return 25;
}
```

TypeScript infers:

```ts
number
```

---

## Recommendation

Prefer explicit return types in production code.

```ts
function getTeaPrice(): number {
  return 25;
}
```

---

# Union Return Types

Sometimes a function may return multiple types.

### Example

```ts
function makeOrder(
  order: string
): string | null {

  if (!order) {
    return null;
  }

  return order;
}
```

---

## Why Use Union Return Types?

Because both values are possible:

```ts
string
```

or

```ts
null
```

---

# Void Functions

A function that returns nothing.

### Syntax

```ts
function fn(): void {}
```

---

## Example

```ts
function logTea(): void {
  console.log("Tea is ready");
}
```

---

## Meaning

```ts
void
```

means:

> This function does not return any value.

---

# Optional Parameters

Parameters can be optional.

### Syntax

```ts
parameter?: type
```

---

## Example

```ts
function orderTea(
  type?: string
) {}
```

---

## Valid Calls

```ts
orderTea();

orderTea("Masala Tea");
```

Both are valid.

---

# Default Parameters

Provide a fallback value.

### Example

```ts
function orderTea(
  type: string = "Masala Tea"
) {
  console.log(type);
}
```

---

## Valid Calls

```ts
orderTea();

orderTea("Ginger Tea");
```

Output:

```text
Masala Tea
Ginger Tea
```

---

# Optional vs Default Parameters

## Optional

```ts
type?: string
```

Value may be:

```ts
undefined
```

---

## Default

```ts
type: string = "Masala Tea"
```

A default value is always available.

---

# Best Practice

Optional and default parameters should appear at the end.

### Good

```ts
function orderTea(
  cups: number,
  type?: string
) {}
```

---

### Avoid

```ts
function orderTea(
  type?: string,
  cups: number
) {}
```

---

# Object Parameters

Functions often receive objects.

### Example

```ts
function createTea(
  order: {
    type: string;
    sugar: number;
  }
) {}
```

---

## Calling Function

```ts
createTea({
  type: "Masala Tea",
  sugar: 2,
});
```

---

# Using Type Aliases

Preferred for readability.

### Type Definition

```ts
type TeaOrder = {
  type: string;
  sugar: number;
};
```

---

### Function

```ts
function createTea(
  order: TeaOrder
) {}
```

---

# Complex Object Parameters

Objects can contain multiple typed fields.

### Example

```ts
type TeaOrder = {
  type: string;
  sugar: number;
  size: "small" | "large";
};
```

---

## Function

```ts
function createTea(
  order: TeaOrder
): number {

  return 4;
}
```

---

# Reading Complex Signatures

Many developers get scared by signatures like:

```ts
function createTea(
  order: {
    type: string;
    sugar: number;
    size: "small" | "large";
  }
): number
```

But it's simply:

### Input

```ts
order
```

with defined structure.

### Output

```ts
number
```

---

# Function Summary

Every function has only two questions:

### Input

```ts
What data comes in?
```

---

### Output

```ts
What data goes out?
```

Everything else is type definitions around these two things.

---

# Interview Questions

## How do you define parameter types?

```ts
function greet(
  name: string
) {}
```

---

## How do you define a return type?

```ts
function greet(): string {
  return "Hello";
}
```

---

## What is a Void Function?

A function that does not return anything.

```ts
function log(): void {}
```

---

## What is an Optional Parameter?

```ts
name?: string
```

The parameter may or may not be provided.

---

## What is a Default Parameter?

```ts
name: string = "Guest"
```

Provides a fallback value.

---

## What is a Union Return Type?

```ts
string | null
```

The function can return either type.

---

## Does TypeScript Infer Return Types?

Yes.

```ts
function getPrice() {
  return 25;
}
```

TypeScript infers:

```ts
number
```

---

## Which is Better?

### Implicit

```ts
function getPrice() {
  return 25;
}
```

### Explicit

```ts
function getPrice(): number {
  return 25;
}
```

✅ Explicit return types are generally preferred in production code.

---

# Quick Revision

### Parameter Type

```ts
name: string
```

---

### Return Type

```ts
(): number
```

---

### Void

```ts
(): void
```

---

### Optional Parameter

```ts
name?: string
```

---

### Default Parameter

```ts
name: string = "Guest"
```

---

### Union Return

```ts
string | null
```

---

### Object Parameter

```ts
function createTea(
  order: TeaOrder
)
```

---

## 🔥 Interview Focus

Most Important Topics:

1. Function Parameter Types
2. Return Types
3. Return Type Inference
4. `void`
5. Optional Parameters (`?`)
6. Default Parameters
7. Union Return Types
8. Object Parameters
9. Type Alias with Functions
10. Reading Complex Function Signatures

These are the core TypeScript function concepts used in React, Next.js, Node.js, Express, and frontend interviews. :contentReference[oaicite:0]{index=0}