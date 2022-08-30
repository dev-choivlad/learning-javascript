# learning javascript
Javascript practice exercises and solutions.  
This collection of tasks helps me better understand javascript. hope it will be useful for you too.

---

#### 1. Get the maximum sum of hourglass (from hackerrank).
Given a 6x6 2D array.
```javascript
const arr = [
  [1, 1, 1, 0, 0, 0],
  [0, 1, 0, 0, 0, 0],
  [1, 1, 1, 0, 0, 0],
  [0, 0, 2, 4, 4, 0],
  [0, 0, 0, 2, 0, 0],
  [0, 0, 1, 2, 4, 0],
]
```
There are 6 hourglasses in array. An hourglass sum is the sum of an hourglass' values. Calculate the hourglass sum for every hourglass in array, then print the maximum hourglass sum. The array will always be 6x6.
```javascript
/*

a b c       1 1 1
  d   ===>    1  
e f g       1 1 1

this hourglass starts at the position of arr[0][0]

Constraints:
-9 <= arr[i][j] <= 9
 0 <= i, j <= 5
 
 */
```

<details><summary><b>Solution</b></summary>
<p>
Points to note:

- Negative values possible.
- Maximum sum can be less than zero.
- Range of element value is -9 to 9.
- Numbers to be summed for each hourglass = 7.
- Minimum possible value for sum = 7 * -9 = -63.

```javascript
function getHourglassMaxSum(arr) {
  let maxSum = -63; // max possible negative value
  
  // loop through the arrays
  for (let i = 0; i < arr.length - 2; i++) {
    
    for (let j = 0; j < arr.length - 2; j++) { // loop through the values of array
      let top = arr[i][j] + arr[i][j+1] + arr[i][j+2]; // sum of top 3 elements of hourglass
      let middle = arr[i+1][j+1]; // the mid element of hourglass
      let bottom = arr[i+2][j] + arr[i+2][j+1] + arr[i+2][j+2]; // sum of bottom 3 elements of hourglass

      let sum = top + middle + bottom;
      maxSum = Math.max(maxSum, sum);
    }
  }
  return maxSum;
}
```
</p>
</details>

---
#### 2. Dynamic Array (from hackerrank).
- Declare a 2-dimensional array, arr, of n empty arrays. All arrays are zero indexed.
- Declare an integer, lastAnswer, and initialize it to 0.
- There are 2 types of queries, given as an array of strings for you to parse:  
    - Query: 1 x y
        1. let index = ((x ^ lastAnswer) % n)  
        2. append the integer y to arr[index]
    - Query: 2 x y  
        1. let index = ((x ^ lastAnswer) % n)  
        2. assign the value arr[index][y % arr.lenght] to lastAnswer  
        3. store the new value of lastAnswer to an answers array

Function Description:  
Complete the dynamicArray function below.
dynamicArray has the following parameters:
- int n: the number of empty arrays to initialize in arr
- string queries[q]: query strings that contain 3 space-separated integers
  
Returns:  
int[]: the results of each type 2 query in the order they are presented

Input Format:  
The first line contains two space-separated integers, n, the size of arr to create, and q, the number of queries, respectively. Each of the  subsequent lines contains a query string, queries[i].

Constraints:  
1 <= n, q <= 10^5  
0 <= x, y <= 10^9  
It is guaranteed that query type 2 will never query an empty array or index.

<details><summary><b>Solution</b></summary>
<p>

```javascript
function dynamicArray(n, queries) {
  // Declare a 2-dimensional array of n empty arrays
  const arr = [];
  for (let i = 0; i < n; i++) {
    arr[i] = []
  }
  
  let lastAnswer = 0;
  const answers = []; // The function returns this array as a solution

  // loop through the queries
  for (let i = 0; i < queries.length; i++) {
    let x = queries[i][1]; // Get value of x
    let y = queries[i][2]; // Get value of y
    let index = (x ^ lastAnswer) % n;

  // Check the statesments 1 or 2  
    if (queries[i][0] == 1) {
      arr[index].push(y)
    } else if (queries[i][0] == 2) {
      lastAnswer = arr[index][y % arr[index].length];
      answers.push(lastAnswer);
    }
  }
  return answers;
}
```
</p>
</details>

---
#### 3. What's the output?

```javascript
function sayHi() {
  console.log(name);
  console.log(age);
  var name = 'Lydia';
  let age = 21;
}

sayHi();
```

- A: `Lydia` and `undefined`
- B: `Lydia` and `ReferenceError`
- C: `ReferenceError` and `21`
- D: `undefined` and `ReferenceError`

<details><summary><b>Solution</b></summary>
<p>

#### Solution: D

Within the function, we first declare the `name` variable with the `var` keyword. This means that the variable gets hoisted (memory space is set up during the creation phase) with the default value of `undefined`, until we actually get to the line where we define the variable. We haven't defined the variable yet on the line where we try to log the `name` variable, so it still holds the value of `undefined`.

Variables with the `let` keyword (and `const`) are hoisted, but unlike `var`, don't get <i>initialized</i>. They are not accessible before the line we declare (initialize) them. This is called the "temporal dead zone". When we try to access the variables before they are declared, JavaScript throws a `ReferenceError`.

</p>
</details>

---
#### 4. What's the output?

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
```

- A: `0 1 2` and `0 1 2`
- B: `0 1 2` and `3 3 3`
- C: `3 3 3` and `0 1 2`

<details><summary><b>Solution</b></summary>
<p>

#### answer: C

Because of the event queue in JavaScript, the `setTimeout` callback function is called _after_ the loop has been executed. Since the variable `i` in the first loop was declared using the `var` keyword, this value was global. During the loop, we incremented the value of `i` by `1` each time, using the unary operator `++`. By the time the `setTimeout` callback function was invoked, `i` was equal to `3` in the first example.

In the second loop, the variable `i` was declared using the `let` keyword: variables declared with the `let` (and `const`) keyword are block-scoped (a block is anything between `{ }`). During each iteration, `i` will have a new value, and each value is scoped inside the loop.

</p>
</details>

---
#### 5. What's the output?

```javascript
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius,
};

console.log(shape.diameter());
console.log(shape.perimeter());
```

- A: `20` and `62.83185307179586`
- B: `20` and `NaN`
- C: `20` and `63`
- D: `NaN` and `63`

<details><summary><b>Solution</b></summary>
<p>

#### answer: B

Note that the value of `diameter` is a regular function, whereas the value of `perimeter` is an arrow function.

Arrow functions don't have their own `this`. If `this` is accessed, it is taken from the outside! This means that when we call `perimeter`, it doesn't refer to the shape object, but to its surrounding scope (window for example).

There is no value `radius` on that object, which returns `NaN`.

</p>
</details>

---
#### 6. What's the output?

```javascript
+true;
!'Lydia';
```

- A: `1` and `false`
- B: `false` and `NaN`
- C: `false` and `false`

<details><summary><b>Solution</b></summary>
<p>

#### answer: A

The unary plus tries to convert an operand to a number. `true` is `1`, and `false` is `0`.

The string `'Lydia'` is a truthy value. What we're actually asking, is "is this truthy value falsy?". This returns `false`.

</p>
</details>

---
#### 7. Filter unique array values
You have an array `arr`  
Create a function `unique(arr)` that returns an array with unique items of arr.
```javascript
const arr = ["gimme", "gimme", "gimme", "a", "man", "after", "midnight"];
console.log(unique(arr)) // ["gimme", "a", "man", "after", "midnight"]
```
<details><summary><b>Solution #1</b></summary>

For each item we’ll check if the resulting array already has that item.
If it is so, then ignore, otherwise add to results.

```javascript
function unique(arr) {
  let result = [];

  for (let str of arr) {
    if (!result.includes(str)) {
      result.push(str);
    }
  }

  return result;
}
```

The code works, but there’s a potential performance problem in it. The method `result.includes(str)` internally walks the array `result` and compares each element against `str` to find the match.  
So if `arr.length` is `10000` we’ll have something like `10000*10000 = 100 millions` of comparisons. That’s a lot. So the solution is only good for small arrays.

</details>

<details><summary><b>Solution #2</b></summary>

Use `Set` to store unique values.

```javascript
function unique(arr) {
  return Array.from(new Set(arr));
}
```

</details>

---
#### 8. Filter anagrams
(Anagrams)[https://en.wikipedia.org/wiki/Anagram] are words that have the same number of same letters, but in different order.  
For example:  
`nap - pan`,
`ear - are - era`
`cheaters - hectares - teachers`.  

Create a function `aclean(arr)` that returns an array cleaned from anagrams.

```javascript
const arr = ["nap", "teachers", "cheaters", "PAN", "ear", "era", "hectares"];
console.log(aclean(arr)) // "nap,teachers,ear" or "PAN,cheaters,era"
```

<details><summary><b>Solution #1</b></summary>

Use `Map` to store sorted rows as keys in Map collection.  
To find all anagrams, let’s split every word to letters and sort them. When letter-sorted, all anagrams are same. If we ever meet a word the same letter-sorted form again, then it would overwrite the previous value with the same key in the map. So we’ll always have at maximum one word per letter-form.

```javascript
function aclean(arr) {
  let map = new Map();

  for (let word of arr) {
    // Split the word by letters, sort them and join back
    let sorted = word.toLowerCase().split('').sort().join(''); // (*)
    
    // Put the word into the map
    map.set(sorted, word);
  }
  // Takes an iterable over map values and returns an array of them.
  return Array.from(map.values());
}
```

</details>

<details><summary><b>Solution #2</b></summary>

Use plain `object` instead of `Map`

```javascript
function aclean(arr) {
  let obj = {};

  for (let i = 0; i < arr.length; i++) {
    let sorted = arr[i].toLowerCase().split("").sort().join("");
    obj[sorted] = arr[i];
  }

  return Object.values(obj);
}
```

</details>

---
