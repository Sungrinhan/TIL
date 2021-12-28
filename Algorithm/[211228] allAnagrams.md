Given a single input string, write a function that produces all possible anagrams
of a string and outputs them as an array. At first, don't worry about
repeated strings. What time complexity is your solution?

Extra credit: Deduplicate your return array without using uniq().

example usage:
var anagrams = allAnagrams('abc');
console.log(anagrams); // 'abc', 'acb', 'bac', 'bca', 'cab', 'cba'


- - -

### Solution
```js
function allAnagrams(string) {
  // string 을 넣으면 조합이 가능한 모든 경우의 수를 배열로 return 해야된다.
    let uniqueOutput = {};
  // 내부 클로저 함수를 만들어준다. (재귀함수)
  // 미리 정할 문자열을 ana, 그 뒤에 정렬할 문자열을 str 로 놓는다.
  
  (function anagram (ana, str) {
    if (str === '') { uniqueOutput[ana] = 1; } // 종료 조건을 만들어준다. 문자열 모두가 ana 로 넘어가고 str 이 빈 문자열이 오면 , 새로 선언한 객체에 넣는다.

    for (let i = 0; i < str.length; i++) {
      anagram(ana + str[i], str.slice(0, i) + str.slice(i + 1));
    } // str 을 순회하면서, ana에 하나씩 추가하는 재귀함수를 만든다. 
  })('', string); // (function anagram(ana,str))함수에 parameter ('', string) 을 넣는다.

  return Object.keys(uniqueOutput); // 객체의 키값만 가져온 배열로 만든다.
}
```
