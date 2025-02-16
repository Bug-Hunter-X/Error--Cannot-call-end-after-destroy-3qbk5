# Node.js Uncommon Error: Calling res.end after res.destroy

This repository demonstrates a subtle error in a Node.js HTTP server where `res.end()` is called after `res.destroy()`.  This leads to an unexpected error because the response object is no longer valid after being destroyed.

## The Bug

The `bug.js` file contains a simple HTTP server that simulates an asynchronous operation.  In some cases (50% probability in this example), the server intentionally calls `res.destroy()` to simulate a failure or unexpected closure of the connection. However, it then attempts to call `res.end()` afterwards which results in the error.

## The Solution

The `bugSolution.js` file corrects this by adding a check to ensure `res.writable` before calling `res.end()`. This prevents the error by only attempting to send the response if the connection is still writable.

## How to reproduce the bug:
1. Clone this repository.
2. Run `node bug.js`.
3. Observe the error messages in the console. You may need to refresh the page multiple times to see both success and failure outputs.
4. Run `node bugSolution.js` to see how to fix the issue.