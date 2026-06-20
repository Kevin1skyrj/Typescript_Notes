# Lecture 9 - Objects in TypeScript

## Topics Covered

- Object Type Inference
- Object Type Declaration
- Type Aliases with Objects
- Duck Typing
- Structural Typing
- Missing Properties Checks
- Nested Type Composition
- Utility Types
  - Partial
  - Required
  - Pick
  - Omit

---

# Object Type Inference

TypeScript automatically infers object property types.

### Example

```ts
const tea = {
  name: "Masala Tea",
  price: 20,
  isHot: true,
};
```

TypeScript infers:

```ts
{
  name: string;
  price: number;
  isHot: boolean;
}
```

---

# Explicit Object Type Declaration

Instead of relying on inference, we can define object types manually.

### Example

```ts
let tea: {
  name: string;
  price: number;
  isHot: boolean;
};
```

### Assigning Values

```ts
tea = {
  name: "Ginger Tea",
  price: 25,
  isHot: true,
};
```

---

# Type Safety

### Invalid

```ts
tea = {
  name: "Ginger Tea",
  price: 25,
  isHot: 5,
};
```

❌ Error

```text
Type 'number' is not assignable to type 'boolean'
```

---

# Type Alias with Objects

Instead of repeating object structures, create reusable types.

### Example

```ts
type Tea = {
  name: string;
  price: number;
  ingredients: string[];
};
```

---

## Using the Type

```ts
const gingerTea: Tea = {
  name: "Ginger Tea",
  price: 25,
  ingredients: [
    "Ginger",
    "Tea Leaves",
  ],
};
```

---

# Array Property Types

### Example

```ts
type Tea = {
  ingredients: string[];
};
```

Only strings are allowed.

### Invalid

```ts
ingredients: [
  "Ginger",
  2
];
```

❌ Error

Because the array expects only strings.

---

# Duck Typing

One of the most important TypeScript concepts.

### Principle

> If it looks like a duck and behaves like a duck, it can be treated as a duck.

TypeScript checks structure, not exact type names.

---

## Example

### Type

```ts
type Cup = {
  size: string;
};
```

### Object

```ts
const bigCup = {
  size: "500ml",
  material: "Steel",
};
```

---

### Assignment

```ts
let cup: Cup = bigCup;
```

✅ Valid

Because `bigCup` contains the required property:

```ts
size
```

Extra properties are allowed.

---

# Structural Typing

TypeScript compares object structures.

It does NOT compare object names.

### Example

```ts
type Brew = {
  brewTime: number;
};
```

```ts
const coffee = {
  brewTime: 5,
  beans: "Arabica",
};
```

```ts
let tea: Brew = coffee;
```

✅ Valid

Because the required structure exists.

---

# Missing Property Checks

Extra properties are usually okay.

Missing required properties are not.

---

## Example

```ts
type User = {
  username: string;
  password: string;
};
```

### Invalid

```ts
const user: User = {
  username: "chaiCode",
};
```

❌ Error

Missing:

```ts
password
```

---

# Splitting Types into Smaller Pieces

Common production-level practice.

---

## Item

```ts
type Item = {
  name: string;
  quantity: number;
};
```

---

## Address

```ts
type Address = {
  street: string;
  pin: number;
};
```

---

## Order

```ts
type Order = {
  orderId: string;
  items: Item[];
  address: Address;
};
```

---

### Benefits

- Better readability
- Reusability
- Easier maintenance
- Cleaner codebase

---

# Utility Types

TypeScript provides built-in utility types.

---

# Partial<T>

Makes all properties optional.

---

## Example

```ts
type Tea = {
  name: string;
  price: number;
  isHot: boolean;
};
```

```ts
function updateTea(
  updates: Partial<Tea>
) {}
```

---

### Valid

```ts
updateTea({
  price: 25,
});
```

Only one property is enough.

---

### Also Valid

```ts
updateTea({});
```

Because all properties become optional.

---

# Required<T>

Makes all properties required.

---

## Example

```ts
type TeaOrder = {
  name?: string;
  quantity?: number;
};
```

```ts
function placeOrder(
  order: Required<TeaOrder>
) {}
```

---

### Invalid

```ts
placeOrder({
  name: "Masala Tea",
});
```

❌ Error

Missing:

```ts
quantity
```

---

### Valid

```ts
placeOrder({
  name: "Masala Tea",
  quantity: 2,
});
```

---

# Pick<T, Keys>

Select specific properties from a type.

---

## Original Type

```ts
type Tea = {
  name: string;
  price: number;
  isHot: boolean;
  ingredients: string[];
};
```

---

## Pick Example

```ts
type BasicTeaInfo =
  Pick<Tea, "name" | "price">;
```

Result:

```ts
{
  name: string;
  price: number;
}
```

---

### Usage

```ts
const tea: BasicTeaInfo = {
  name: "Lemon Tea",
  price: 30,
};
```

---

# Omit<T, Keys>

Removes specific properties.

---

## Original Type

```ts
type Tea = {
  name: string;
  price: number;
  isHot: boolean;
  secretIngredients: string[];
};
```

---

## Omit Example

```ts
type PublicTea =
  Omit<Tea, "secretIngredients">;
```

Result:

```ts
{
  name: string;
  price: number;
  isHot: boolean;
}
```

---

### Usage

```ts
const tea: PublicTea = {
  name: "Masala Tea",
  price: 20,
  isHot: true,
};
```

---

# Utility Types Summary

| Utility Type | Purpose |
|-------------|----------|
| Partial<T> | Makes all properties optional |
| Required<T> | Makes all properties mandatory |
| Pick<T, K> | Select specific properties |
| Omit<T, K> | Remove specific properties |

---

# Interview Questions

## What is Duck Typing?

A concept where TypeScript checks object structure rather than object names.

---

## What is Structural Typing?

Compatibility is based on properties and shape rather than explicit type names.

---

## Difference Between Extra and Missing Properties?

### Extra Properties

Usually allowed.

```ts
{
  size: "500ml",
  material: "Steel"
}
```

---

### Missing Properties

Not allowed.

```ts
{
  username: "Rajat"
}
```

if required fields are missing.

---

## What is Partial<T>?

Makes every property optional.

```ts
Partial<User>
```

---

## What is Required<T>?

Makes every property mandatory.

```ts
Required<User>
```

---

## What is Pick<T, K>?

Creates a new type using selected properties.

---

## What is Omit<T, K>?

Creates a new type by removing selected properties.

---

# Quick Revision

### Object Type

```ts
{
  name: string;
  price: number;
}
```

---

### Duck Typing

Structure matters, names do not.

---

### Partial

```ts
Partial<T>
```

All optional.

---

### Required

```ts
Required<T>
```

All mandatory.

---

### Pick

```ts
Pick<T, K>
```

Select properties.

---

### Omit

```ts
Omit<T, K>
```

Remove properties.

---

## 🔥 Interview Focus

Very Important Topics:

1. Object Type Inference
2. Type Aliases with Objects
3. Duck Typing
4. Structural Typing
5. Partial<T>
6. Required<T>
7. Pick<T, K>
8. Omit<T, K>
9. Missing vs Extra Properties
10. Nested Object Types

These utility types are used heavily in React, Next.js, API responses, Redux, Zustand, and production TypeScript applications. :contentReference[oaicite:0]{index=0}