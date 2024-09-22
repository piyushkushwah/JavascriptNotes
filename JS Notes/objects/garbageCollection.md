# Garbage Collection in JavaScript

## 1. Main Concept: Reachability
The core principle of memory management in JavaScript is **reachability**. An object is considered reachable if there is a reference to it from another object or a global context. If no references to an object exist, it becomes unreachable and can be collected by the garbage collector.

## 2. Automatic Memory Management
In JavaScript, memory allocation and deallocation occur automatically. Developers do not need to manually manage memory, as the garbage collector takes care of reclaiming unused memory.

## 3. Garbage Collection Algorithm
JavaScript primarily uses the **mark-and-sweep** algorithm for garbage collection:
- **Mark**: The garbage collector traverses objects starting from root objects (like global variables) and marks all reachable objects.
- **Sweep**: It then scans through all objects and collects those that are not marked (i.e., unreachable).

## Example: Demonstrating Reachability

Consider the following function that creates a family structure:

```javascript
function marry(man, woman) {
    man.wife = woman;   // man references woman
    woman.husband = man; // woman references man

    return {
        father: man,
        mother: woman
    };
}

var family = marry(
    { name: 'John' }, 
    { name: 'Ann' }
);

After execution, the family object looks like this:

family = {
    father: {
        name: 'John',
        wife: {
            name: 'Ann'
        }
    },
    mother: {
        name: 'Ann',
        husband: {
            name: 'John'
        }
    }
};

Removing References:

To demonstrate how reachability affects garbage collection, we can remove references to the father and husband:


// Remove references from family and mother object
delete family.father;
delete family.mother.husband;

// Now, redefine family to only include mother
family = {
    mother: {
        name: 'Ann'
    }
};

Conclusion

After removing the references to father and mother.husband, these objects are now unreachable. As a result, they become eligible for garbage collection. The garbage collector will eventually reclaim the memory used by these unreachable objects, keeping the memory usage efficient.
