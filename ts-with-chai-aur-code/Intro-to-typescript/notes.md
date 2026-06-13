# Lecture 1 - Introduction to TypeScript

## What is TypeScript?

TypeScript is a superset of JavaScript that adds static typing.

TypeScript = JavaScript + Types

---

## Why TypeScript?

JavaScript allows any type of value:

```js
function greet(name) {
  return `Hello ${name}`;
}

greet("Rajat"); // Valid
greet(42);      // Also valid ❌
greet(true);    // Also valid ❌
```

TypeScript prevents such issues using type checking.

---

## TypeScript Example

```ts
function greet(name: string): string {
  return `Hello ${name}`;
}

greet("Rajat"); // ✅
greet(42);      // ❌ Error
greet(true);    // ❌ Error
```

---

## When to Learn TypeScript?

Learn TypeScript after JavaScript.

Recommended Order:

JavaScript → TypeScript → React/Next.js

---

## Relationship Between JavaScript and TypeScript

TypeScript is a superset of JavaScript.

Every valid JavaScript code is generally valid TypeScript code.

---

## Core Feature

Type Checking

```ts
let username: string = "Rajat";

username = 123; // ❌ Error
```

---

## TypeScript Compilation

```text
TypeScript (.ts)
        ↓
   Compiler
        ↓
JavaScript (.js)
```

TypeScript does not run directly.

JavaScript is executed in the browser or Node.js.

---

## Benefits of TypeScript

- Type Safety
- Early Error Detection
- Better IDE Support
- Better Maintainability
- Better Scalability
- Better Team Collaboration

---

## Interview Questions

### What is TypeScript?

TypeScript is a statically typed superset of JavaScript.

### Why use TypeScript?

To catch errors during development and improve code maintainability.

### Does TypeScript run directly?

No. TypeScript is compiled into JavaScript.

### What is the biggest feature of TypeScript?

Static Type Checking.

### Is TypeScript a replacement for JavaScript?

No. TypeScript is built on top of JavaScript.