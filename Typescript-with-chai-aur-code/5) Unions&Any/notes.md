# Lecture 5 - Union Types & Any

## Union Types

A Union Type allows a variable to store multiple possible types.

### Syntax

```ts
type1 | type2
```

### Example

```ts
let subscribers: number | string = 10;

subscribers = "1 Million";
subscribers = 1000000;
```

Both values are valid because the variable accepts either a `number` or a `string`.

---

# Why Use Union Types?

Sometimes data can come in different formats.

Example:

```ts
let userId: string | number;

userId = 101;
userId = "101";
```

Both values are valid.

---

# Union with Fixed Values (Literal Types)

One of the most common real-world uses of unions.

### API Request Status

```ts
let apiRequestStatus: "pending" | "success" | "error";

apiRequestStatus = "pending";
apiRequestStatus = "success";
apiRequestStatus = "error";
```

### Invalid Value

```ts
apiRequestStatus = "done";
```

❌ Error

Because `"done"` is not part of the allowed union.

---

## Benefits

- Better autocomplete
- Prevents invalid values
- Makes code more predictable
- Improves type safety

---

# Real World Example

### Airline Seat Type

```ts
let airlineSeat: "aisle" | "window" | "middle";

airlineSeat = "window";
airlineSeat = "middle";
```

### Invalid

```ts
airlineSeat = "front";
```

❌ Error

Only the predefined values are allowed.

---

# Any Type

`any` disables TypeScript's type checking.

### Example

```ts
let currentOrder: any;

currentOrder = 42;
currentOrder = "Tea";
currentOrder = true;
currentOrder = {};
```

All values are allowed.

---

## Why is `any` Dangerous?

TypeScript loses all type safety.

### Example

```ts
let currentOrder: any = "Tea";

currentOrder = 42;
```

No error.

TypeScript will not help detect mistakes.

---

# Avoid Using Any

### Bad Practice

```ts
let data: any;
```

### Preferred

```ts
let data: string;
```

or

```ts
let data: string | number;
```

Be as specific as possible.

---

# Union with Undefined

Sometimes a variable may not have a value initially.

### Example

```ts
let currentOrder: string | undefined;
```

This means:

```ts
currentOrder = "28";
currentOrder = undefined;
```

Both are valid.

---

# Practical Example

```ts
const orders = ["12", "28", "42"];

let currentOrder: string | undefined;

for (const order of orders) {
  if (order === "28") {
    currentOrder = order;
    break;
  }
}
```

TypeScript allows this because we explicitly told it that the value may be `undefined`.

---

# Why TypeScript Warns Here

### Example

```ts
let currentOrder: string;

console.log(currentOrder);
```

❌ Error

```text
Variable 'currentOrder' is used before being assigned.
```

TypeScript cannot guarantee that a value exists.

---

# Fix

```ts
let currentOrder: string | undefined;
```

Now TypeScript knows the variable may be undefined.

---

# Interview Questions

## What is a Union Type?

A Union Type allows a variable to hold values of multiple types.

### Example

```ts
let value: string | number;
```

---

## What is the Symbol Used for Union Types?

```ts
|
```

(pipe operator)

Example:

```ts
string | number
```

---

## What is a Literal Union Type?

A union made up of fixed values.

### Example

```ts
let status: "pending" | "success" | "error";
```

---

## What is the `any` Type?

`any` disables TypeScript's type checking.

Example:

```ts
let value: any;
```

---

## Why Should We Avoid `any`?

Because it removes type safety and allows any value to be assigned.

---

## Which is Better?

```ts
let data: any;
```

❌ Avoid

```ts
let data: string | number;
```

✅ Preferred

---

## What Does This Mean?

```ts
let user: string | undefined;
```

The variable can contain either:

- a string
- undefined

---

# Quick Revision

### Union Type

```ts
string | number
```

Allows multiple types.

---

### Literal Union

```ts
"pending" | "success" | "error"
```

Allows only specific values.

---

### Any

```ts
let value: any;
```

Disables type checking.

---

### Recommendation

- Prefer Union Types
- Avoid `any` whenever possible
- Use `undefined` explicitly when a value may not exist

---

## 🔥 Interview Focus

Most Important Concepts from this Lecture:

1. Union Types (`|`)
2. Literal Union Types
3. `any`
4. Why `any` is dangerous
5. `string | undefined`
6. Variable used before being assigned error