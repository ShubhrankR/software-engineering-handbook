# Execution Context

## Definition

An Execution Context is the environment in which JavaScript code runs. It contains the variables, functions, scope information, and the value of `this` needed to execute a piece of code.

---

## Types

- **Global Execution Context** - Created when a JavaScript file starts running.
- **Function Execution Context** - Created each time a function is invoked.
- **Eval Execution Context** - Created for code run through `eval()`; it is rarely used and generally avoided.

---

## Execution Phases

### Memory Creation Phase

JavaScript prepares the execution context before running code:

- Scans declarations.
- Allocates memory.
- Initializes `var` as `undefined`.
- Leaves `let` and `const` uninitialized.
- Stores function declarations completely in memory.

### Execution Phase

JavaScript then runs the code line by line:

- Updates variable values.
- Invokes functions.
- Creates a Function Execution Context for each function call.
- Pushes and pops contexts on the Call Stack.

---

## Call Stack

The Call Stack tracks which Execution Context is currently executing. The Global Execution Context is placed on the stack first. When a function is called, its Function Execution Context is pushed on top. When that function finishes, its context is popped, and execution resumes in the context below it.

```
Top
| Function Execution Context |
| Global Execution Context   |
Bottom
```

---

## Common Interview Questions

- What is an Execution Context?
- Explain the Memory Creation Phase.
- Explain the Execution Phase.
- What is Hoisting?
- What is the difference between `var` and `let`?
- What is the Temporal Dead Zone (TDZ)?
- Explain the Call Stack.

---

## Common Mistakes

❌ Memory Creation executes code.

✓ It only scans declarations and allocates memory.

---

❌ `let` creates another Execution Context.

✓ `let` is block scoped; it does not create an Execution Context by itself.

---

❌ Hoisting moves variables to the top of the file.

✓ JavaScript scans declarations before execution; it does not physically move code.

---

## Whiteboard Diagram

For:

```js
console.log("A");

function greet() {
    console.log("B");
}

greet();

console.log("C");
```

```
Memory Creation Phase
Global Context:
- greet -> function definition

Execution Phase
1. console.log("A")  -> A
2. greet()           -> push Function Context
3. console.log("B")  -> B
4. greet returns      -> pop Function Context
5. console.log("C")  -> C

Call Stack during greet():

Top
| greet() |
| Global  |
Bottom
```

---

## 2 Minute Interview Answer

An Execution Context is the environment JavaScript creates to run code. It holds the variables, function declarations, scope information, and `this` value needed during execution.

JavaScript creates a Global Execution Context when a file starts, and it creates a new Function Execution Context whenever a function is called. Each context has two phases. In the Memory Creation Phase, JavaScript scans declarations, allocates memory, initializes `var` with `undefined`, leaves `let` and `const` uninitialized in the Temporal Dead Zone, and stores function declarations. In the Execution Phase, it runs code line by line and updates values.

The Call Stack manages these contexts. The global context starts on the stack. Function calls push a new context on top, and completed functions are popped off. This model explains hoisting, the TDZ, and why JavaScript executes synchronous code in a predictable order.

---

## Revision Notes

- Execution Context is the environment in which JavaScript runs code.
- Global Execution Context is created once per script.
- Function Execution Context is created per function invocation.
- `eval()` creates an Eval Execution Context but is rarely used.
- Memory Creation scans declarations and allocates memory.
- `var` is initialized as `undefined`; `let` and `const` remain uninitialized.
- Function declarations are available during Memory Creation.
- Execution Phase runs code line by line.
- The Call Stack pushes function contexts and pops them after completion.
- Hoisting describes declaration handling before execution, not physical code movement.
