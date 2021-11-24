
# fibonacci
문제
아래와 같이 정의된 피보나치 수열 중 n번째 항의 수를 리턴해야 합니다.

0번째 피보나치 수는 0이고, 1번째 피보나치 수는 1입니다. 그 다음 2번째 피보나치 수부터는 바로 직전의 두 피보나치 수의 합으로 정의합니다.
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, ...
입력
인자 1 : n
number 타입의 n (n은 0 이상의 정수)
출력
number 타입을 리턴해야합니다.
### 주의사항
재귀함수를 이용해 구현해야 합니다.
반복문(for, while) 사용은 금지됩니다.
함수 fibonacci가 반드시 재귀함수일 필요는 없습니다.
### 입출력 예시
```js
let output = fibonacci(0);
console.log(output); // --> 0

output = fibonacci(1);
console.log(output); // --> 1

output = fibonacci(5);
console.log(output); // --> 5


output = fibonacci(9);
console.log(output); // --> 34
```

- - -
피보나치 정의를 생각해봤다.
f(n) = f(n-1) + f(n-2)
```js
function fibonacci(n) {
  if(n<=1){ // 
    return n ;
  }
  return fibonacci(n-1) + fibonacci(n-2);
}
```
위의 방법같이 재귀함수를 사용 할 경우 , 매우 많은 함수를 계산해야 한다. 예를들어 n이 5일 경우

f(5) = f(4) + f(3) = (f(3) + f(2)) + f(3) = ((f(2) + f(1)) + f(2)) + f(3) = ((1 + 1) + 1) + (f(2) + f(1)) = ((1 + 1) + 1) + (1 + 1) = 5 처럼 호출되는 재귀함수가 급격하게 늘어난다.

시간복잡도 = O(2^n)
