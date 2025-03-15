# JavaScript Promise Chaining
_Last Updated: 18 Dec, 2024_

Promise chaining allows you to execute a series of asynchronous operations in sequence. It is a powerful feature of JavaScript promises that helps you manage multiple operations, making your code more readable and easier to maintain.

- Allows multiple asynchronous operations to run in sequence.
- Reduces callback hell by eliminating deeply nested functions.
- Each `then()` returns a new promise, allowing further chaining.
- Error handling is easier with a single `.catch()` for the entire chain.

## Example of Promise Chaining

```javascript
function task(message, delay) {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log(message);
            resolve();
        }, delay);
    });
}

// Chaining promises
task('Task 1 completed', 1000)
    .then(() => task('Task 2 completed', 2000))
    .then(() => task('Task 3 completed', 1000));
```

### Output:
```
Task 1 completed
Task 2 completed
Task 3 completed
```

In this example:
- `task()` is a function that returns a promise, simulating a delay using `setTimeout`.
- Each task waits for the previous one to complete before executing, thanks to the `.then()` chaining.
- The tasks will execute in order, printing:
  - “Task 1 completed”
  - “Task 2 completed”
  - “Task 3 completed”

This is the core of promise chaining, where each promise is linked to the next one through `.then()`.

## Promise States
A promise in JavaScript can be in one of three states, which determine how it behaves:
- **Pending:** This state represents the initial state of the promise. It is neither fulfilled nor rejected.
- **Fulfilled:** This state represents that the asynchronous operation has successfully completed, and the promise has resolved with a value.
- **Rejected:** This state represents that the asynchronous operation has failed, and the promise has rejected with a reason (error).

## Error Handling in Chaining

```javascript
Promise.resolve(5)
    .then((num) => {
        console.log(`Value: ${num}`);
        throw new Error("Something went wrong!");
    })
    .then((num) => {
        console.log(`This won't run`);
    })
    .catch((error) => {
        console.error(`Error: ${error.message}`);
    });
```

### Output:
```
Value: 5
Error: Something went wrong!
```

## Chaining with Dependent Tasks

```javascript
function fetchUser(userId) {
    return Promise.resolve({ id: userId, name: "GFG" });
}

function fetchOrders(user) {
    return Promise.resolve([{ orderId: 1, userId: user.id }]);
}

fetchUser(101)
    .then((user) => {
        console.log(`User: ${user.name}`);
        return fetchOrders(user);
    })
    .then((orders) => {
        console.log(`Orders: ${orders.length}`);
    })
    .catch((error) => console.error(error));
```

### Output:
```
User: GFG
Orders: 1
```

## Advanced Usage: Parallel and Sequential Tasks in a Chain
You can combine `Promise.all()` with chaining for efficient execution.

```javascript
Promise.all([
    Promise.resolve("Task 1 done"),
    Promise.resolve("Task 2 done")
])
    .then(([result1, result2]) => {
        console.log(result1, result2);
        return Promise.resolve("Final Task done");
    })
    .then((finalResult) => console.log(finalResult))
    .catch((error) => console.error(error));
```

### Output:
```
Task 1 done Task 2 done
Final Task done
```

## Why Use Promise Chaining?
- **Improved Readability:** Makes code cleaner and easier to understand compared to deeply nested callbacks.
- **Error Handling:** Centralized error management with a single `.catch()` for the entire chain.
- **Sequential Execution:** Ensures tasks are executed one after the other, passing results along.
- **Simplifies Dependencies:** Handles tasks that depend on the output of previous asynchronous operations.
- **Enhanced Debugging:** Stack traces in Promise chains are easier to follow compared to callback chains.

## When to Use Promise Chaining?
- **Dependent Async Operations:** When one async task relies on the result of another (e.g., fetching user data, then their orders).
- **Sequential Steps:** For workflows with multiple stages, like data transformation or processing pipelines.
- **Avoiding Callback Hell:** To keep the structure of async code flat and maintainable.
- **Error Propagation:** When you need to ensure that an error in any step is caught and handled.
- **Data Aggregation:** Combining results from multiple async calls in sequence.
- **Cleanup After Tasks:** Using `.finally()` to execute code regardless of success or failure.