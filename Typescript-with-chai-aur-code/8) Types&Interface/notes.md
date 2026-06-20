# Lecture 8 - Type Aliases, Interfaces, Union, Intersection, Optional & Readonly Properties

# Type Aliases

A Type Alias allows us to create a custom name for a type.

### Syntax

```ts
type TypeName = {
  property: type;
};
```

---

## Problem Without Type Alias

```ts
function makeTea(order: {
  type: string;
  sugar: number;
  strong: boolean;
}) {}

function serveTea(order: {
  type: string;
  sugar: number;
  strong: boolean;
}) {}
```

The same object structure is repeated multiple times.

---

## Solution Using Type Alias

```ts
type TeaOrder = {
  type: string;
  sugar: number;
  strong: boolean;
};
```

Now reuse it:

```ts
function makeTea(order: TeaOrder) {}

function serveTea(order: TeaOrder) {}
```

### Benefits

- Reusability
- Better Readability
- Easier Maintenance
- Cleaner Code

---

# Type Alias for Literal Values

```ts
type TeaType =
  | "masala"
  | "ginger"
  | "lemon";
```

Only these values are allowed.

---

## Example

```ts
function orderTea(tea: TeaType) {
  console.log(tea);
}
```

Valid:

```ts
orderTea("masala");
orderTea("ginger");
```

Invalid:

```ts
orderTea("coffee");
```

❌ Error

---

# Literal Types

When exact values are allowed instead of generic types.

### Example

```ts
type TeaType =
  | "masala"
  | "ginger"
  | "lemon";
```

This is called a **Literal Type**.

---

# Interfaces

Interfaces define the structure (contract) of an object.

### Syntax

```ts
interface TeaRecipe {
  water: number;
  milk: number;
}
```

---

## Type Alias vs Interface

### Type Alias

```ts
type TeaRecipe = {
  water: number;
  milk: number;
};
```

### Interface

```ts
interface TeaRecipe {
  water: number;
  milk: number;
}
```

For simple objects, both work similarly.

---

# Using Interface with Classes

### Interface

```ts
interface TeaRecipe {
  water: number;
  milk: number;
}
```

### Class

```ts
class MasalaTea implements TeaRecipe {
  water = 100;
  milk = 50;
}
```

### Why Interface?

Classes commonly use interfaces with:

```ts
implements
```

---

# Important Interview Point

Prefer:

```ts
interface
```

when working with classes.

Prefer:

```ts
type
```

for unions, intersections, and advanced compositions.

---

# Union Types

Union means:

```ts
A OR B
```

### Syntax

```ts
|
```

---

## Example

```ts
type TeaType =
  | "masala"
  | "ginger"
  | "lemon";
```

Meaning:

```text
Either masala
OR ginger
OR lemon
```

Only one value is allowed at a time.

---

# Intersection Types

Intersection means:

```ts
A AND B
```

### Syntax

```ts
&
```

---

## Example

### Base Tea

```ts
type BaseTea = {
  teaLeaves: number;
};
```

### Extra Ingredient

```ts
type ExtraIngredient = {
  masala: number;
};
```

### Combine Both

```ts
type MasalaTea =
  BaseTea & ExtraIngredient;
```

---

## Result

```ts
const cup: MasalaTea = {
  teaLeaves: 2,
  masala: 1,
};
```

Both properties are required.

---

# Union vs Intersection

## Union (`|`)

```ts
A | B
```

Means:

```text
A OR B
```

---

## Intersection (`&`)

```ts
A & B
```

Means:

```text
A AND B
```

---

# Optional Properties

Not every property is required.

### Syntax

```ts
property?: type
```

---

## Example

```ts
type User = {
  username: string;
  bio?: string;
};
```

---

### Valid

```ts
const user1: User = {
  username: "Rajat",
};
```

---

### Also Valid

```ts
const user2: User = {
  username: "Rajat",
  bio: "Frontend Developer",
};
```

---

# Readonly Properties

Prevents modification after initialization.

### Syntax

```ts
readonly property: type
```

---

## Example

```ts
interface Config {
  readonly appName: string;
  version: number;
}
```

---

### Create Object

```ts
const config: Config = {
  appName: "MasterJi",
  version: 1,
};
```

---

### Invalid

```ts
config.appName = "ChaiCode";
```

❌ Error

```text
Cannot assign to 'appName'
because it is a read-only property.
```

---

### Valid

```ts
config.version = 2;
```

✅ Allowed

---

# Common Interview Question

## Why Use Readonly?

To protect important data from accidental modification.

Examples:

- App Configuration
- IDs
- Database Keys
- API Constants

---

# Type Alias vs Interface

| Feature | Type | Interface |
|----------|----------|----------|
| Object Types | ✅ | ✅ |
| Class Implementation | ⚠️ Less Common | ✅ Preferred |
| Union Types | ✅ | ❌ |
| Intersection Types | ✅ | ❌ |
| Readability for Classes | ⚠️ | ✅ |
| Advanced Type Composition | ✅ | ⚠️ |

---

# Interview Questions

## What is a Type Alias?

A custom name for a type.

```ts
type User = {
  name: string;
};
```

---

## What is an Interface?

A contract describing an object's structure.

```ts
interface User {
  name: string;
}
```

---

## Difference Between Type and Interface?

- Both define object shapes.
- Interfaces are preferred with classes.
- Types support unions and intersections.

---

## What is a Union Type?

```ts
A | B
```

Allows one of multiple possible types.

---

## What is an Intersection Type?

```ts
A & B
```

Combines multiple types into one.

---

## What is an Optional Property?

```ts
bio?: string
```

The property may or may not exist.

---

## What is Readonly?

A property that cannot be modified after initialization.

---

## What are Literal Types?

Types containing exact values.

```ts
type Status =
  | "success"
  | "error";
```

---

# Quick Revision

### Type Alias

```ts
type User = {}
```

---

### Interface

```ts
interface User {}
```

---

### Union

```ts
A | B
```

OR

---

### Intersection

```ts
A & B
```

AND

---

### Optional Property

```ts
bio?: string
```

---

### Readonly Property

```ts
readonly id: string
```

---

### Literal Type

```ts
"small" | "medium" | "large"
```

---

## 🔥 Interview Focus

Most Important Topics:

1. Type vs Interface
2. Union (`|`)
3. Intersection (`&`)
4. Optional Properties (`?`)
5. Readonly Properties
6. Literal Types
7. `implements` with Interfaces
8. Type Alias Reusability

These topics are extremely common in React + TypeScript interviews and production code. :contentReference[oaicite:0]{index=0}