# write a function that takes a string of text and returns true if the parentheses are balanced and false otherwise.

### Example:
balancedParens('('); // false
balancedParens('()'); // true
balancedParens(')('); // false
balancedParens('(())'); // true

### Step 2:
make your solution work for all types of brackets

### Example:
balancedParens('{}'); // true
balancedParens('({})'); // true

balancedParens('({)}'); // false

### Step 3:
ignore non-bracket characters
balancedParens(' var wow = { yo: thisIsAwesome() }'); // true
balancedParens(' var hubble = function() { telescopes.awesome();'); // false

- - - 
### Mine
```js
//
function balancedParens (str) {

//브라켓을 제외한 모든것은 제외됨.
// (,),{,},[,]
// 제외한 배열을 arr 라고 할때, arr.length 가 홀수이면 일단 false
// 짝수인 상태에서 반으로 나누고  , 왼쪽에 },),] 가 오면 false, 오른쪽에 {,(,[ 가 오면 false 다.
// arr 를 반으로 나눠서, arr1 = []    ,  arr2 = [].reverse 를 해서, 각 배열을 순회하여 (이면 ), {이면 }, [이면 ]조건을 만족하면 true 다.
let arr = str.split('') // 배열로 만들고
arr.filter((el)=> { // bracket 이 아닌것들은 제거
  el === '(' || el === ')' || el === '{' || el === '}' || el === '[' || el === ']'
    
})
let leftSide = ['(','[','{']
let rightSide = [')',']','}']
if(arr.length %2 ===0 ){ // 짝수인 경우
  let arr1 = arr.slice(0,arr.length/2)
  let arr2 = arr.slice(arr.length/2, arr.length)
  for(let i =0; i<arr.length/2 ; i++){
    if(rightSide.includes(arr1[i]) || leftSide.includes(arr2[i])){
      return false
    }

  }
  return true
  // if(arr1.includes(')') || arr1.includes( ']' ) || arr1.includes('}'))
}
return false
}
function foo() {}
```

### Others

bracket 에는 짝이 있기때문에 , 나는 두개의 배열을 만들었지만

레퍼런스에는 객체를 사용하였다. 키값과 밸류가 정해진다면 객체로 사용하여 더 쉽게 해보자.

그리고 출력할 기본 스택 = [] 빈배열로 두었고,

키값이 들어가면 그에 해당하는 밸류값이 있나 찾고, 있다면 스택에 push 한다.
그다음 밸류값이 있으면 pop 을하여 stack 이 0이 되면 true 가 출력되게 하였다.

만약에 키값이 없는데 밸류값이 들어가면 false 가 출력되게 했음.

```js
var balancedParens = function(input) {
  /* START SOLUTION */
  var stack = [];
  var pairs = {
    '{': '}',
    '[': ']',
    '(': ')'
  };

  for (var i = 0; i < input.length; i++) {
    var chr = input[i];

    if (pairs[chr]) {
      stack.push(chr);
    } else if (chr === '}' || chr === ']' || chr === ')') {
      if (pairs[stack.pop()] !== chr) {
        return false;
      }
    }
  }

  //return false if there are any unclosed brackets
  return stack.length === 0;
  /* END SOLUTION */
};
```
