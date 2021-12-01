Write a function

   ` runLength(str)`
   
Using the JavaScript language, have the function RunLength(str) take the str parameter being passed and return a compressed version of the string using the Run-length encoding algorithm.
This algorithm works by taking the occurrence of each repeating character and outputting that number along with a single character of the repeating sequence.

### Examples:
1. "wwwggopp" would return 3w2g1o2p. The string will not contain any numbers, punctuation, or symbols.
2. "EDNSOEQTWVOQQVDVRC" would return 1E1D1N1S1O1E1Q1T1W1V1O2Q1V1D1V1R1C.

Write an efficient algorithm for the following assumptions:

str.length is an integer within the range 1.. 100,000

- - -

### Mine
```js
function runLength(str) {
  // 빈 String 을 만든다.
  // str이 빈 문자열이면 빈문자열을 출력한다.
  // str을 split 하여 배열형태로 만든다.
  // 새로운배열 arr 을 만들고, str[0]요소에 대한 숫자와 알파벳을 더해준다.
  // newarr 을 순회한다. i=1부터 시작한다. 왜? i-1이 0 이상이어야 하므로.
  // newarr[i] 와 newarr[i-1] 값을 비교해서 같으면 앞의 숫자를 ++ , 다르면 숫자 1과 newarr[i]를 푸쉬해준다.
  
  // 엣지 케이스는 항상 생각하자.
  if(str ===''){
    return ''
  }
  
  let newarr = str.split('')
  let arr = [1,newarr[0]]

  for(let i = 1 ; i< newarr.length ; i++){
    if(newarr[i]===newarr[i-1]){
      
      arr[arr.length-2]++
    }
    else {
      arr.push(1)
      arr.push(newarr[i])
    }
  }
  return arr.join('')
}


```

### Others

While문을 두번 사용하였다. 

그리고 str의 각요소를 compressed = [number, value] 값으로 표현하고, 마지막에 join 메소드를 써서 기존 빈 문자열에 합쳐주는 방식으로 하였다.

i=0 ; i< str.length 로 범위를 정했고

그다음문자열에 관한것을 j= i+1 , 같으면 number++ 해주고, 아니면 break 를 사용했다.

이것을 끝까지 순회하여 빈문자열에 합쳐주면 기존 답이 나온다.
```js
function runLength(str) {
  let i = 0;
  let rle = "";
  while (i < str.length) {
    const c = str[i];
    let j = i + 1;
    const compressed = [1, c];

    while (j < str.length) {
      if (str[j] === c) {
        compressed[0] += 1;
      } else {
        break;
      }
      j++;
    }

    rle += compressed.join('');
    i = j;
  }

  return rle;
}
```
