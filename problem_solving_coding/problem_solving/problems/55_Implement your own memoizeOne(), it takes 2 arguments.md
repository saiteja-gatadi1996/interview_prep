## Implement your own memoizeOne(), it takes 2 arguments

**Approach Taken**

1. to implement memoization, three conditions has to be satisfied,
   i) isCacheSet && lastContext === this && parameters of lastArgs should match with currentArgs
   ii) isCached and lastContext will be set to true for the very first time
   iii) for third condition we are looping using every condition
   iv) if all three are true, simply return cachedResult
   v) otherwise mutate the cachedResult = funcYouWantToMemoize.call(this, ...args)
   vi) mutate the lastArgs = args, mutate the lastContext = this, isCacheSet = true

```js
function areArraysEqual(a, b) {
  if (a.length !== b.length) return false;
  //every will return true if `every element in a` matches the `corresponding element in b`.
  return a.every((item, i) => item === b[i]);
}

function memoizeOne(func, isEqual = areArraysEqual) {
  let lastArgs = [];
  let lastContext = null;
  let cachedResult = null;
  let isCacheSet = false;

  // The function returned by memoizeOne takes any number of arguments
  return function (...args) {
    // Cache Check (if condition): Checks if: 1. The function was called before (isCacheSet), 2. The this context hasn't changed (lastContext === this), 3. The previous arguments (lastArgs) are equal to the current arguments (args) using isEqual.
    if (isCacheSet && lastContext === this && isEqual(lastArgs, args)) {
      // If all conditions are true, returns the cached result (cachedResult) without calling the original function.
      return cachedResult;
    }

    //If any condition fails, calls the original function with the current this context and arguments, updates the cache, and returns the new result.
    cachedResult = func.call(this, ...args);
    lastArgs = args;
    lastContext = this;
    isCacheSet = true;

    return cachedResult;
  };
}

function add(a, b) {
  console.log('Computing...');
  return a + b;
}

// Memoizing the 'add' function
const memoizedAdd = memoizeOne(add);

// Calling memoizedAdd with same arguments
console.log(memoizedAdd(1, 2)); // Outputs: "Computing..." 3
console.log(memoizedAdd(1, 2)); // Outputs: 3 (No "Computing..." as the result is cached)

// Calling with different arguments resets the cache
console.log(memoizedAdd(2, 3)); // Outputs: "Computing..." 5
```
