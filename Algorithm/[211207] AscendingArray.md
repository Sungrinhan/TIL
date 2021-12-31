# AscendingArray
### Question
You should be return an ascending integer array that starts with indicated by the start parameter and ends with the end parameter.

### Input
Parameter 1: start
number type
Parameter 2: end
number type
### Output
Your function should return an array
Constraints
The function ascendingArray is written in the form of a recursive function.
The use of repeat statements (for, while) is prohibited.
The start parameter must always be less than or equal to the end parameter.
### I/O Example
```js
let output = ascendingArray(1,7);
console.log(output); // --> [1, 2, 3, 4, 5, 6, 7]

output = ascendingArray(6,12);
console.log(output); // --> [6, 7, 8, 9, 10, 11, 12]

output = ascendingArray(24,31);
console.log(output); // --> [24, 25, 26, 27, 28, 29, 30, 31]

output = ascendingArray(106,114);
console.log(output); // --> [106, 107, 108, 109, 110, 111, 112, 113, 114]
```

- - -
### MINE
```js
function ascendingArray(start, end) {
  if (start === end) {
    return [start];
  } else { 
    const result = ascendingArray(start + 1, end)
    // result.unshift(start);
    return [start, ...result]
  }
};

// 종료되는 시점 = 시작인덱스와 종료되는 인덱스가 같은지점이다.
// head 부분과 tail 부분을 나눴다. result 를 선언하고, unshift 로 start 를 추가하던지, spread syntax 를 사용해서 start 값을 추가해준다.
// start index 와 end 가 같아지면 재귀함수가 종료된다. 
// ascendingArray(start, end) = [start] + ascendingArray(start+1, end)
// f(n) = n +f(n-1)
// 1, 7 
// [1,...ascendingArray(2, 7)] [1,2, ...ascendingArray(3,7)]
```
