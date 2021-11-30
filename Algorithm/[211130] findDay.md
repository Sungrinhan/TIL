# Write a function

 `   function day(ab);`
 
January 1, 2007 is a Monday. What day is a and b in 2007?
a and b are given in the form of a string, and a space is given between a and b.
The input value is a string and is given in the form of 'a b'.

In 2007, January, March, May, July, August, October and December have 31 days, April, June, September and November have 30 days, and February has 28 days.

Output format: SUN, MON, TUE, WED, THU, FRI, SAT

### Examples:
1. day("1 1"); 1/12007 is a MON.
2. day("3 17"); 3/17/2007 is a SAT.

? Let's think of an edge case even if it's not in the test case.
44th April or 44th April, when only one number is given, when the type of the input value is different, etc.

- - -

### Mine
```js
function day(str) {
  //우선 스플릿을 통해 월과 날짜를 나눠야 한다. arr = str.split(' ')
  // let month = [1,2,3,4,5,6,7,8,9,10,11,12]
  // let days = [31,28,31,30,31,30,31,31,30,31,30,31]
  // let day = ['MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT', 'SUN']
  // month(arr[0])-1 까지의 days + arr[1] 를 7로 나누었을 때 나머지값 
  // 출력은 day[나머지 값 ]
  let a = Number(str.split(' ')[0])
  let b = Number(str.split(' ')[1])
  // index 는 0부터 이기 때문에 0번째 index에 더미데이터를 넣어준다 .
  let month = [0,31,28,31,30,31,30,31,31,30,31,30,31]
  let day = ['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT' ]
  let days = month.slice(0, a).reduce((acc, cur) => acc + cur)
  days = days + b
  days = days % 7
  return day[days]
}
```

### Others

```js
new Date(`2007 ${a} ${b}).getDay()
날짜와 .getDay() 메소드를 이용해서 days 값을 구해줄 수 있다. 
```
