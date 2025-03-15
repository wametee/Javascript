# Async and Await in JavaScript

_Last Updated : 12 Dec, 2024_

Async and Await in JavaScript is used to simplify handling asynchronous operations using promises. By enabling asynchronous code to appear synchronous, they enhance code readability and make it easier to manage complex asynchronous flows.

```javascript
async function fetchData() {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
  const data = await response.json();
  console.log(data);
}

fetchData();
```

**Output:**

```json
{
  userId: 1,
  id: 1,
  title: '...',
  body: '...'
}
```

## Syntax:

```javascript
async function functionName() {
  try {
    const result = await someAsyncFunction();
    console.log(result);
  } catch (error) {
    console.error("Error:", error.message);
  }
}
```

### Async Function

The async function allows us to write promise-based code as if it were synchronous. This ensures that the execution thread is not blocked. Async functions always return a promise. If a value is returned that is not a promise, JavaScript automatically wraps it in a resolved promise.

**Syntax:**

```javascript
async function myFunction() {
  return "Hello";
}

const getData = async () => {
    let data = "Hello World";
    return data;
}

getData().then(data => console.log(data));
```

**Output:**

```
Hello World
```

### Await Keyword

The await keyword is used to wait for a promise to resolve. It can only be used within an async block. Await makes the code wait until the promise returns a result, allowing for cleaner and more manageable asynchronous code.

```javascript
const getData = async () => {
    let y = await "Hello World";
    console.log(y);
}

console.log(1);
getData();
console.log(2);
```

**Output:**

```
1
2
Hello World
```

### Key Points

- The `async` keyword transforms a regular JavaScript function into an asynchronous function, causing it to return a Promise.
- The `await` keyword is used inside an async function to pause its execution and wait for a Promise to resolve before continuing.

### Error Handling in Async/Await

JavaScript provides predefined arguments for handling promises: `resolve` and `reject`.

- `resolve`: Used when an asynchronous task is completed successfully.
- `reject`: Used when an asynchronous task fails, providing the reason for failure.

```javascript
async function fetchData() {
  try {
    let response = await fetch('https://api.example.com/data');
    let data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}
```

## Advantages of Async and Await

- **Improved Readability**: Async and Await allow asynchronous code to be written in a synchronous style, making it easier to read and understand.
- **Error Handling**: Using try/catch blocks with async/await simplifies error handling.
- **Avoids Callback Hell**: Async and Await prevent nested callbacks and complex promise chains, making the code more linear and readable.
- **Better Debugging**: Debugging async/await code is more intuitive since it behaves similarly to synchronous code.

## Async and Await in JavaScript - FAQ’s

**What does async do?**

Marks a function to always return a Promise.

**What does await do?**

Pauses the execution of the async function until the Promise is resolved or rejected.

**Can you use await outside async functions?**

No, await must be used inside an async function.

**What happens if an async function throws an error?**

The Promise returned by the function is rejected, and the error can be caught with try…catch or .catch().

**How is Async/Await different from Promises?**

Async/Await is syntactic sugar over Promises, making the code easier to read and manage.