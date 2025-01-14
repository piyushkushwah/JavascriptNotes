
# JavaScript Optional Chaining (`?.`) Cheat Sheet

Optional chaining (`?.`) is a safe way to access nested properties or methods of an object without worrying about `null` or `undefined` errors.

---

## **1. Accessing Properties Safely**
```javascript
const payments = {
    cash: '300'
};

console.log(payments.cash?.value?.test); // Output: undefined
```
- If `cash` or `value` is `undefined` or `null`, the expression short-circuits and returns `undefined`.

---

## **2. Short-Circuiting**
```javascript
const user = null;

console.log(user?.sayHi()); // Output: undefined
```
- If `user` is `null` or `undefined`, `sayHi()` is not called, avoiding runtime errors.

---

## **3. Optional Chaining with Methods**
```javascript
let userAdmin = {
    admin() {
        console.log("I am admin");
    }
};

let userGuest = {};

userAdmin.admin?.(); // Output: I am admin
userGuest.admin?.(); // Output: undefined (no error)
```
- Use `?.()` to call a method only if it exists.

---

## **4. Optional Chaining with Dynamic Properties**
```javascript
let key = "firstName";

let user1 = {
    firstName: "John"
};

let user2 = null;

console.log(user1?.[key]); // Output: John
console.log(user2?.[key]); // Output: undefined
```
- Use `?.[]` for dynamic property access when the key is stored in a variable.

---

## **5. Using Optional Chaining with `delete`**
```javascript
delete user2?.admin; // No error, even if user2 is null or undefined
```

---

## **6. Invalid Use Cases for Optional Chaining**
- Optional chaining cannot be used on the **left-hand side** of an assignment.
```javascript
user2?.admin = 'John'; // SyntaxError: Invalid left-hand side in assignment
```

---

## **Key Benefits**
- Avoids errors like `Cannot read property 'x' of undefined`.
- Makes code cleaner and reduces the need for nested `if` checks.

---

## **Additional Notes**
1. **Works with Arrays**:
   ```javascript
   const arr = null;
   console.log(arr?.[0]); // Output: undefined
   ```

2. **Alternative Syntax**:
   - Without optional chaining:
     ```javascript
     if (user && user.sayHi) {
         user.sayHi();
     }
     ```
   - With optional chaining:
     ```javascript
     user?.sayHi();
     ```

3. **Performance**:
   - Slightly slower than direct property access due to the safety checks but negligible for most use cases.
