
# JavaScript: Pass by Value, Pass by Reference, and Object Handling

This guide explains fundamental JavaScript concepts, including **Pass by Value**, **Pass by Reference**, object comparisons, and cloning techniques.

---

## **1. Pass by Value**

In JavaScript, **primitive data types** (e.g., `number`, `string`, `boolean`, `null`, `undefined`, `symbol`, `bigint`) are passed by value. This means the actual value is copied when assigned to a variable or passed to a function.

### **Example**
```javascript
let originalValue = 42;
let copiedValue = originalValue;

copiedValue = 100;

console.log(originalValue); // Output: 42 (remains unchanged)
console.log(copiedValue);   // Output: 100
```

### **Explanation**
- The values of `originalValue` and `copiedValue` are independent. Modifying one does not affect the other.

---

## **2. Pass by Reference**

**Objects, arrays, and functions** are passed by reference. Instead of copying the object, JavaScript passes the memory location where the object is stored.

### **Example**
```javascript
const user = { name: 'Alice' };
const admin = user;

admin.name = 'Bob';

console.log(user.name); // Output: 'Bob'
```

### **Explanation**
- Both `user` and `admin` reference the same object in memory. Changing `admin.name` also updates `user.name`.

---

## **3. Key Differences: Pass by Value vs. Pass by Reference**

| **Aspect**             | **Pass by Value**                     | **Pass by Reference**                   |
|------------------------|---------------------------------------|-----------------------------------------|
| **Data Types**         | Primitives                           | Objects, arrays, and functions          |
| **What is Copied**     | The actual value                     | The reference (memory address)          |
| **Independence**       | Independent copies                   | Changes affect all references           |

---

## **4. Comparison by Reference**

Objects are compared by their reference, not by their content. Even if two objects have identical properties, they are not equal unless they share the same reference.

### **Example**
```javascript
const obj1 = { key: 'value' };
const obj2 = obj1;
const obj3 = { key: 'value' };

console.log(obj1 === obj2); // true (same reference)
console.log(obj1 === obj3); // false (different references)
```

---

## **5. Shallow Cloning**

Shallow cloning creates a new object or array with the same top-level properties. This can be done using `Object.assign()` or the spread operator (`...`).

### **Example**
```javascript
const original = { name: 'John', age: 30 };
const shallowClone = { ...original };

shallowClone.age = 40;

console.log(original.age);      // Output: 30
console.log(shallowClone.age);  // Output: 40
```

### **Limitation**
- **Shallow cloning** does not create independent copies of nested objects. Changes to nested properties affect the original.

---

## **6. Deep Cloning**

To create a fully independent copy of an object, use **deep cloning** techniques like `structuredClone()` (native) or libraries like Lodash (`_.cloneDeep`).

### **Example**
```javascript
const original = {
  name: 'Dave',
  details: {
    age: 30,
    address: { city: 'New York' },
  },
};

const deepClone = structuredClone(original);

deepClone.details.address.city = 'Los Angeles';

console.log(original.details.address.city); // Output: 'New York'
console.log(deepClone.details.address.city); // Output: 'Los Angeles'
```

---

## **Key Takeaways**

1. **Pass by Value** applies to primitives, and modifications do not affect the original value.
2. **Pass by Reference** applies to objects, arrays, and functions, where changes affect all references.
3. Use **shallow cloning** for simple, top-level properties.
4. Use **deep cloning** for nested objects to avoid shared references.
5. Object equality (`===`) compares references, not values.

---

Feel free to use this as a cheat sheet or guide for working with objects and references in JavaScript! 🚀
