# Execution Context

## Definition

An **Execution Context** is the environment in which JavaScript code is executed. Every Execution Context contains a **Lexical Environment**, a **Variable Environment**, and a **this Binding**. The `this` binding is important but is intentionally not covered here.

---

## Types of Execution Context

- **Global Execution Context** - Created when a JavaScript file begins execution.
- **Function Execution Context** - Created every time a function is invoked.
- **Eval Execution Context** - Created by `eval()`; it is rarely used and generally avoided.

Blocks do **not** create Execution Contexts.

---

## Execution Phases

### Memory Creation Phase

Before execution begins, JavaScript prepares the current scope:

- Scans the entire scope for declarations.
- Allocates memory for declarations.
- Initializes `var` with `undefined`.
- Allocates `let` and `const`, but leaves them uninitialized.
- Stores function declarations completely in memory.
- Does **not** execute code.

### Execution Phase

JavaScript then executes code line by line:

- Variable assignments happen here.
- Function invocations create new Function Execution Contexts.
- Function Execution Contexts are pushed onto the Call Stack.
- After a function completes, its context is popped from the Call Stack.

---

## Call Stack

The **Call Stack** tracks the order in which Execution Contexts run. The Global Execution Context starts first. Each function call pushes a new Function Execution Context on top of the stack. When the function returns, that context is popped.

```
Global Execution Context
        |
        v
greet()
        |
        v
anotherFunction()
```

The last context pushed is the first context popped.

---

## Lexical Environment

A **Lexical Environment** stores variable bindings and contains a reference to its **Outer Lexical Environment**.

Variable lookup always starts in the current Lexical Environment. If JavaScript cannot find the variable there, it follows the Outer Lexical Environment Reference.

---

## Scope Chain

Consider:

```js
let name = "Shubhrank";

function outer() {
    let age = 30;

    function inner() {
        console.log(name);
        console.log(age);
    }
}
```

When `inner` looks up a variable, JavaScript searches in this order:

```
inner Lexical Environment
        |
        v
outer Lexical Environment
        |
        v
Global Lexical Environment
```

Variable lookup always goes from the current scope outward.

It never searches inward.

---

## Block Scope

Blocks create **Lexical Environments**.

Blocks do **not** create Execution Contexts.

```js
{
    let age = 30;
}
```

`age` cannot be accessed outside the block because its binding exists in the block's Lexical Environment.

That block environment has an Outer Lexical Environment Reference pointing to its enclosing scope.

---

## Hoisting

Hoisting does not physically move declarations to the top of the file.

Instead, the JavaScript engine scans declarations during the Memory Creation Phase before execution begins.

| Declaration | Memory Creation behavior |
| --- | --- |
| `var` | Allocated and initialized with `undefined` |
| `let` | Allocated but uninitialized |
| `const` | Allocated but uninitialized and must be initialized at declaration |
| Function declaration | Stored completely in memory |

---

## Temporal Dead Zone

`let` and `const` are hoisted in the sense that memory is allocated for them during the Memory Creation Phase.

However, they remain uninitialized until execution reaches their declaration.

Accessing them before initialization throws a `ReferenceError`. This period is the **Temporal Dead Zone (TDZ)**.

---

## Common Interview Questions

- What is an Execution Context?
- Explain the Memory Creation Phase.
- Explain the Execution Phase.
- What is Hoisting?
- What is the difference between `var` and `let`?
- What is the TDZ?
- What is a Lexical Environment?
- What is the Scope Chain?
- What is the difference between an Execution Context and a Lexical Environment?
- Do blocks create Execution Contexts?

---

## Common Mistakes

❌ JavaScript executes code during Memory Creation.

✓ Memory Creation only scans declarations and allocates memory.

---

❌ `let` creates another Execution Context.

✓ `let` creates bindings inside a Lexical Environment.

---

❌ Blocks create Execution Contexts.

✓ Blocks create Lexical Environments.

---

❌ Scope lookup works in both directions.

✓ Scope lookup always searches outward.

---

❌ Hoisting moves declarations.

✓ JavaScript scans declarations before execution.

---

## Whiteboard Diagram

```
Global Execution Context
        |
        v
Function Execution Context
        |
        v
Lexical Environments
        |
        v
Outer Lexical Environment References
        |
        v
Global Lexical Environment
```

---

## 2 Minute Interview Answer

An Execution Context is the environment JavaScript creates to run code. It includes a Lexical Environment, a Variable Environment, and a `this` binding. JavaScript creates one Global Execution Context for a script and a new Function Execution Context for every function invocation. Blocks do not create Execution Contexts.

Each context has two phases. In the Memory Creation Phase, JavaScript scans the scope, allocates memory, initializes `var` as `undefined`, leaves `let` and `const` uninitialized, and stores function declarations. No code executes in this phase. In the Execution Phase, JavaScript runs code line by line, assigns values, and creates function contexts as functions are called.

The Call Stack manages those contexts using push and pop behavior. Lexical Environments manage variable lookup. A Lexical Environment stores bindings and points to its outer environment, which creates the Scope Chain. JavaScript always searches from the current scope outward, never inward. This model explains hoisting, block scope, and the Temporal Dead Zone.

---

## Revision Notes

- Execution Context is the environment in which JavaScript runs code.
- Every context contains a Lexical Environment, Variable Environment, and `this` binding.
- Global, Function, and Eval are the Execution Context types.
- `eval()` is rarely used and generally avoided.
- Blocks create Lexical Environments, not Execution Contexts.
- Memory Creation scans declarations and allocates memory.
- `var` becomes `undefined`; `let` and `const` remain uninitialized.
- Function declarations are stored completely before execution.
- Execution Phase runs code line by line.
- Function calls push contexts onto the Call Stack; returns pop them.
- A Lexical Environment stores bindings and references its outer environment.
- Scope Chain lookup starts locally and searches outward only.
- Hoisting is declaration handling before execution, not code movement.
- TDZ is the period before a `let` or `const` declaration is initialized.
- Accessing a `let` or `const` binding in the TDZ throws `ReferenceError`.
