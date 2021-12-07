# Palindrome
### Question
When the input string is placed upside down, it should return whether it matches or not.

### Input
Parameter 1: str
string type
### Output
boolean type must be returned.
### Constraints
The function palindrome is written in the form of a recursive function.
The use of repeat statements (for, while) is prohibited.
boolean type must be returned.
If it is an empty string, you should be return true.
Upper and lower case letters are treated as different characters.
### I/O Example
```js
let output = palindrome('apple');
console.log(output); // --> false

output = palindrome('level');
console.log(output); // --> true

output = palindrome('now i won');
console.log(output); // --> true

output = palindrome('Now i won');
console.log(output); // --> false
```

- - -
### MINE
```js
 function palindrome(str) {
   return isPalindrome(str, 0, str.length - 1); // 기존 palindrome 외에 palindrome 을 판별하는 외부함수를 만들었다.
 }

 function isPalindrome(str, start, end) {
   if (start >= end) {  // 종료시점을 만들어준다. start 인덱스와 end 인덱스가 같으면 true 를 리턴한다. 다른점을 못찾았기 때문
       return true;
   }
   if (str.charAt(start) !== str.charAt(end)) {
       return false; // 끝과 시작점을 비교해서 , 다른 문자열이 나오면 false 를 반환한다.
   } else {
       return isPalindrome(str, start + 1, end - 1); // 같지만 start 와 end가 같아질때까지 재귀함수를 실행한다.
   }
 }

```

### Others
```js
위의 경우는 start와 end 인덱스를 끝에서 부터 안쪽으로 찾았지만, 다른방법도 있다.
midleIndex 를 찾아서 양끝쪽으로 찾아가는 방법도 있다. 
```
