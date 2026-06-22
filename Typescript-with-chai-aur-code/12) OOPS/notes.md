# Lecture 12 - Object-Oriented Programming (OOP) in TypeScript

## Topics Covered

- Classes
- Constructors
- `this` Keyword
- Access Modifiers
  - Public
  - Private
  - Protected
- Readonly Properties
- Getters & Setters
- Static Members
- Abstract Classes
- Inheritance
- Composition

---

# Classes

Classes act as blueprints for creating objects.

## Syntax

```ts
class Tea {
  flavor: string;
  price: number;
}
```

---

## Creating Objects

```ts
const masalaTea = new Tea();
```

---

### Accessing Properties

```ts
masalaTea.flavor = "Masala";
masalaTea.price = 20;
```

---

# Constructor

A constructor initializes an object when it is created.

## Syntax

```ts
class Tea {
  flavor: string;
  price: number;

  constructor(
    flavor: string,
    price: number
  ) {
    this.flavor = flavor;
    this.price = price;
  }
}
```

---

## Creating an Instance

```ts
const tea = new Tea(
  "Ginger",
  20
);
```

---

# this Keyword

`this` refers to the current object instance.

## Example

```ts
class Tea {
  flavor: string;

  constructor(
    flavor: string
  ) {
    this.flavor = flavor;
  }
}
```

---

### Meaning

```ts
this.flavor
```

refers to the flavor of the object currently being created.

---

# Access Modifiers

TypeScript provides access control for class members.

---

# Public

Accessible from anywhere.

## Example

```ts
class Tea {
  public flavor: string =
    "Masala";
}
```

---

## Access

```ts
const tea = new Tea();

tea.flavor;
```

✅ Allowed

---

# Private

Accessible only inside the class.

## Example

```ts
class Tea {
  private secretIngredient =
    "Cardamom";
}
```

---

## Invalid

```ts
const tea = new Tea();

tea.secretIngredient;
```

❌ Error

---

## Access Through Methods

```ts
class Tea {
  private secretIngredient =
    "Cardamom";

  reveal() {
    return this.secretIngredient;
  }
}
```

---

```ts
const tea = new Tea();

tea.reveal();
```

✅ Allowed

---

# Protected

Accessible:

- Inside the class
- Inside child classes

Not accessible outside.

---

## Example

```ts
class Shop {
  protected shopName =
    "Chai Corner";
}
```

---

# Inheritance

```ts
class Branch extends Shop {
  getName() {
    return this.shopName;
  }
}
```

---

## Valid

```ts
const branch =
  new Branch();

branch.getName();
```

---

## Invalid

```ts
branch.shopName;
```

❌ Error

---

# Access Modifier Summary

| Modifier | Same Class | Child Class | Outside Class |
|-----------|-----------|-----------|-----------|
| public | ✅ | ✅ | ✅ |
| private | ✅ | ❌ | ❌ |
| protected | ✅ | ✅ | ❌ |

---

# Parameter Properties

A TypeScript shortcut.

Instead of:

```ts
class Tea {
  flavor: string;

  constructor(
    flavor: string
  ) {
    this.flavor = flavor;
  }
}
```

Use:

```ts
class Tea {
  constructor(
    public flavor: string
  ) {}
}
```

TypeScript automatically creates and assigns the property.

---

# Private Field (#)

Modern JavaScript private fields.

## Example

```ts
class Wallet {
  #balance = 100;
}
```

---

## Access

```ts
wallet.#balance;
```

❌ Error

---

## Getter Method

```ts
class Wallet {
  #balance = 100;

  getBalance() {
    return this.#balance;
  }
}
```

---

# Readonly Properties

Can be assigned once.

After that, they cannot be modified.

---

## Example

```ts
class Cup {
  readonly capacity: number;

  constructor(
    capacity: number
  ) {
    this.capacity = capacity;
  }
}
```

---

## Valid

```ts
const cup =
  new Cup(250);
```

---

## Invalid

```ts
cup.capacity = 500;
```

❌ Error

---

# Getters

Used to control reading values.

## Example

```ts
class ModernTea {
  private _sugar = 0;

  get sugar() {
    return this._sugar;
  }
}
```

---

## Usage

```ts
const tea =
  new ModernTea();

console.log(
  tea.sugar
);
```

---

# Setters

Used to control updates.

## Example

```ts
class ModernTea {
  private _sugar = 0;

  set sugar(
    value: number
  ) {
    this._sugar = value;
  }
}
```

---

# Validation Example

```ts
class ModernTea {
  private _sugar = 0;

  set sugar(
    value: number
  ) {
    if (value > 5) {
      throw new Error(
        "Too Sweet"
      );
    }

    this._sugar = value;
  }
}
```

---

## Usage

```ts
tea.sugar = 3;
```

✅ Valid

---

```ts
tea.sugar = 10;
```

❌ Error

---

# Static Members

Belong to the class itself.

Not individual objects.

---

## Example

```ts
class Tea {
  static shopName =
    "ChaiCode Cafe";
}
```

---

## Access

```ts
Tea.shopName;
```

✅ Correct

---

```ts
const tea =
  new Tea();

tea.shopName;
```

❌ Invalid

---

# Why Use Static?

Used for:

- Constants
- Configuration
- Utility Methods
- Shared Data

---

# Abstract Classes

Cannot be instantiated directly.

Used as blueprints.

---

## Example

```ts
abstract class Drink {
  abstract make(): void;
}
```

---

## Invalid

```ts
const d =
  new Drink();
```

❌ Error

---

# Implementing Abstract Class

```ts
class MyTea
  extends Drink {

  make(): void {
    console.log(
      "Brewing Tea"
    );
  }
}
```

---

## Rule

Every child class must implement abstract methods.

---

# Inheritance

Allows one class to reuse another class.

---

## Example

```ts
class Shop {
  protected shopName =
    "Chai Corner";
}

class Branch
  extends Shop {

  getName() {
    return this.shopName;
  }
}
```

---

# Composition

A class uses another class instead of extending it.

---

## Heater Class

```ts
class Heater {
  heat() {
    console.log(
      "Heating"
    );
  }
}
```

---

## TeaMaker Class

```ts
class TeaMaker {

  constructor(
    private heater: Heater
  ) {}

  makeTea() {
    this.heater.heat();
  }
}
```

---

# Composition vs Inheritance

## Inheritance

```ts
class Branch
  extends Shop
```

Represents:

```text
IS-A Relationship
```

Example:

```text
Branch IS-A Shop
```

---

## Composition

```ts
class TeaMaker {
  constructor(
    private heater: Heater
  ) {}
}
```

Represents:

```text
HAS-A Relationship
```

Example:

```text
TeaMaker HAS-A Heater
```

---

# Interview Questions

## What is a Class?

A blueprint used to create objects.

---

## What is a Constructor?

A special method executed when an object is created.

---

## What does `this` refer to?

The current object instance.

---

## Difference Between Public, Private and Protected?

| Modifier | Accessible Outside? |
|-----------|-----------|
| public | ✅ |
| private | ❌ |
| protected | ❌ |

Protected is accessible inside child classes.

---

## What is a Readonly Property?

A property that can only be assigned once.

---

## What are Getters and Setters?

Methods used to control reading and updating values.

---

## What is a Static Member?

A member belonging to the class rather than object instances.

---

## What is an Abstract Class?

A class that cannot be instantiated directly and acts as a blueprint.

---

## Difference Between Inheritance and Composition?

### Inheritance

```text
IS-A
```

Relationship.

### Composition

```text
HAS-A
```

Relationship.

---

# Quick Revision

### Class

```ts
class Tea {}
```

---

### Constructor

```ts
constructor() {}
```

---

### this

```ts
this.flavor
```

---

### Public

```ts
public name
```

---

### Private

```ts
private name
```

---

### Protected

```ts
protected name
```

---

### Readonly

```ts
readonly id
```

---

### Getter

```ts
get sugar()
```

---

### Setter

```ts
set sugar()
```

---

### Static

```ts
static shopName
```

---

### Abstract Class

```ts
abstract class Drink
```

---

### Inheritance

```ts
extends
```

---

### Composition

```ts
constructor(
  private heater: Heater
)
```

---

## 🔥 Interview Focus

Most Important Topics:

1. Classes
2. Constructors
3. `this` Keyword
4. Public vs Private vs Protected
5. Parameter Properties
6. Readonly Properties
7. Getters & Setters
8. Static Members
9. Abstract Classes
10. Inheritance vs Composition

These are among the most frequently asked TypeScript OOP concepts in frontend, React, Angular, Node.js, and full-stack interviews. :contentReference[oaicite:0]{index=0}