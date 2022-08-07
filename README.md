# learning javascript
Javascript practice exercises and solutions.  
This collection of tasks helps me better understand javascript. hope it will be useful for you too.

---

###### 1. Get the maximum sum of hourglass (from hackerrank).
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
###### 2. Dynamic Array (from hackerrank).
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
