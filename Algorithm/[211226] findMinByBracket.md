After creating an expression with a maximum length of 50 with negative and positive numbers, +, -, and (), I deleted all parentheses in the expression. Let's call this a strange formula.
Write a function that minimizes the value of strange formula using parentheses appropriately.

The number consists of up to 4 digits.

Examples:
'55-50+40' => '55-(50+40)', and the minimum number is -35.
'-1-2-3-4-5' => '-1-2-3-4-5', and the minimum number is -15.

- - -

### SOLUTION
```js
function findMinByBracket(str) {
  let cnt = 0; 
  // +면 count 가 추가되게 한다.
  for (let i = 1; i < str.length ; i +=1 ) {
    if (str[i] == "+") {
      cnt += 1; 
      // str 요소가 + 인 경우는 count+=1 을 해준다.
    } else if (str[i] == '-') {
      break; 
      // str 요소가 -인  경우는 break 루프를 빠져나간다.
    }
  }
  let separators = [' ', '+', '-']; 
  // 연산자를 나눈다.
  let tokens = str.split(new RegExp('[' + separators.join('') + ']', 'g'));

  let sum = Number(tokens[0]); // 모든 수의 합을 tokens[0] 0번째 요소로하고 이를 숫자Number 메소드를 쓴다.

  let temp = 0; // 임시로 저장할 값을 temp 로 선언하고 0을 할당한다.
  for(let i = 1; i < tokens.length; i += 1) {
    if (temp < cnt) {
      sum += Number(tokens[i]); 
      // temp 가 cnt 보다 작으면 sum = sum + Number(tokens[i])
    } else {
    sum -= Number(tokens[i]); 
    // temp 가 cnt 보다 크거나 같으면 sum = sum - Number(tokens[i])
    }
    temp ++; 
    // temp 는 i 를 순회할때마다 ++ 을 해준다.
  }
  return sum; 
  // 마지막으로 sum 을 출력한다.
}
```
