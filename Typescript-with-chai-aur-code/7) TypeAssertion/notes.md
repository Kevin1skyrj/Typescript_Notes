# Lecture 7 - Type Assertion, Any vs Unknown, Never Type

# Type Assertion

Type Assertion tells TypeScript:

> "Trust me, I know the actual type of this value."

It does **not** perform type conversion.

---

## Syntax

```ts
value as Type
```

### Example

```ts
let response: any = "Chai Aur Code";

let length = (response as string).length;
```

Now TypeScript treats `response` as a string and provides string methods.

---

## Why Type Assertion is Needed

Sometimes TypeScript cannot determine the exact type.

Common scenarios:

- API Responses
- Local Storage Data
- Environment Variables
- DOM Elements

---

# Type Assertion with JSON.parse()

### Custom Type

```ts
type Book = {
  name: string;
};
```

### Example

```ts
const bookString =
  '{"name":"The One Thing"}';

const book = JSON.parse(bookString) as Book;
```

Now TypeScript knows:

```ts
book.name
```

is valid.

Without assertion:

```ts
const book = JSON.parse(bookString);
```

TypeScript cannot guarantee the structure of the parsed object.

---

# Type Assertion with DOM Elements

### Example

```ts
const username =
  document.getElementById("username")
  as HTMLInputElement;
```

Now TypeScript provides:

```ts
username.value
username.focus()
```

and other input-specific properties.

---

# Important Note

Type Assertion does NOT convert data.

❌ Wrong Understanding

```ts
let value = "42" as number;
```

This does not convert a string into a number.

Type Assertion only changes TypeScript's understanding of the type.

---

# Any Type

```ts
let value: any;
```

### Characteristics

- Accepts any value
- No type checking
- No safety
- No validation

Example:

```ts
let value: any = "Tea";

value = 123;
value = true;

value.toUpperCase();
```

TypeScript allows everything.

---

# Unknown Type

```ts
let value: unknown;
```

### Characteristics

- Safer alternative to `any`
- Requires type checking before use
- Prevents unsafe operations

Example:

```ts
let value: unknown = "Tea";
```

---

## Invalid Usage

```ts
value.toUpperCase();
```

❌ Error

TypeScript doesn't know the type yet.

---

## Correct Usage

```ts
if (typeof value === "string") {
  value.toUpperCase();
}
```

✅ Valid

Because the type is narrowed first.

---

# Any vs Unknown

## Any

```ts
let value: any;

value.toUpperCase();
```

✅ Allowed

No checks required.

---

## Unknown

```ts
let value: unknown;

value.toUpperCase();
```

❌ Error

Must narrow first.

---

## Recommendation

Prefer:

```ts
unknown
```

Avoid:

```ts
any
```

unless absolutely necessary.

---

# Type Assertion with Unknown

### Example

```ts
let data: unknown = "Chai Aur Code";

let text = data as string;

console.log(text.toUpperCase());
```

---

# Error Handling in TypeScript

A common mistake:

```ts
try {
  // code
} catch (error) {
  console.log(error.message);
}
```

TypeScript cannot guarantee that `error` has a `message` property.

---

## Correct Approach

```ts
try {
  // code
} catch (error) {
  if (error instanceof Error) {
    console.log(error.message);
  }
}
```

### Why?

`instanceof Error` narrows the type.

Now TypeScript knows:

```ts
error: Error
```

---

# Never Type

One of the most important advanced TypeScript types.

```ts
never
```

Represents a value that should never occur.

---

# Use Case 1: Exhaustive Checks

### Example

```ts
type Role =
  | "admin"
  | "user";
```

```ts
function redirect(role: Role) {
  if (role === "admin") {
    return;
  }

  if (role === "user") {
    return;
  }

  role;
}
```

At this point:

```ts
role: never
```

because all possible cases have already been handled.

---

## Why is This Useful?

Suppose another developer adds:

```ts
type Role =
  | "admin"
  | "user"
  | "superAdmin";
```

Now TypeScript detects that the new case is not handled.

This helps catch bugs during development.

---

# Better Never Pattern

```ts
function exhaustiveCheck(
  value: never
): never {
  throw new Error(
    `Unhandled value: ${value}`
  );
}
```

Usage:

```ts
switch (role) {
  case "admin":
    break;

  case "user":
    break;

  default:
    exhaustiveCheck(role);
}
```

---

# Use Case 2: Functions That Never Return

### Example

```ts
function neverReturn(): never {
  while (true) {}
}
```

The function never finishes execution.

---

## Another Example

```ts
function throwError(
  message: string
): never {
  throw new Error(message);
}
```

This function always throws an error and never returns.

---

# Void vs Never

## Void

```ts
function log(): void {
  console.log("Hello");
}
```

Meaning:

> Function finishes execution but returns nothing useful.

---

## Never

```ts
function crash(): never {
  throw new Error("Boom");
}
```

Meaning:

> Function never completes normally.

---

# Interview Questions

## What is Type Assertion?

A way to tell TypeScript the expected type of a value.

```ts
value as string
```

---

## Does Type Assertion Convert Data?

No.

It only affects TypeScript's type checking.

---

## When is Type Assertion Commonly Used?

- JSON.parse()
- DOM Elements
- Environment Variables
- Third-party Libraries

---

## Difference Between Any and Unknown?

### Any

- No checks
- Unsafe

### Unknown

- Requires narrowing
- Type safe

---

## What is Never?

A type representing values that should never exist.

---

## Common Use Cases of Never?

1. Exhaustive checking
2. Functions that never return

---

## Difference Between Void and Never?

### Void

Function completes successfully.

### Never

Function never completes or always throws.

---

# Quick Revision

### Type Assertion

```ts
value as string
```

---

### Any

```ts
let value: any;
```

Avoid when possible.

---

### Unknown

```ts
let value: unknown;
```

Preferred over `any`.

---

### Error Handling

```ts
if (error instanceof Error)
```

---

### Never

```ts
function throwError(): never
```

---

### Main Uses of Never

- Exhaustive Checks
- Infinite Loops
- Functions that always throw errors

---

## 🔥 Interview Focus

Most Important Concepts:

1. Type Assertion (`as`)
2. JSON.parse() + Assertion
3. DOM Type Assertions
4. Any vs Unknown
5. `instanceof Error`
6. Never Type
7. Void vs Never
8. Exhaustive Checking Pattern

These are frequently asked in TypeScript and React + TypeScript interviews. :contentReference[oaicite:0]{index=0}