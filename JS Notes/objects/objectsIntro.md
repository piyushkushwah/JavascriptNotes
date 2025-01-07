# JavaScript Objects Quick Revision

## 1. **Creating Objects**
Objects can be created using either:
- **Object Literal Syntax** (most common):
  ```javascript
  const user = { firstname: 'Piyush', lastname: 'Kushwaha' };
  ```
- **Constructor Syntax**:
  ```javascript
  const user = new Object({ firstname: 'Piyush', lastname: 'Kushwaha' });
  ```
  
  Both methods create objects, but the literal syntax is preferred for simplicity.

---

## 2. **Property Naming and Access**

### Dot Notation:
- Only supports keys that:
  - Are valid identifiers (e.g., `a-z`, `A-Z`, `_`, `$`, and numbers after the first character).
  - Do not contain special characters or spaces.
- Example:
  ```javascript
  user.firstname = 'Piyush'; // Valid
  user.$age = 20;    // Valid
  user._address = "20, New York"; // Valid
  console.log(user); // { firstname: 'Piyush', lastname: 'Kushwaha', $age: 20, _address: '20, New York' }
  ```

### Square Bracket Notation:
- More flexible as it allows:
  - Multiword property names.
  - Special characters and spaces in keys.
  - Dynamic (computed) property names.
- Example:
  ```javascript
  const multiwordProperty = { "New Year Coupon Code": "20259090" };
  console.log(multiwordProperty["New Year Coupon Code"]); // Accesses value using square brackets
  ```

### Computed Properties:
- Property names can be dynamically computed at runtime.
- Example:
  ```javascript
  const dynamicKey = '2' + '2'; // Key will be '22'
  multiwordProperty[dynamicKey] = 20;
  console.log(multiwordProperty); // { 'New Year Coupon Code': '20259090', '22': 20 }
  ```

---

## 3. **Property Shorthand**
- Shorthand syntax allows you to create object properties where the key name matches the variable name:
  ```javascript
  const apple = 2;
  const bag = { apple }; // Same as { apple: apple }
  console.log(bag); // { apple: 2 }
  ```

---

## 4. **Key Coercion in Objects**
- Keys in objects are always stored as strings (or symbols).
- Numbers or booleans used as keys are coerced into strings.
  ```javascript
  const obj = { 1: 3, true: 23 };
  console.log(obj[1]);     // Accesses "1", coerced from 1
  console.log(obj["true"]); // Accesses "true", coerced from true
  ```

---

## 5. **Using Reserved Keywords and Special Characters**
- Object keys can use reserved keywords, numbers, special characters, or even `null`.
- Example:
  ```javascript
  const obj = {
    $test: 'value',
    null: '',
    "3": 3
  };
  console.log(obj[3]); // Outputs 3 (coerced to "3")
  ```

---

## 6. **Checking Property Existence**

### Using the `in` Operator:
- Checks whether a key exists in an object (including inherited properties).
  ```javascript
  const car = { model: '2025' };
  console.log('model' in car); // true
  ```

### Comparing with `undefined`:
- Checks if a property’s value is `undefined`.
  ```javascript
  const garage = { employee: undefined };
  console.log(garage.employee === undefined); // true
  console.log('employee' in garage); // true (key exists but value is undefined)
  ```
- **Key Difference**: `in` checks for the presence of the property, even if its value is `undefined`.

---

## 7. **Iterating Over Properties**
- Use `for...in` to loop through an object's enumerable properties:
  ```javascript
  const obj = { a: 1, b: 2 };
  for (let key in obj) {
    console.log(key, obj[key]);
  }
  ```
- **Note**: Properties inherited from the prototype chain will also be iterated unless filtered with `hasOwnProperty()`.

---

## 8. **Property Order**
- Property order follows these rules:
  1. Integer keys (e.g., "1", "2") are sorted numerically.
  2. All other keys (non-integer strings) are iterated in creation order.
  ```javascript
  let codes = {
    "49": "Germany",
    "41": "Switzerland",
    "44": "Great Britain",
    "1": "USA"
  };
  console.log(codes); // Outputs: { '1': 'USA', '41': 'Switzerland', '44': 'Great Britain', '49': 'Germany' }
  ```

---

## Summary of Key Features

1. **Object Basics**:
   - Objects store properties as key-value pairs.
   - Keys are strings or symbols; values can be any data type.

2. **Accessing Properties**:
   - **Dot Notation**: Simplified, but restricted to valid identifiers.
   - **Square Bracket Notation**: Allows dynamic, special character, or multiword keys.

3. **Property Manipulation**:
   - Add/Update: `obj.key = value` or `obj["key"] = value`.
   - Delete: `delete obj.key`.
   - Check Existence: `"key" in obj` or `obj.key === undefined`.

4. **Iteration**:
   - Use `for...in` to iterate over enumerable properties.

5. **Key Coercion**:
   - Non-string keys (like numbers and booleans) are coerced to strings.

6. **Special Rules for Property Order**:
   - Integer keys are sorted numerically.
   - Non-integer keys are iterated in creation order.
