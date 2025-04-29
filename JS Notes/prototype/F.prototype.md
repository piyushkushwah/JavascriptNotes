
# 🔍 JavaScript: `Function.prototype` Explained Simply

In JavaScript, **functions are objects**, and every function has a special property called `.prototype`. This `.prototype` object becomes the **prototype of any object created using that function as a constructor**.

---

## 📦 What Is `Function.prototype`?

When you create a function like this:

```js
function Rabbit() {}
```

JavaScript automatically sets:

```js
Rabbit.prototype = { constructor: Rabbit };
```

This `Rabbit.prototype` object is used when you create a new object with `new Rabbit()`. The new object’s internal `[[Prototype]]` is set to `Rabbit.prototype`.

---

## 🧱 Understanding the Prototype Chain

```js
function Rabbit() {}
let rabbit = new Rabbit();

console.log(Object.getPrototypeOf(rabbit) === Rabbit.prototype); // true
```

- `rabbit` doesn’t have a method? JavaScript checks `Rabbit.prototype` next.

---

## 🛠️ Adding Methods to the Prototype

```js
function Rabbit(name) {
  this.name = name;
}

Rabbit.prototype.sayHi = function() {
  console.log(`Hi, my name is ${this.name}`);
};

const rabbit = new Rabbit("Fluffy");
rabbit.sayHi(); // Hi, my name is Fluffy
```

🔹 All instances of `Rabbit` share the `sayHi` method via the prototype.

---

## 🔄 The `constructor` Property

Every prototype has a `constructor` property pointing to the function itself:

```js
function Rabbit() {}
console.log(Rabbit.prototype.constructor === Rabbit); // true
```

🛑 If you overwrite the whole prototype, this link is broken:

```js
Rabbit.prototype = { jumps: true };
console.log(Rabbit.prototype.constructor === Rabbit); // false
```

✅ Fix it manually if needed:

```js
Rabbit.prototype = {
  jumps: true,
  constructor: Rabbit
};
```

---

## 🧪 Extending `Function.prototype`

You can even add methods to all functions:

```js
Function.prototype.defer = function(ms) {
  setTimeout(this, ms);
};

function sayHello() {
  console.log("Hello!");
}

sayHello.defer(1000); // Logs "Hello!" after 1 second
```

⚠️ Be cautious when modifying `Function.prototype` as it affects all functions globally.

---

## 🧭 Summary

- Every function has a `.prototype` property.
- Objects created with `new` use the function’s `.prototype` as their prototype.
- You can define shared methods and properties on `.prototype`.
- The `.constructor` links the prototype back to the function.
- You can extend `Function.prototype` to add custom methods to all functions (use wisely).

---

📌 Mastering `Function.prototype` and the prototype chain helps you understand **JavaScript inheritance** deeply.
