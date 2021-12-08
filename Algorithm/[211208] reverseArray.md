Given an arbitrary input array, write a function that reverses the contents of the array (ie, without modifying the original array.)
Don't use the native Array.prototype.reverse() method.

Extra Credit: Reverse in-place (don't use an extra array).

Here's a sample input to get you going:

reverseArray(1, 8, 39, null, 2, 9, 'bob')0 // should equal => 'bob'

- - -

### MINE
```js
// 재귀함수가 종료되는 지점을 만든다.
// head  와 tail 을 만들어준다.
// head 는 array의 0번째 요소, 그 이후는 tail
// reverse 를 해야하므로, head 를 맨마지막으로, tail 부분을 앞쪽으로 보낸다.
// tail부분을 재귀함수로 출력한다.
function reverseArray(array) {
  // your code here
    if(array.length === 0){
    return [];
  }
  let head = array[0];
  let tail = array.slice(1);
  return reverseArray(tail).concat(head);
}
```
