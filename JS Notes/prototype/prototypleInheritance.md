
# 📘 JavaScript: Prototypal Inheritance

In JavaScript, prototypal inheritance allows objects to inherit properties and methods from other objects. This is especially useful when you want to create new objects based on existing ones without duplicating code.

---

## 🧠 Concept Overview

Imagine you have a base object `user`, and you want to create `admin` and `guest` objects with some modifications. Instead of rewriting everything, you can build these new objects on top of the `user` using prototypal inheritance.

```js
const user = {
  isHuman: true,
  greet() {
    console.log("Hello!");
  }
};

const admin = Object.create(user);
admin.role = "admin";

admin.greet(); // "Hello!" – inherited from user
```

---

## 🛠️ What Is `[[Prototype]]`?

- Every object in JavaScript has an internal hidden property called `[[Prototype]]`.
- If a property or method is not found in the object, JavaScript automatically looks it up in its prototype.

---

## ⚠️ Limitations of Prototype Chains

1. **No circular references**: You cannot create circular prototype chains. It will throw an error.
2. **Must be object or null**: `__proto__` can only be assigned to an object or `null`. Other types are ignored.

```js
const a = {};
a.__proto__ = a; // ❌ Error: Circular reference
```

---

## 🧾 `__proto__` vs `[[Prototype]]`

- `__proto__` is a historical getter/setter for accessing or modifying `[[Prototype]]`.
- Modern JavaScript prefers:
  - `Object.getPrototypeOf(obj)`
  - `Object.setPrototypeOf(obj, prototype)`

```js
Object.getPrototypeOf(admin); // returns user object
Object.setPrototypeOf(admin, null); // breaks the link
```

> 💡 Although `__proto__` is widely supported, it's recommended to use the modern functions above in production code.

---

## ✍️ Property Writing and Deletion

> **Writing does not use the prototype chain.**  
If a property is written (assigned), it is added directly to the object — not to its prototype.

```js
admin.isHuman = false;
console.log(admin.isHuman); // false
console.log(user.isHuman);  // true (unchanged)
```

---

## 🧭 `this` Keyword in Inherited Methods

- When calling a method, `this` always refers to the object **before the dot**, regardless of where the method is defined.

```js
const user = {
  sayHi() {
    console.log(this.name);
  }
};

const guest = {
  __proto__: user,
  name: "Guest"
};

guest.sayHi(); // "Guest"
```

---

## 🔁 `for...in` Loop and Inherited Properties

- The `for...in` loop **includes** enumerable inherited properties.

```js
for (let key in admin) {
  console.log(key); // includes inherited keys if enumerable
}
```

- Built-in prototype properties like `hasOwnProperty` don't appear because they are non-enumerable.

---

## 🔑 Object Key/Value Methods

Most key/value-related methods **ignore inherited properties**:

```js
Object.keys(admin);    // only own enumerable keys
Object.values(admin);  // only own enumerable values
```

---

## 📌 Summary

- All objects have a hidden `[[Prototype]]` which links to another object or `null`.
- Use `Object.create(obj)` to create a new object with `obj` as its prototype.
- Use `Object.getPrototypeOf()` and `Object.setPrototypeOf()` to access/set prototypes safely.
- Property lookups traverse the prototype chain, but writes do not.
- In method calls, `this` always refers to the actual calling object.
- `for...in` includes inherited properties (if enumerable), while `Object.keys/values/entries()` do not.

---

## 📎 Bonus Example

```js
const animal = {
  eats: true
};

const rabbit = Object.create(animal);
rabbit.hops = true;

console.log(rabbit.eats); // true (from prototype)
console.log(rabbit.hops); // true (own property)
```
