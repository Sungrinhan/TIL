![image](https://user-images.githubusercontent.com/78065205/143272883-71fdbe5a-efe3-406d-86c1-0394757c052a.png)

- - - 
우선 알파벳 전체 개수를 구한다.
입력되는 암호를 배열로 바꿔주기 위해 split 메소드를 사용한다.
기존 배열에서 처리되는 경우와 , 기존배열을 벗어나 처리되는 경우 2가지로 나눈다.
내가 푼 식은 맞으나 깔끔한 코드는 아닌 것 같다. 변수를 선언하던지 해서 깔끔하게 처리하려면 어떻게 해야할까...
```js
function solution(s, n) {
  var answer = '';
// 알파벳은 a,b,c,d,e ... ,x,y,z 로 26개 
// n 은 1이상 25이하인 자연수 ., 인덱스는 0~ 25까지 
let arr = ['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z']
let newarr = s.split('')

// 어떠한 알파벳의 인덱스 + n 의 숫자가 <= 25인경우, arr[인덱스 + n]
// 인덱스 + n 의 숫자가 26이상인 경우 arr[인덱스+n - 26]


for(let i = 0; i< newarr.length; i ++){
  // 공백일때
  if(newarr[i]===' '){
      answer = answer + ' '
  }
  // 소문자일경우
  else if(arr.includes(newarr[i])){
    if(arr.indexOf(newarr[i]) + n <=25){
      answer = answer + arr[arr.indexOf(newarr[i]) + n]
    }else {
      answer = answer + arr[arr.indexOf(newarr[i]) + n - 26]
    }
  }
  // 대문자일경우
  else {
    if(arr.indexOf(newarr[i].toLowerCase()) + n <=25){
      answer= answer + arr[arr.indexOf(newarr[i].toLowerCase()) + n].toUpperCase()
    } else{
      
      answer = answer + arr[arr.indexOf(newarr[i].toLowerCase()) +n -26].toUpperCase()
    }
  }
}
return answer;
}


console.log(solution('abc', 3))
```
