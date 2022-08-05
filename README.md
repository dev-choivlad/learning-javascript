# learning javascript
Javascript practice exercises and solutions.  
This collection of tasks helps me better understand javascript. hope it will be useful for you too.

---

###### 1. Get the maximum sum of hourglass.
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
