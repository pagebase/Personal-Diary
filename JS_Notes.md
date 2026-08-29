# Table of content

- [Short circuiting](#short-circuiting)
---
# Short circuiting


**1. Logical AND with two truthy values**

```js
console.log("Apple" && "Banana");
// Output: "Banana"
```

> **Why:** The `&&` (AND) operator looks for the first **falsy** value. If the first operand is truthy ("Apple"), it must evaluate and return the second operand ("Banana").


**2. Logical AND with a falsy value**

```js
console.log(0 && "Hello");
// Output: 0
```

> **Why:** Since `0` is falsy, the `&&` operator short-circuits immediately and returns `0`. It completely ignores "Hello".


**3. Logical OR with all falsy values**

```js
console.log("" || false || null);
// Output: null
```

> **Why:** It checks from left to right. Since `""`, `false`, and `null` are all falsy, it reaches the end of the chain and simply returns the very last value (`null`).

**4. Logical AND chain**

```js
console.log(1 && 2 && 3);
// Output: 3
```

> **Why:** It evaluates left to right. Since `1` is truthy, it moves to `2`. Since `2` is truthy, it moves to `3`. Because there are no falsy values to short-circuit on, it returns the final evaluated operand.

**5. Nullish Coalescing (??) with 0**

```js
console.log(0 ?? 45);
// Output: 0
```

> **Why:** The `??` operator only skips `null` and `undefined`. Unlike `||`, it considers `0` to be a perfectly valid value, so it returns `0` and ignores `45`.

**6. Nullish Coalescing (??) with null**

```js
console.log(null ?? "Default");
// Output: "Default"
```

> **Why:** Because the first value is literally `null`, the `??` operator falls back to the right side and returns "Default".

**7. Logical OR with multiple truthy values**

```js
console.log("First" || "Second" || "Third");
// Output: "First"
```

> **Why:** The `||` operator returns the very first truthy value it finds. "First" is truthy, so it stops immediately.


**8. The NaN (Not a Number) falsy case**

```js
console.log(NaN || "Fallback");
// Output: "Fallback"
```

> **Why:** In JavaScript, `NaN` is considered falsy. The `||` operator skips it and returns the truthy string "Fallback".

**9. Undefined in a logical AND**

```js
console.log(undefined && "Test");
// Output: undefined
```

> **Why:** `undefined` is falsy. The `&&` operator stops immediately upon hitting a falsy value and returns it, ignoring "Test".

**10. Mixing AND (&&) and OR (||)**

```js
console.log(0 || "Yes" && "No");
// Output: "No"
```

> **Why:** The `&&` operator has a **higher precedence** than `||`, so it gets evaluated first. `"Yes" && "No"` evaluates to `"No"`. Then, the expression becomes `0 || "No"`. Since `0` is falsy, it returns `"No"`.

---

