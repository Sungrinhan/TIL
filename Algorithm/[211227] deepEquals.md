Write a function that, given two objects, returns whether or not the two are deeply equivalent--meaning the structure of the two objects is the same, and so is the structure of each of their corresponding descendants.

Examples:
deepEquals({a:1, b: {c:3}},{a:1, b: {c:3}}); // true
deepEquals({a:1, b: {c:5}},{a:1, b: {c:6}}); // false

don't worry about handling cyclical object structures.

- - - 

### Solution
```js
function deepEquals(a, b) {
  
  if(a === b) { 
    return true;
    }
    // a와 b가 같으면 true 를 출력
  if(a && !b || !a && b) {
    return false;
    }
    // a 혹은 b 가 없으면 false 를 출력
  if(typeof a !== 'object' || typeof b !== 'object') {
    return false;
    }
    // a 혹은 b 가 객체가 아니면 false 를 출력
    
  let aKeys = Object.keys(a); // a 의 키를 배열로
  let bKeys = Object.keys(b); // b 의 키를 배열로
  if(aKeys.length !== bKeys.length) {
    return false;
    }
    // aKeys 와 bKeys 의 길이가 다르면 false 를 출력
  if(aKeys.length === 0) {
    return true;
    } // 빈 두 객체는 같다고 한다.

  for(let i = 0; i < aKeys.length; i++) {
    if(!deepEquals(a[aKeys[i]], b[aKeys[i]])) {
      return false;
      }
  }
  // a 객체에 akeys[i] 각 요소를 순회하여 같지 않으면 false
  return true; // 이외에는 모두 true 를 반환한다.
  
};
```
