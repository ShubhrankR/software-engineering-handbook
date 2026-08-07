# Scope Chain

## Definition

The **Scope Chain** is the mechanism JavaScript uses to resolve variables. When JavaScript cannot find a variable in the current Lexical Environment, it follows the Outer Lexical Environment Reference until the variable is found or the Global Lexical Environment is reached.

---

## Why do we need Scope Chain?

Consider:

```javascript
let name = "Shubhrank";

function greet() {
    console.log(name);
}

greet();
```

`name` does not exist inside `greet()`.

JavaScript first searches the current Lexical Environment for `greet()`. Since it is not found, JavaScript follows the Outer Lexical Environment Reference to the Global Lexical Environment, where `name` is found.

---

## Variable Lookup Order

Consider:

```javascript
let name = "Shubhrank";

function outer() {
    let age = 30;

    function inner() {
        console.log(name);
        console.log(age);
    }
}
```

Searching for `age`:

```
inner()
  |
  v
outer()
  |
  v
Found
```

Searching for `name`:

```
inner()
  |
  v
outer()
  |
  v
Global
  |
  v
Found
```

JavaScript always searches outward.

It never searches inward.

---

## Block Scope

Consider:

```javascript
{
    let age = 30;
}

console.log(age);
```

Blocks create Lexical Environments.

Variables declared with `let` and `const` are block scoped, so `age` cannot be accessed outside this block.

The Global Lexical Environment cannot search inside child Lexical Environments.

---

## Mental Model

```sql
Global Lexical Environment
        |
        |
        v
Outer Function Lexical Environment
        |
        v
Inner Function Lexical Environment
```

Variable lookup always starts from the current Lexical Environment and walks upward.

---

## Interview Questions

- What is Scope Chain?
- How does JavaScript resolve variables?
- Why can an inner function access outer variables?
- Why can't the outer scope access variables declared inside an inner function?
- What is the difference between Scope Chain and Execution Context?

---

## Common Mistakes

❌ JavaScript searches every scope.

✓ JavaScript only searches the current scope and then outward.

---

❌ Scope lookup works both ways.

✓ Scope lookup only moves outward.

---

❌ Block scopes create Execution Contexts.

✓ Blocks create Lexical Environments only.

---

## 2 Minute Interview Answer

The Scope Chain is the mechanism JavaScript uses to resolve variables. Every Lexical Environment has a reference to its outer Lexical Environment. When JavaScript needs a variable, it first checks the current scope. If the variable is not there, it follows the outer reference and continues searching until it reaches the Global Lexical Environment.

This is why an inner function can access variables declared in an outer function or globally. Its Scope Chain includes those outer environments. The reverse is not true: an outer scope cannot access a variable declared only inside an inner function because lookup never searches inward.

The Scope Chain is about variable resolution. An Execution Context is the broader environment in which code runs; it contains information such as Lexical Environments, the Variable Environment, and the `this` binding.

---

## Revision Notes

- Scope Chain is JavaScript's variable-resolution mechanism.
- Lookup starts in the current Lexical Environment.
- If not found, JavaScript follows the Outer Lexical Environment Reference.
- Lookup continues until the Global Lexical Environment.
- Inner scopes can access outer-scope variables.
- Outer scopes cannot access child-scope variables.
- Lookup always moves outward, never inward.
- Blocks create Lexical Environments, not Execution Contexts.
- `let` and `const` variables are block scoped.
- Scope Chain resolves variables; Execution Context is the environment in which code executes.
