# Lecture 11 - Arrays, Tuples & Enums

## Topics Covered

- Arrays
- Array of Objects
- Readonly Arrays
- Multidimensional Arrays
- Tuples
- Optional Tuple Elements
- Readonly Tuples
- Named Tuples
- Enums
- String Enums
- Numeric Enums
- Const Enums

---

# Arrays

Arrays store multiple values of the same type.

## Syntax

```ts
let teaFlavors: string[] = [];
```

### Example

```ts
let teaFlavors: string[] = [
  "Masala",
  "Ginger"
];
```

---

## Invalid

```ts
let teaFlavors: string[] = [
  "Masala",
  10
];
```

❌ Error

```text
Type 'number' is not assignable to type 'string'
```

---

# Number Arrays

```ts
let teaPrices: number[] = [
  10,
  20,
  30
];
```

---

# Generic Array Syntax

Alternative way of writing arrays.

## Syntax

```ts
Array<Type>
```

### Example

```ts
let ratings: Array<number> = [
  4.5,
  5.0
];
```

Equivalent to:

```ts
let ratings: number[];
```

---

# Array of Objects

Very common in React and API responses.

## Type Definition

```ts
type Tea = {
  name: string;
  price: number;
};
```

---

## Array of Tea Objects

```ts
let menu: Tea[] = [
  {
    name: "Masala Tea",
    price: 15
  },
  {
    name: "Ginger Tea",
    price: 20
  }
];
```

---

# Readonly Arrays

Prevents modification after creation.

## Syntax

```ts
readonly string[]
```

### Example

```ts
const cities: readonly string[] = [
  "Delhi",
  "Jaipur"
];
```

---

## Invalid

```ts
cities.push("Pune");
```

❌ Error

Cannot modify readonly array.

---

# Multidimensional Arrays

Arrays inside arrays.

## Syntax

```ts
number[][]
```

---

## Example

```ts
const table: number[][] = [
  [1, 2, 3],
  [4, 5, 6]
];
```

---

# Tuples

Tuples allow fixed-length arrays with fixed types and order.

## Syntax

```ts
type TeaTuple = [
  string,
  number
];
```

---

## Example

```ts
let tea: TeaTuple = [
  "Masala",
  20
];
```

---

## Invalid Order

```ts
let tea: TeaTuple = [
  20,
  "Masala"
];
```

❌ Error

Because tuple order matters.

---

# Why Tuples?

Arrays:

```ts
(string | number)[]
```

No fixed order.

Tuples:

```ts
[string, number]
```

Strict order.

---

# Optional Tuple Elements

## Syntax

```ts
type UserInfo = [
  string,
  number,
  boolean?
];
```

---

## Example

```ts
const user1: UserInfo = [
  "Rajat",
  100
];
```

---

## Also Valid

```ts
const user2: UserInfo = [
  "Rajat",
  100,
  true
];
```

---

# Readonly Tuples

Prevent tuple modification.

## Example

```ts
type Location =
  readonly [
    number,
    number
  ];
```

---

```ts
const coords: Location = [
  28.66,
  32.22
];
```

---

## Invalid

```ts
coords[0] = 50;
```

❌ Error

Readonly tuple cannot be modified.

---

# Named Tuples

Improves readability.

## Example

```ts
type TeaItem = [
  name: string,
  price: number
];
```

---

## Usage

```ts
const tea: TeaItem = [
  "Masala Tea",
  25
];
```

Named tuples make it easier to understand what each position represents.

---

# Tuple Gotcha ⚠️

Tuples are internally arrays.

### Example

```ts
let t: [string, number] = [
  "Tea",
  10
];

t.push("Extra");
```

Surprisingly, TypeScript may allow this.

Reason:

> Tuples are implemented using arrays underneath.

Be careful while using tuple mutation methods.

---

# Enums

Enums restrict values to predefined choices.

## Syntax

```ts
enum EnumName {}
```

---

# Basic Enum

```ts
enum CupSize {
  Small,
  Medium,
  Large
}
```

---

## Usage

```ts
let size = CupSize.Large;
```

---

### Benefits

- Autocomplete
- Restricted values
- Better readability
- Fewer bugs

---

# Numeric Enums

## Example

```ts
enum Status {
  Pending = 100,
  Served,
  Cancelled
}
```

Values become:

```ts
Pending   = 100
Served    = 101
Cancelled = 102
```

---

# Auto Increment Behavior

```ts
enum Status {
  Pending = 5,
  Served,
  Cancelled
}
```

Result:

```ts
Pending   = 5
Served    = 6
Cancelled = 7
```

⚠️ Be aware of automatic incrementing.

---

# String Enums

Preferred in modern applications.

## Example

```ts
enum TeaType {
  MASALA = "Masala",
  GINGER = "Ginger"
}
```

---

## Usage

```ts
function makeTea(
  type: TeaType
) {
  console.log(type);
}
```

---

```ts
makeTea(
  TeaType.MASALA
);
```

✅ Valid

---

```ts
makeTea("Masala");
```

❌ Error

Must use enum values.

---

# Why String Enums?

Benefits:

- More readable
- Better debugging
- No auto-increment surprises
- Better API communication

---

# Heterogeneous Enums

Mixing strings and numbers.

## Example

```ts
enum Random {
  ID = 1,
  NAME = "Tea"
}
```

---

⚠️ Valid but generally discouraged.

Avoid mixing data types inside enums.

---

# Const Enums

Used for optimization.

## Syntax

```ts
const enum Sugar {
  Low = 1,
  Medium = 2,
  High = 3
}
```

---

## Usage

```ts
const sugar =
  Sugar.Medium;
```

---

### Benefit

Values are inlined during compilation.

---

# Array vs Tuple

| Feature | Array | Tuple |
|----------|----------|----------|
| Fixed Length | ❌ | ✅ |
| Fixed Order | ❌ | ✅ |
| Same Type Elements | Usually | Not Required |
| Flexibility | High | Low |
| Strictness | Low | High |

---

# Enum vs Union Type

### Enum

```ts
enum TeaType {
  MASALA,
  GINGER
}
```

---

### Union

```ts
type TeaType =
  | "Masala"
  | "Ginger";
```

Many modern TypeScript developers prefer union types over enums for simple cases.

---

# Interview Questions

## How do you define an array of strings?

```ts
let tea: string[];
```

---

## Alternative Array Syntax?

```ts
Array<string>
```

---

## What is an Array of Objects?

```ts
type Tea = {
  name: string;
  price: number;
};

let menu: Tea[];
```

---

## What is a Tuple?

A fixed-length array with fixed types and order.

```ts
[string, number]
```

---

## Difference Between Array and Tuple?

Array:

```ts
string[]
```

Flexible.

Tuple:

```ts
[string, number]
```

Fixed structure.

---

## What is a Readonly Array?

An array that cannot be modified after creation.

---

## What is an Enum?

A way to define a fixed set of allowed values.

---

## Difference Between Numeric and String Enums?

Numeric Enum:

```ts
enum Status {
  Pending,
  Served
}
```

String Enum:

```ts
enum Status {
  Pending = "Pending"
}
```

String enums are generally preferred.

---

## Why Avoid Heterogeneous Enums?

Because they mix different data types and reduce readability.

---

# Quick Revision

### String Array

```ts
string[]
```

---

### Number Array

```ts
number[]
```

---

### Generic Array

```ts
Array<number>
```

---

### Tuple

```ts
[string, number]
```

---

### Optional Tuple Element

```ts
[string, number, boolean?]
```

---

### Readonly Array

```ts
readonly string[]
```

---

### Enum

```ts
enum TeaType {}
```

---

### String Enum

```ts
enum TeaType {
  MASALA = "Masala"
}
```

---

### Const Enum

```ts
const enum Sugar {}
```

---

## 🔥 Interview Focus

Most Important Topics:

1. Arrays (`string[]`, `number[]`)
2. Array of Objects
3. Readonly Arrays
4. Tuples
5. Optional Tuple Elements
6. Readonly Tuples
7. Named Tuples
8. Enums
9. String Enums vs Numeric Enums
10. Tuple Gotcha (`push()` issue)

Modern frontend interviews frequently ask:
- Array vs Tuple
- Enum vs Union Types
- Readonly Arrays
- String Enums
- Array of Objects

These concepts are heavily used in React, Next.js, Redux, Zustand, API responses, and production TypeScript applications. :contentReference[oaicite:0]{index=0}