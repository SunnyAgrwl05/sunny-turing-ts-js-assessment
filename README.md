# JavaScript & TypeScript Assessment — Detailed Questions, Answers & Solutions

Detailed study notes for the JavaScript/TypeScript assessment questions reviewed in this conversation.

## Q2 — JSON Serialization and Object Copying

**Correct Answer:** Use a shallow copy such as `Object.assign({}, obj)` when the goal is to avoid JSON serialization losses.

`JSON.parse(JSON.stringify(obj))` is not a general-purpose cloning method. `Date` becomes an ISO string, `undefined` object properties are omitted, `Infinity` becomes `null`, and `RegExp` is not preserved as a `RegExp` instance. `Object.assign()` performs a shallow copy without these JSON conversions.

```js
const clone = Object.assign({}, customerRide);
```

## Q3 — Delete a Customer by ID

**Correct Answer:** `findIndex, ===, splice`

```js
function deleteCustomerById(customers, value) {
  const index = customers.findIndex(
    (customer) => customer.id === value
  );

  if (index > -1) customers.splice(index, 1);
  return customers;
}
```

`findIndex()` finds the matching index, `===` compares value and type strictly, and `splice()` removes the element.

## Q4 — Flatten Nested Sensor Readings

**Correct Answer:** `const flatArray = sensorReading.flat(5);`

```js
const flatArray = sensorReading.flat(5);
const mapped = flatArray.map((temperature) => temperature * 2);
```

`flat(depth)` recursively flattens nested arrays up to the specified depth. The assessment's nesting requires depth 5.

## Q5 — Debouncing vs Throttling

**Correct Answer:** Debouncing waits until an event stops firing for a specified period; throttling allows execution at controlled intervals while the event continues.

- **Debounce:** wait for inactivity. Common example: search input/API calls.
- **Throttle:** limit execution frequency. Common example: scroll/resize handlers.

## Q6 — Array Indexing and Custom Properties

**Correct Answer:** The `-1` property is not an array element.

```js
customerRide[-1] = { /* ... */ };
```

creates an ordinary property named `"-1"`. It does not increase `length` and is not visited by `for...of`.

If the real indexed elements are `5.658` and `6931`, the sum is:

```text
5.658 + 6931 = 6936.658
```

## Q7 — Remove an Object Property

**Correct Answer:**

```js
const { isSelected: _, ...newObj } = bankAccount;
```

Destructuring extracts `isSelected`; the rest operator collects every other property into `newObj` without mutating the original object.

## Q8 — Why Check for `null`?

**Correct Answer:** Checking for `null` helps prevent invalid operations/calculations that can lead to unexpected results such as `NaN`.

```js
if (value !== null) {
  // perform calculation
}
```

For an actual `NaN` check, use `Number.isNaN(value)`.

## Q9 — Preserving the Original Error

**Correct Answer:** Use the standard `cause` option.

```js
throw new Error("Method: Server", {
  cause: error
});
```

The original error is then available through:

```js
exception.cause
```

This is the standard error-chaining mechanism instead of inventing custom properties.

## Q10 — `call()`, `bind()`, and `apply()`

**Correct Answer:**

- `call()` — invokes immediately; arguments are passed individually.
- `apply()` — invokes immediately; arguments are passed as an array/array-like value.
- `bind()` — does not invoke immediately; returns a new function with `this` bound.

```js
fn.call(obj, arg1, arg2);
fn.apply(obj, [arg1, arg2]);
const bound = fn.bind(obj);
bound();
```

## Q11 — `Object.freeze()` and Strict Mode

**Correct Answer:** Add `"use strict"`.

```js
"use strict";

const account = { balance: 5000 };
Object.freeze(account);
account.balance = 10000; // TypeError in strict mode
```

A frozen object's properties cannot be changed. In strict mode, an attempted invalid mutation throws `TypeError` rather than silently failing.

## Q12 — TypeScript Generics

**Correct Answer:** **Error**

```ts
const turingQueue = new TuringQueue<number>();

turingQueue.push(0);   // Valid
turingQueue.push("1"); // TypeScript error
```

`TuringQueue<number>` means the queue accepts numbers. The string `"1"` violates the generic type and is rejected at compile time.

# Quick Answer Key

| Q | Answer |
|---|---|
| Q2 | `Object.assign()` / avoid JSON serialization losses |
| Q3 | `findIndex, ===, splice` |
| Q4 | `sensorReading.flat(5)` |
| Q5 | Debounce waits; throttle limits frequency |
| Q6 | `-1` is a custom property, not an array element |
| Q7 | Object destructuring + rest operator |
| Q8 | Null checking helps avoid invalid/`NaN` results |
| Q9 | `Error(..., { cause: error })` + `exception.cause` |
| Q10 | `call()` / `bind()` / `apply()` semantics |
| Q11 | `"use strict"` with `Object.freeze()` |
| Q12 | TypeScript compile-time type error |

# Topics Covered

JSON serialization, `Object.assign()`, `findIndex()`, strict equality, `splice()`, `flat()`, debouncing, throttling, array properties, destructuring, rest syntax, null handling, `NaN`, error chaining, `call()`, `bind()`, `apply()`, `Object.freeze()`, strict mode, TypeScript generics, and compile-time type checking.
