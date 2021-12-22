## convertToBinary
### Question
Use the recursive function to create a function that returns a decimal number to binary number

### Input
Parameter 1 : n
number type
### Output
Returns the value of the string type converted from decimal number N to binary number
### Constraints
The function convertToBinary should be written in the form of a recursive function.
The use of repeat statements (for, while) is prohibited.
Do not use 'toString' method.
String type must be returned.
### I/O Example
```js
let output = convertToBinary(31);
console.log(output); // --> "11111"

output = convertToBinary(19);
console.log(output); // --> "10011"

output = convertToBinary(84);
console.log(output); // --> "1010100"
```

- - -
### MINE
```js
function convertToBinary(n) {
  // your code here
  // 재귀함수로 풀어본다. 
  // 종료 시점을 정한다.
    if (n === 1 || n === 0) {
        return String(n)
	}
  // 2진법으로 바꾸는 것이니까, 계속 2로 나눈값을 더해주면 된다. 
  // n을 2로 나눈값과, 나머지값이 표기된다.
    return convertToBinary(Math.floor(n / 2)) + String(n % 2)
// 31을 넣으면 -> 15 + '1' > 7+'1'+'1' > 3+ '1'+'1'+'1' > "11111"
// 17 넣으면 > 8+'1' > 4+ '0' + '1' > 2 + '0' + '0' + '1' > '10001'
}
```
