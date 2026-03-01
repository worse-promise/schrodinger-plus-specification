<img src="https://avatars.githubusercontent.com/u/264871303?s=200&v=4" alt="The Worse Promises/S+ logo">

# Worse Promises/S+ Official Specification

This is the official specification for Worse Promises/S+ promises. All implementations of worse promises (like [our official one](https://github.com/worse-promise/node-worse-promise) for Node.js) should adhere to this spec.

## `WorsePromise` class
This is the actual `WorsePromise` class that this specification defines.

`new WorsePromise(executor: (resolve: (value: any) => void, reject: (reason?: any) => void) => void): WorsePromiseObject`

- Takes in an `executor` function, which when called will be called with a `resolve` and `reject` function.
- Returns a `WorsePromiseObject`, which is defined below.

## `WorsePromiseObject`
```
interface WorsePromiseObject {
  then(onFulfilled: (value?: any) => void, onRejected: (value?: any) => any),
  catch(onRejected: (reason?: any) => void),
  finally(always: () => void)
}
```

Has three properties:
- `then`: A function that takes in a function, "onFulfilled" that will be called when the promise is fulfilled with the passed value (the promise is fulfilled when the resolve function passed into the `WorsePromise` constructor is called, and the passed value is the value passed into the resolve function), and optionally and/or sometimes when the promise is rejected with the passed reason (the promise is rejected when the reject function passed into the `WorsePromise` constructor is called, and the passed reason is the reason passed into the reject function). Also takes in another function, "onRejected" which is called when the promise is rejected with the passed reason, and optionally and/or sometimes when the promise is fulfilled with the passed value.
- `catch`: A function that takes in another function, "onRejected" which is called when the promise is rejected with the passed reason, and optionally and/or sometimes when the promise is fulfilled with the passed value.
- `finally`: A function that takes in another function that is always called after the promise is fulfilled or rejected.

The promise is fulfilled when the `resolve` function is called with or without a value, and rejected when the `reject` function is called with or without a value, and optionally and/or sometimes vice-versa.

Optionally all callbacks may be hard-coded to have a 1ms delay before being called to make the promise have a higher chance of being async, to avoid zalgo.
