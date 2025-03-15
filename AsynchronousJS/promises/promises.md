# JavaScript Promise

**Last Updated: 18 Jan, 2025**

JavaScript Promises make handling asynchronous operations like API calls, file loading, or time delays easier. Think of a Promise as a placeholder for a value that will be available in the future. It can be in one of three states:

- **Pending**: The task is in the initial state.
- **Fulfilled**: The task was completed successfully, and the result is available.
- **Rejected**: The task failed, and an error is provided.

## Example Promise
Here is an example Promise to check if a number is even. If yes, it resolves; otherwise, it rejects.

```javascript
let checkEven = new Promise((resolve, reject) => {
    let number = 4;
    if (number % 2 === 0) resolve("The number is even!");
    else reject("The number is odd!");
});

checkEven
    .then((message) => console.log(message)) // On success
    .catch((error) => console.error(error)); // On failure
```

**Note**: The `resolve` and `reject` are not keywords. You can use any name that you want to give to a function.

## Syntax

```javascript
let promise = new Promise((resolve, reject) => {
    // Perform async operation
    if (operationSuccessful) {
        resolve("Task successful");
    } else {
        reject("Task failed");
    }
});
```

- `resolve(value)`: Marks the promise as fulfilled and provides a result.
- `reject(error)`: Marks the promise as rejected with an error.

## Advanced Promise Methods and Patterns for Effective Async Handling

### 1. `Promise.all()` Method
Waits for all promises to resolve and returns their results as an array. If any promise is rejected, it immediately rejects.

```javascript
Promise.all([
    Promise.resolve("Task 1 completed"),
    Promise.resolve("Task 2 completed"),
    Promise.reject("Task 3 failed")
])
    .then((results) => console.log(results))
    .catch((error) => console.error(error));
```

**Output**
```
Task 3 failed
```

### 2. `Promise.allSettled()` Method
Waits for all promises to settle (fulfilled or rejected) and returns an array of their outcomes.

```javascript
Promise.allSettled([
    Promise.resolve("Task 1 completed"),
    Promise.reject("Task 2 failed"),
    Promise.resolve("Task 3 completed")
])
    .then((results) => console.log(results));
```

**Output**
```
[
  { status: 'fulfilled', value: 'Task 1 completed' },
  { status: 'rejected', reason: 'Task 2 failed' },
  { status: 'fulfilled', value: 'Task 3 completed' }
]
```

### 3. `Promise.race()` Method
Resolves or rejects as soon as the first promise settles.

```javascript
Promise.race([
    new Promise((resolve) => setTimeout(() => resolve("Task 1 finished"), 1000)),
    new Promise((resolve) => setTimeout(() => resolve("Task 2 finished"), 500)),
])
    .then((result) => console.log(result));
```

**Output**
```
Task 2 finished
```

### 4. `Promise.any()` Method
Resolves with the first fulfilled promise. If all are rejected, it rejects with an `AggregateError`.

```javascript
Promise.any([
    Promise.reject("Task 1 failed"),
    Promise.resolve("Task 2 completed"),
    Promise.resolve("Task 3 completed")
])
    .then((result) => console.log(result))
    .catch((error) => console.error(error));
```

**Output**
```
Task 2 completed
```

### 5. `Promise.resolve()` Method
Returns a promise that resolves with the given value.

```javascript
Promise.resolve("Immediate success")
    .then((value) => console.log(value));
```

**Output**
```
Immediate success
```

### 6. `Promise.reject()` Method
Returns a promise that immediately rejects with a given reason.

```javascript
Promise.reject("Immediate failure")
    .catch((error) => console.error(error));
```

**Output:**
```
Immediate failure
```

### 7. `Promise.finally()` Method
Runs a cleanup or final code block regardless of the promise’s result.

```javascript
Promise.resolve("Task completed")
    .then((result) => console.log(result))
    .catch((error) => console.error(error))
    .finally(() => console.log("Cleanup completed"));
```

**Output**
```
Task completed
Cleanup completed
```

### 8. Chaining with `Promise.prototype.then()` Method
Allows sequential execution of promises, passing results to the next `.then()` method.

```javascript
Promise.resolve(5)
    .then((value) => value * 2) // Multiplies by 2
    .then((value) => value + 3) // Adds 3
    .then((finalValue) => console.log(finalValue)); // Logs: 13
```

**Output**
```
13
```

### 9. Sequential Execution with `Array.prototype.reduce()`

```javascript
let tasks = [1, 2, 3];
tasks.reduce((prevPromise, current) => {
    return prevPromise.then(() => {
        return new Promise((resolve) => {
            console.log(`Processing task ${current}`);
            setTimeout(resolve, 500); // Simulate async task
        });
    });
}, Promise.resolve());
```

**Output**
```
Processing task 1
Processing task 2
Processing task 3
```

### 10. Dynamic Promise Creation
Creating and resolving promises dynamically for runtime-based decisions.

```javascript
function asyncTask(taskName) {
    return new Promise((resolve) => {
        setTimeout(() => resolve(`${taskName} completed`), 1000);
    });
}
asyncTask("Download File").then((result) => console.log(result));
```

**Output:**
```
Download File completed
```

## Benefits of Promises
- **Avoid Callback Hell**: Promises organize asynchronous code more neatly than nested callbacks.
- **Error Handling**: Errors can be caught in one place using `.catch()` method.
- **Chaining**: Perform tasks sequentially with `.then()` method.

By leveraging Promises effectively, large JavaScript applications can handle complex asynchronous tasks efficiently and maintain readable, maintainable code.
