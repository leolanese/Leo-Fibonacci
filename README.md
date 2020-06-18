# Fibonachi with recursion, destructoring and memoization:



### Fibonacchi:
The Fibonacci Sequence is such that each number is the sum of the previous two numbers.

### Recursion:
In simple terms, a recursive function is a function that calls itself.

### Why is important:
The common Fibonacci logic and interview question may at first sight appear to be a simple question designed to test your basic understanding of 'recursion'. A major reason why this question appears so often in coding interviews is because answering it correctly demonstrates an understanding of a fundamental concept in programming: recursion. 

> If we don’t use it, it is not VERY smart solution.

### How to think about this:
By definition, the first two numbers in the Fibonacci sequence are either 1 and 1, or 0 and 1, depending on the chosen starting point of the sequence,
and each subsequent number is the sum of the previous two.

### Fibonnacci Sequance:
| F0  | F1  | F2  | F3  | F4 | F5 | F6 | F7 | F8 | F9 | F10| F11| F12| F13| F14| F15| F16|
|---	|---	|---	|---	|--- |--- |--- |--- |--- |----|----|----|----|----|----|----|----|
| 0   | 1   | 1   | 2   | 3	 | 5  | 8  | 13 | 21 | 34 | 55 | 89 | 144| 233| 377| 610| 987|


## first attempt
// first attempt
```javascript
function fibonacci(position){
   if(position < 3) return 1;
   else return fibonacci(position - 1) + fibonacci(position - 2) // stack overflow: you've to exceed the maximum call stack limit.
};
fibonacci(15); // 610
```

### Further information:
A deep visualization of the breakdown of how each function: ttps://www.youtube.com/watch?v=zg-ddPbzcKM&t=319s

---

## simplest approach
// simplest approach usign recursion
```javascript
function fib(n) {
  if (n <= 1) {
    return n;
  } else {
    return fib(n - 1) + fib(n - 2);
  }
}
fib(15); // 610
```
---

## ES5 Fibonacci
// ES5 and not very smart not fast way to get the Fibonacci number
```javascript
function fibIterative(n) {
  var a = 1;
  var b = 0;
  while (n > 0) {
    [a, b] = [b + a, a];
    n--;
  }
  return b;
}
fibIterative(15); // 610
```

---

## ES5 recursive Fibonacci
// ES5 recursive Fibonacci number
```javascript
var recursive = function(n) {
    if(n <= 2) {
        return 1;
    } else {
        return this.recursive(n - 1) + this.recursive(n - 2);
    }
};
recursive(15); // 610
```

## ES6 recursive Fibonacci
```javascript
function fibRecursive(n, a = 1, b = 0) {
  if (n === 0) {
    return b;
  } else {
    return fibRecursive(n - 1, a + b, a);
  }
}
fibRecursive(15); // 610
```

---

## Fibonacci Series using recursion
```javascript
var fseries = function (var1) {
  if (var1===1) {
    return [0, 1];
  } else {
    var sum = fseries(var1 - 1);
    sum.push(sum[sum.length - 1] + sum[sum.length - 2]);
    return sum;
  }
}; // [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610]

```

---

## using cache 
```javascript
const resultsCache = [];
function fib(n) {
  if (n <= 2)
	return 1;
  if (resultsCache[n]) // check if N-th element is already calculated and stored in cache
    return resultsCache[n]; // if element is in cache read it and return
  fibN = fib(n-1) + fib(n-2); // if element is not in cache calculate it
  resultsCache[n] = fibN; // put element into cache right after calculating it
  return fibN;
};
fib(15); // 610
```

## using cache + recursion + IIFE (from TDD Developer book)
```javascript
var fibonacci = (function () {
  var cache = {};

  function fibonacci(x) {
    if (x <= 2) return 1;
    if (!cache[x]) cache[x] = fibonacci(x-1) + fibonacci(x-2);
    return cache[x];
  }

  return fibonacci;
}());
fibonacci(15); // 610
```

## Memoization
Is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls.

// using memoisation 
```javascript
function fibonacci(num, memo) {
  memo = memo || {};
  if (memo[num]) return memo[num];
  if (num <= 2) return 1;
  return memo[num] = fibonacci(num - 1, memo) + fibonacci(num - 2, memo);
}
fibonacci(15); // 610
fibonacci(1500); // Infinity
```

## Destructoring and generators
// fibonacchi using destructoring
```javascript
function* fibonacci() {
  let a = 0;
  let b = 1;

  while (true) {
    yield a;
    [a, b] = [b, a + b];
  }
}
const fib = fibonacci();
const [first, second, third, fourth, fifth, sixth, seventh] = fib;
```

## ES6 JS + recursive (MB and very short)
```javascript
const fib = x => (x <= 1) ? x : fib(x-1) + fib(x-2);
fib(15); // 610
```

## recursive and great performance
```javascript
const fib = (acc, x = 0, y = 1) => 0 < acc ? fib(--acc, y, x + y) : x;
fib(15); // 610
```
