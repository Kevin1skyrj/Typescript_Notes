# Lecture 6 - Type Guards, Type Narrowing, Unknown & Any

## Type Narrowing

Type Narrowing is the process of reducing a broad type (Union Type) into a more specific type.

### Example

```ts
function getTea(kind: string | number) {
  if (typeof kind === "string") {
    return `Making ${kind} tea`;
  }

  return `Tea Order #${kind}`;
}
```

### What's Happening?

Inside:

```ts
if (typeof kind === "string")
```

TypeScript knows:

```ts
kind: string
```

And outside:

```ts
kind: number
```

This is called **Type Narrowing**.

---

# Using typeof for Type Guards

### Syntax

```ts
typeof variable === "string"
typeof variable === "number"
typeof variable === "boolean"
```

### Example

```ts
function process(value: string | number) {
  if (typeof value === "string") {
    return value.toUpperCase();
  }

  return value.toFixed(2);
}
```

TypeScript automatically narrows the type.

---

# Truthiness Narrowing

Used when a value may or may not exist.

### Example

```ts
function serveTea(message?: string) {
  if (message) {
    return `Serving ${message}`;
  }

  return "Serving default Masala Tea";
}
```

### Benefit

Inside:

```ts
if (message)
```

TypeScript guarantees:

```ts
message: string
```

Not:

```ts
string | undefined
```

---

# Exhaustive Checks

When handling multiple possible values, check every case.

### Example

```ts
function orderTea(
  size: "small" | "medium" | "large" | number
) {
  if (size === "small") {
    return "Small Cutting Tea";
  }

  if (size === "medium" || size === "large") {
    return "Extra Tea";
  }

  return `Order ${size}`;
}
```

This ensures every possible value is handled.

---

# Type Guards with Classes

### Example

```ts
class KulhadTea {
  serve() {
    return "Serving Kulhad Tea";
  }
}

class CuttingTea {
  serve() {
    return "Serving Cutting Tea";
  }
}
```

---

## instanceof Type Guard

```ts
function serveTea(
  tea: KulhadTea | CuttingTea
) {
  if (tea instanceof KulhadTea) {
    return tea.serve();
  }

  return tea.serve();
}
```

### Purpose

Checks whether an object belongs to a specific class.

---

# Custom Types

### Creating a Type

```ts
type TeaOrder = {
  type: string;
  sugar: number;
};
```

---

## Using Custom Types

```ts
const order: TeaOrder = {
  type: "Masala",
  sugar: 2,
};
```

---

# Custom Type Guard

### Type Definition

```ts
type TeaOrder = {
  type: string;
  sugar: number;
};
```

### Type Guard Function

```ts
function isTeaOrder(
  obj: any
): obj is TeaOrder {
  return (
    typeof obj === "object" &&
    obj !== null &&
    typeof obj.type === "string" &&
    typeof obj.sugar === "number"
  );
}
```

---

## Why Use It?

After validation:

```ts
if (isTeaOrder(item)) {
  console.log(item.type);
  console.log(item.sugar);
}
```

TypeScript knows:

```ts
item: TeaOrder
```

---

# Discriminated Unions

One of the most important TypeScript interview concepts.

### Example

```ts
type MasalaTea = {
  type: "masala";
  spiceLevel: number;
};

type GingerTea = {
  type: "ginger";
};

type ElaichiTea = {
  type: "elaichi";
};
```

---

## Combine Types

```ts
type Tea =
  | MasalaTea
  | GingerTea
  | ElaichiTea;
```

---

## Narrowing with switch

```ts
function makeTea(order: Tea) {
  switch (order.type) {
    case "masala":
      return "Masala Tea";

    case "ginger":
      return "Ginger Tea";

    case "elaichi":
      return "Elaichi Tea";
  }
}
```

### Benefits

- Better autocomplete
- Safer code
- Exhaustive checking
- Easier maintenance

---

# Using "in" Operator

Used to check whether a property exists.

### Example

```ts
type MasalaTea = {
  spiceLevel: number;
};

type GingerTea = {
  aroma: string;
};

function brew(
  order: MasalaTea | GingerTea
) {
  if ("spiceLevel" in order) {
    return order.spiceLevel;
  }
}
```

### Benefit

TypeScript automatically narrows the type.

---

# Any Type

```ts
let value: any;
```

### Characteristics

- Accepts anything
- No type checking
- No safety
- No validation

Example:

```ts
let value: any = "Tea";

value = 10;
value = true;
value = {};
```

All valid.

---

# Unknown Type

```ts
let value: unknown;
```

### Characteristics

- Safer than `any`
- Must be checked before use
- Forces type narrowing

Example:

```ts
let value: unknown = "Tea";

if (typeof value === "string") {
  console.log(value.toUpperCase());
}
```

---

# Any vs Unknown

## any

```ts
let value: any;

value.toUpperCase();
```

✅ Allowed

No checking required.

---

## unknown

```ts
let value: unknown;

value.toUpperCase();
```

❌ Error

Must narrow first:

```ts
if (typeof value === "string") {
  value.toUpperCase();
}
```

✅ Allowed

---

# Which One Should You Use?

Prefer:

```ts
unknown
```

Avoid:

```ts
any
```

Use `any` only when absolutely necessary.

---

# Interview Questions

## What is Type Narrowing?

The process of reducing a broader type into a more specific type.

---

## What is a Type Guard?

A runtime check that helps TypeScript determine a more specific type.

Examples:

```ts
typeof
instanceof
in
custom type guards
```

---

## What is the difference between Any and Unknown?

### any

- No type checking
- Unsafe

### unknown

- Type safe
- Must be narrowed before use

---

## What is instanceof used for?

To check whether an object belongs to a specific class.

---

## What is the "in" operator used for?

To check whether a property exists in an object.

---

## What is a Custom Type Guard?

A function returning:

```ts
obj is SomeType
```

which tells TypeScript the object's type after validation.

---

## What are Discriminated Unions?

Union types that contain a common property (usually `type`) used for narrowing.

Example:

```ts
type Tea =
  | MasalaTea
  | GingerTea
  | ElaichiTea;
```

---

# Quick Revision

- Type Narrowing = Reduce broader types to specific types.
- `typeof` → Primitive type checking.
- `instanceof` → Class checking.
- `in` → Property existence checking.
- Custom Type Guards → `obj is Type`.
- Prefer `unknown` over `any`.
- Discriminated Unions are heavily used in production React + TypeScript code.
- `switch` + Discriminated Unions is a common interview pattern.