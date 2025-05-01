# JavaScript Variable Naming Rules & Best Practices

## ✅ Naming Rules

1. **Variable names must start with**:
   - A letter: `a-z` or `A-Z`
   - An underscore: `_`
   - A dollar sign: `$`

   ✅ Examples:
   ```javascript
   let name = 'John';
   let _value = 10;
   let $count = 5;
   ```

2. **Subsequent characters can include**:
   - Letters
   - Digits `0–9`
   - Underscores `_`
   - Dollar signs `$`

   ✅ Valid:
   ```javascript
   let user2 = 'Alex';
   let $total_Amount = 100;
   ```

3. ❌ **Cannot start with a number**:
   ```javascript
   let 3years = 3; // ❌ SyntaxError
   ```

4. ❌ **Cannot use JavaScript reserved keywords** as variable names:
   - Examples of reserved keywords: `let`, `const`, `function`, `class`, `if`, etc.
   ```javascript
   let let = 5; // ❌ Invalid
   ```

5. ✅ **Variable names are case-sensitive**:
   ```javascript
   let myVar = 1;
   let myvar = 2; // Both are separate variables
   ```

---

## 🟡 Naming Conventions & Best Practices

1. ✅ **Use meaningful variable names**:
   ```javascript
   let userAge = 25; // 👍 Good
   let x = 25;       // 👎 Bad
   ```

2. ✅ **Use camelCase** for variables and functions (recommended style):
   ```javascript
   let firstName = 'John';
   function calculateTotal() {}
   ```

3. ✅ **Use UPPERCASE with underscores for constants**:
   ```javascript
   const MAX_USERS = 100;
   const API_KEY = 'your-key-here';
   ```

4. ⚠️ **Avoid using global objects like `name`** as variable names:
   - `name` is not a reserved keyword but is a predefined global property (e.g., `window.name`).

5. ✅ **Using `$` and `_`**:
   - `$`: Often used in libraries like jQuery (`$element`)
   - `_`: Common for internal/private variables

---

## 🔥 Additional Tips

- ❌ Avoid vague or short names like `x`, `y` (unless in limited scope):
  ```javascript
  let i = 0; // ok in loops
  ```

- ✅ Use consistent naming patterns for related variables:
  ```javascript
  let userName, userEmail, userPassword;
  ```

- ✅ Prefer `const` for constants, use `let` only when reassignment is required:
  ```javascript
  const PI = 3.14;
  let score = 0;
  ```

- ❌ Avoid re-declaring variables in the same scope to prevent logic bugs.
   - 🔴 Bad Example: Re-declaration in the same scope
      ```javascript
         let count = 5;
         let count = 10; // ❌ SyntaxError: Identifier 'count' has already been declared
      ```
   - ⚠️ Subtle Bug Example with var
     ```javascript
         var user = "Alice";
         var user = "Bob"; // ✅ No error, but logic bug potential
         console.log(user); // "Bob"
      ```
   - ✅ Good Practice
     ```javascript
        let count = 5;
        count = 10; //✅ just update the value, don't re-declare
      ```
     
---

## ✅ Summary Table

| Rule | Description | Example |
|------|-------------|---------|
| ✅ Starts with `a-z`, `_`, or `$` | Valid | `let _x = 1;` |
| ❌ Starts with digit | Invalid | `let 1value = 10;` |
| ❌ Reserved keyword | Invalid | `let const = 5;` |
| ✅ Case-sensitive | `myVar` ≠ `myvar` | `let myVar = 1; let myvar = 2;` |
| ✅ Constants uppercase | Best practice | `const MAX_LIMIT = 100;` |
