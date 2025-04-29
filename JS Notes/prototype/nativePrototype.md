# Native Prototypes in JavaScript

## 🧠 What Are Native Prototypes?

In JavaScript, **native prototypes** refer to built-in objects like `Object`, `Array`, `Function`, `Date`, etc. Each of these has a `prototype` object that contains shared methods and properties for all instances.

---

## 🔗 How Prototypes Work

When you create an object with a constructor, JavaScript sets its internal `[[Prototype]]` (which we can access via `__proto__`) to the constructor's `prototype`. This allows inheritance.

### Example:
```js
let obj = {};
console.log(obj.toString()); // "[object Object]"
```
Even though `obj` is empty, it can use `toString()` because it's inherited from `Object.prototype`.

```js
console.log(obj.__proto__ === Object.prototype); // true
console.log(Object.prototype.__proto__); // null
```

---

## 📚 Built-in Prototypes

Other types like arrays and functions have their own prototypes:

### Array Example:
```js
let arr = [1, 2, 3];
console.log(arr.__proto__ === Array.prototype); // true
```

### Function Example:
```js
function greet() {
  console.log("Hello");
}
console.log(greet.__proto__ === Function.prototype); // true
```

These prototypes provide useful methods like `push()` for arrays or `call()` for functions.

---

## 🛠️ Modifying Native Prototypes (Not Recommended)

You can add your own methods to built-in prototypes, but this is discouraged as it may cause conflicts or bugs.

### Example:
```js
Array.prototype.sayHi = function() {
  console.log("Hi from array");
};

let numbers = [1, 2, 3];
numbers.sayHi(); // "Hi from array"
```

This affects **all arrays** in your app or even in libraries you use.

---

## 🧬 Prototype Chain

The prototype chain is how JavaScript handles inheritance:

- `{}` ➔ inherits from `Object.prototype`
- `[]` ➔ inherits from `Array.prototype` ➔ which inherits from `Object.prototype`
- functions ➔ inherit from `Function.prototype`

This chain allows property and method lookup through the hierarchy.

---

## 🗺️ Summary

- Every object in JS has a hidden `[[Prototype]]`, accessible via `__proto__`.
- Built-in types like `Array`, `Object`, `Function` have their own `prototype`.
- Instances inherit methods from their constructor's prototype.
- Avoid changing built-in prototypes in real projects.

Understanding prototypes helps you master inheritance and method sharing in JavaScript!

