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
```
After execution, the family object looks like this:
```javascript
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
```

Removing References:

To demonstrate how reachability affects garbage collection, we can remove references to the father and husband:

Remove references from family and mother object
```javascript
delete family.father;
delete family.mother.husband;
```

Now, redefine family to only include mother
```javascript
family = {
    mother: {
        name: 'Ann'
    }
};
```

## Conclusion

After removing the references to father and mother.husband, these objects are now unreachable.
As a result, they become eligible for garbage collection.
The garbage collector will eventually reclaim the memory used by these unreachable objects, keeping the memory usage efficient.

# Mark-and-Sweep Garbage Collection

The **mark-and-sweep** algorithm is a way for JavaScript to clean up memory by removing objects that are no longer needed. It has two main steps: **marking** and **sweeping**.

## Steps of the Mark-and-Sweep Algorithm

### 1. Mark Phase
- **Start with Roots**: The garbage collector begins with root objects, like global variables and active functions.
- **Mark Reachable Objects**: It looks at everything that can be reached from these roots and marks those objects as "in use."

### 2. Sweep Phase
- **Scan All Objects**: After marking, the collector goes through all objects in memory.
- **Collect Unreachable Objects**: Any object that wasn’t marked is considered unreachable and is cleaned up, freeing its memory.

### 3. Resetting Marks
- Once the sweep is done, all marks are reset for the next time garbage collection runs.

## Example Workflow
1. **Identify Roots**: Start with the main variables and active functions.
2. **Mark**: Mark all reachable objects from these roots.
3. **Sweep**: Remove any objects that were not marked.

## Benefits
- **Easy to Understand**: The algorithm is simple and effective for finding unused memory.
- **Cleans Up Unreachable Objects**: It helps prevent memory leaks by getting rid of objects that are no longer needed.

## Limitations
- **Pause in Execution**: During garbage collection, the program may temporarily pause.
- **Fragmented Memory**: This method can sometimes leave small gaps in memory, making it less efficient.

## Conclusion
The mark-and-sweep algorithm is an important part of how JavaScript manages memory, helping to keep applications running smoothly by cleaning up unused objects.

