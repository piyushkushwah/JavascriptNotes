# 🧠 JavaScript Primitive Data Types (Overview)

JavaScript has **7 primitive data types**. These are **immutable** (cannot be altered) and are **passed by value**. JavaScript is **dynamically typed**, meaning variables can hold any type and change over time.

---

## 1. Number
- Represents both **integers** and **floating-point numbers**.
- Examples:
  ```javascript
  let age = 25;
  let price = 99.99;
  ```
- Special numeric values:
  - `NaN` (Not a Number)
  - `Infinity`, `-Infinity`

---

## 2. String
- Sequence of characters, enclosed in **single ('')**, **double ("")**, or **template literals (``)**.
- Examples:
  ```javascript
  let name = "Alice";
  let greeting = 'Hello';
  let message = `Welcome, ${name}`;
  ```

---

## 3. Boolean
- Logical type representing **true** or **false**.
- Used in conditional logic.
  ```javascript
  let isLoggedIn = true;
  let isAdult = false;
  ```

---

## 4. Undefined
- A variable that has been declared but **not assigned a value**.
  ```javascript
  let child;
  console.log(child); // undefined
  ```

---

## 5. Null
- Represents **explicitly no value** (intentional empty).
  ```javascript
  let data = null;
  ```
> ✅ `typeof null` returns `"object"` – this is a known historical quirk in JavaScript.

---

## 6. Symbol
- Introduced in ES6.
- Represents a **unique and immutable value**, often used as object keys to avoid name conflicts.
  ```javascript
  const sym1 = Symbol('id');
  const sym2 = Symbol('id');
  console.log(sym1 === sym2); // false
  ```

---

## 7. BigInt
- Used for numbers **larger than the `Number` type can safely handle** (i.e., > 2⁵³ - 1).
  ```javascript
  const big = 1234567890123456789012345678901234567890n;
  ```

---

## 🔑 Additional Key Points
- **Primitive types are stored in the stack**, not heap.
- All primitive values are **immutable** (their value cannot be changed).
- **Type of check**:
  ```javascript
  typeof "hello"  // "string"
  typeof 123       // "number"
  typeof true      // "boolean"
  typeof undefined // "undefined"
  typeof null      // "object" ❗ (known bug)
  typeof Symbol()  // "symbol"
  typeof 10n       // "bigint"
  ```
