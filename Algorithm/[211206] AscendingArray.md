# AscendingArray
### Question
You should be return an ascending integer array that starts with indicated by the start parameter and ends with the end parameter.

### Input
- Parameter 1: start
number type
- Parameter 2: end
number type
### Output
- Your function should return an array
### Constraints
- The function ascendingArray is written in the form of a recursive function.
- The use of repeat statements (for, while) is prohibited.
- The start parameter must always be less than or equal to the end parameter.
### I/O Example
```js
let output = ascendingArray(1,7);
console.log(output); // --> [1, 2, 3, 4, 5, 6, 7]

output = ascendingArray(6,12);
console.log(output); // --> [6, 7, 8, 9, 10, 11, 12]

output = ascendingArray(24,31);
console.log(output); // --> [24, 25, 26, 27, 28, 29, 30, 31]

output = ascendingArray(106,114);
console.log(output); // --> [106, 107, 108, 109, 110, 111, 112, 113, 113, 114]
```
- - -
### MINE
```js
function ascendingArray(start, end) {
if (start === end) {
    return [start]; // 재귀함수가 종료되는 시점을 정해준다.
  } else { 
    const result = ascendingArray(start + 1, end) // result 가 start+1 로 tail 부분이라고 하고
    result.unshift(start); // result 앞부분에 start head 를 심어준다.
    return result; // 마지막으로 출력할 재귀함수 값을 넣어준다.
  }
};
```
