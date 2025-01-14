# Understanding the `new` Keyword and Constructor in JavaScript

## Example 1: Basic Usage of `new`
```javascript
function User() {
    this.name = 'test';
}
const newUser = new User(); // Note: Capitalizing constructor names is a convention, not a requirement.
console.log(newUser); // Output: User { name: 'test' }
```

### Steps When Using `new`
1. A new empty object is created and assigned to `this`.
2. The function body executes, typically modifying `this` and adding properties to it.
3. The value of `this` is returned unless the function explicitly returns another object.

## Example 2: Checking the `new.target` Property
```javascript
function UserTest() {
    console.log(new.target); // `new.target` is undefined when called without `new`.
}

UserTest(); // Output: undefined
let result = new UserTest(); // Output: [Function: UserTest]
console.log(result); // Output: UserTest {}
```

## Example 3: Ensuring Constructor is Called with `new`
```javascript
function User(name) {
    if (!new.target) { // If called without `new`
        return new User(name); // Recursively call with `new`
    }
    this.name = name;
}

let john = User("John"); // Automatically redirects to `new User("John")`
console.log(john); // Output: User { name: 'John' }
```

## Rule of Return

### 1. If `return` is an object, the function will return that object instead of `this`.
```javascript
function GetLastname() {
    this.lastname = 'test';
    return { name: 'test return' };
}
console.log(new GetLastname()); // Output: { name: 'test return' }
```

### 2. If `return` is a primitive value, it is ignored, and `this` is returned.
```javascript
function NumericReturn() {
    this.num = 3;
    return 2; // Ignored because it is a primitive value
}
console.log(new NumericReturn()); // Output: NumericReturn { num: 3 }
```

## Constructor Calls Without Parentheses
```javascript
let constructorA = new User;
let constructorB = new User();
console.log(constructorA, constructorB); // Both are valid
```

## Methods in Constructor
```javascript
function UserWithMethod(name) {
    this.name = name;
    this.sayHi = function() {
        console.log("My name is: " + this.name);
    };
}
let john2 = new UserWithMethod("John");
john2.sayHi(); // Output: My name is: John
```

## Singleton-Like Behavior (Shared Object Reference)
```javascript
const obj = {};
function A() {
    return obj;
}
function B() {
    return A();
}

console.log(new A() === new B()); // Output: true

let a = new A();
let b = new B();
console.log(a === b); // Output: true
```

## Example: Calculator Constructor
```javascript
function Calculator() {
    this.read = function () {
        this.a = 3; // Example hardcoded values instead of prompts
        this.b = 5;
    };

    this.sum = function () {
        return this.a + this.b;
    };

    this.mul = function () {
        return this.a * this.b;
    };
}

let calculator = new Calculator();
calculator.read();
console.log(`SUM = ${calculator.sum()}`); // Output: SUM = 8
console.log(`MUL = ${calculator.mul()}`); // Output: MUL = 15
```

## Example: Accumulator Constructor
```javascript
function Accumulator(startingValue) {
    this.value = startingValue;
    this.read = function () {
        let userValue = 10; // Example hardcoded value instead of prompt
        this.value += userValue;
    };
}

let accumulator = new Accumulator(1); // Initial value: 1
accumulator.read(); // Adds 10
accumulator.read(); // Adds 10
console.log(accumulator.value); // Output: 21
```
