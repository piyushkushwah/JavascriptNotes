
# JavaScript Symbols Cheat Sheet

**Symbols** are unique and immutable primitive values often used as unique keys for object properties. They are created using the `Symbol()` function.

---

## **Key Points and Usage**

### **1. Creating Symbols**
```javascript
const id1 = Symbol("id");
const id2 = Symbol("id");

console.log(id1 === id2); // false, each Symbol is unique
```

- Each symbol is unique, even if it has the same description.

---

### **2. Symbols Cannot Be Automatically Converted to Strings**
```javascript
const id = Symbol("id");

// console.log(id); // TypeError: Cannot convert a Symbol to a string
console.log(id.toString()); // "Symbol(id)"
console.log(id.description); // "id" (description of the symbol)
```

---

### **3. Using Symbols as Object Keys**
```javascript
const user = { name: 'John' };
const userId = Symbol("id");

user[userId] = "30";

console.log(user[userId]); // "30"
```

- **Advantage**: Prevents property name collisions in objects.

---

### **4. Symbols in Object Literals**
```javascript
const carId = Symbol("id");
const car = {
    value: 200,
    [carId]: "Ford"
};

console.log(car[carId]); // "Ford"
```

---

### **5. Symbols in Loops and Object Methods**
- Symbols are **ignored** by:
  - `for...in`
  - `Object.keys()`
  - `Object.entries()`

Example:
```javascript
const carId = Symbol("id");
const car = { value: 200, [carId]: "Ford" };

console.log(Object.keys(car)); // ["value"]
for (let key in car) {
    console.log(key); // Only logs "value"
}
```

- Use `Object.getOwnPropertySymbols()` to retrieve symbols:
```javascript
console.log(Object.getOwnPropertySymbols(car)); // [Symbol(id)]
```

---

### **6. Copying Symbols**
- `Object.assign()` includes symbols:
```javascript
const source = { [Symbol("id")]: "123" };
const target = Object.assign({}, source);

console.log(Object.getOwnPropertySymbols(target)); // [Symbol(id)]
```

---

### **7. Global Symbols**
- Symbols can be registered globally using `Symbol.for()`. This ensures reusability across the code.
```javascript
const id1 = Symbol.for("id");
const id2 = Symbol.for("id");

console.log(id1 === id2); // true (both refer to the same global symbol)
```

---

### **8. Retrieving Symbol Keys**
- Use `Symbol.keyFor()` to get the description of global symbols:
```javascript
const sym = Symbol.for("name");

console.log(Symbol.keyFor(sym)); // "name"
```

---

## **Use Cases**
1. **Unique Property Keys**: Prevent accidental overrides in large projects or libraries.
2. **Hidden Properties**: Create properties not exposed in `for...in` or `Object.keys()`.
3. **Global Symbols**: Share symbols across different parts of the code using `Symbol.for()`.

---

## **Best Practices**
- Use descriptive names for symbols for better debugging.
- Avoid overusing symbols unless necessary, as they add complexity to code.
