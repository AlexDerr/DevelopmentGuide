# Debouncing

The goal of debouncing a function is to make sure that it isn't getting called too frequently which can cause errors and performance issues.

```typescript
/**
 * Debounces a function, ensuring it's only called after a specific delay 
 * since the last time it was invoked.
 * 
 * @param func The function to debounce.
 * @param delay The duration (in milliseconds) to wait before executing the function.
 * @returns A new, debounced function.
 */
function debounce<T extends (...args: any[]) => void>(func: T, delay: number): (...args: Parameters<T>) => void {
    // `timeoutId` is the crucial variable, it's declared here in the outer function's scope.
    let timeoutId: NodeJS.Timeout | null;

    // The function returned here is the actual debounced function that the user will call repeatedly
    return function (this: any, ...args: Parameters<T>) {
        // The closure: This inner function "remembers" and can access `timeoutId` form parent scope 

        // If a timer is already running from a previous call, cancel it. `timeoutId` still holds the reference to the last timer set.
        if (timeoutId) {
            clearTimeout(timeoutId);
        }

        //  Schedule the function to run after the 'delay', store the new timer's ID in the *same* 'timeoutId' variable.
        timeoutId = setTimeout(() => {
            // Use `apply` to maintain the correct `this` context and arguments
            func.apply(this, args);
        }, delay);
    };
}

// Usage with multiple params, the above implementation is generic and accepts any number of param to be passed through
function handleInput(name: string, param2: number) {
    ...
}

// This is the debounced function
// 200 is the timeout
const debouncedHandleInput = debounce(handleInput, 200)

// So this would be called three times, but if they are all executed before the inital 200ms are expired
//      that we defined above when making `debouncedHandleInput`, then only the final one will execute
debouncedHandleInput("name1", 1)
debouncedHandleInput("name2", 2)
debouncedHandleInput("name3", 3)

// Usage with a counter

// So we define our count
let counter = 0;

// Define the function that will add to the counter, and will be debounced
function increment() {
    counter++;
}

// This creates our debounced function
const debouncedIncrement = debounce(incrememt, 500);

// We call this 3 times in a row, so the first execution will not be done waiting 500 ms, before the second is called.
//      This means that when the second is called, it will cancel the previous call due to the `clearTimeout` call.
//      Same with the third
debouncedIncrement();
debouncedIncrement();
debouncedIncrement();

console.log(counter); // Prints 1, because of the debounce 2 calls get cancelled and the third executes
```

This debounce works due to the concept of a closure in Javascript/Typescript.
- When you initially call `... = debounce(..., 200)`, the function `debounce` runs once, but it creats the variable `timeoutId`
- The inner function that is returned, maintains a link (a closure) to the the environment it was created in which contains that `timeoutId` variable. The `timeoutId` stays in memory because the inner function may reference it, which we are doing with our debounce
- So then every time we call `debouncedHandleInput`, we are executing the same inner function which then reads from the shared state containing `timeoutId` that we can then reset causing only the function to run once