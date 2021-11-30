# Write a function

`    function isIsogram(str)`

An isogram is a word that has no repeating letters, consecutive or non-consecutive.
Implement a function that determines whether a string that contains only letters is an isogram.

Assume the empty string is an isogram. Ignore letter case.

### Examples:
1. "Dermatoglyphics" would return true. The string will not repeating letters.
2. "gdhnVzgv" would return false. The string will repeating letters 'g', 'v'.

Write an efficient algorithm for the following assumptions:

str.length is an integer within the range [1.. 10,000]

- - -
### Mine
```js
let isIsogram = function(str) {
  // code goes here
  // 빈 배열을 만든다.
  // str 을 하나하나 조회하여
  // 빈배열에 같은값이 있나 조회를 하고
  // 없으면 추가하고 , 있으면 false를 출력한다.
  let arr = [];
  let newarr = str.split('')
  for(let el of newarr){
    if(arr.includes(el)){
      return false
    } else {
      arr.push(el)
    }
  }
  return true
}
// 하나하나 조회를 해보기 때문에 시간복잡도는 O(N) 이 되겠다.
// 
```

### Others
```js
new Set() 메소드를 이용한다.  중복된 값을 제외하고 리턴한다. 그 값은 객체 형태이다.
let arr = [...new Set(newarr)] // spread 문법으로 배열로 복사해준다.
if(arr.length === newarr.length) true  // 중복된 값이 제거된 배열과 기존배열의 길이가 같으면 true
else false // 아니면 false 값이다.

이방법이 더 좋은 이유는 시간복잡도가 매우 줄어든다. 하나하나의 요소를 검색하지 않기 때문에 O(N) 이 되겠다.
```
