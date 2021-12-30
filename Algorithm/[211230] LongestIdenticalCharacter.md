Implement a function that, given a string, Finds the longest run of identical characters and returns an array containing the start and end indices of that run.
If there are two runs of equal length, return the first one.

### Constraints: Try your function with long, random strings to make sure it handles large inputs well.
1 <= string <= 10,000

### Examples:
```js
test2("abbbcc") // [1, 3]
test2("aabbc")  // [0, 1]
test2("abcd")   // [0, 0]
test2("")       // [0, 0]
```

- - - 

### Solution
```js
function test2(str) {
  // str 이 없는경우, null 값을 리턴한다.
  if (!str) { 
    return null;
  }

  let currentCount = 1;
  let topCount = 0;
  let currentStart = 0;
  let topStart = 0;
  let topEnd = 0;
  let topRun = str[0];

  for (let i = 1; i < str.length; i++) { // str 을 순회한다.
    if (str[i] === str[i - 1]) { // i번째요소와 그전요소가 같으면 currentCount 를 1씩 늘린다.
      currentCount++;
      if (currentCount > topCount) { // current 가 top 보다 크면 top 값을 current 로 해주고 start 도 current 스타트로 바꾼다. 마지막으로 topEnd = i번째로 바꾼다.
        topCount = currentCount;
        topStart = currentStart;
        topEnd = i;
      }
    } else {
      currentCount = 1; // 그 외에는 current Count 와 start 를 그대로 해준다.
      currentStart = i;
    }
  }

  return [topStart, topEnd]; // 마지막으로 결과값인 스타트와 end 를 출력해준다.
  
};

// If you need a random string generator, use this!
// (you wont need this function for your solution but it may help with testing)
function randomstring(len) {
  let text = '';
  let possible = 'abcdefghijklmnopqrstuvwxyz';

  for (let i = 0; i < len; i++) {
    text += possible.charAt(Math.floor(Math.random() * possible.length));
  }

  return text;
};
```
