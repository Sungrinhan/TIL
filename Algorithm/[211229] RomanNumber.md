Implement a function that given a roman numeral as input, write a function that converts the roman numeral to a number and outputs it. You should return null on invalid input.

Constraints: When a smaller numeral appears before a larger one, it becomes a subtractive operation. You can assume only one smaller numeral may appear in front of larger one.
I: 1, V: 5, X: 10, L: 50, C: 100, D: 500, M: 1000
1 <= romanNumeral <= 10,000

### Examples:
```js
test1("IV") => 4 Because I(1) is smaller than V(5), it is 5 - 1, not 5 + 1.
test1("LX") => 60
```

- - -

### Solution
```js
const DIGIT_VALUES = {
  I: 1,
  V: 5,
  X: 10,
  L: 50,
  C: 100,
  D: 500,
  M: 1000
};

function test1(romanNumeral) {
  // 엣지케이스, 인자의 값이 문자열이 아닌경우 null 을 return 한다.
  if (typeof romanNumeral !== 'string') {
    return null;
  }
  // 인자가 빈 문자열인 경우 0을 리턴한다.
  if (romanNumeral === '') {
    return 0;
  }
  // 출력할 값 total 을 선언한다.
  let total = 0;
  //문자열을 각 문자를 요소로 같는 배열로 split 한다.
  let romanNumerals = romanNumeral.split('');
  //요소를 순회한다.
  for (let i = 0; i < romanNumerals.length; i++) {
    //i번째 요소값과 그다음값을 미리 선언한다.
    let singleRomanNumeral = romanNumerals[i];
    let nextSingleRomanNumeral = romanNumerals[i + 1];
    //위의 DIGIT_VALUES 객체에서 value 값을 가져온다.
    let numberFromRomanNumeral = DIGIT_VALUES[singleRomanNumeral];
    let nextNumberFromRomanNumeral = DIGIT_VALUES[nextSingleRomanNumeral];
    //현재 요소가 다음 요소보다 작거나, 다음요소가 없는경우
    if (numberFromRomanNumeral < nextNumberFromRomanNumeral && i !== romanNumerals.length - 1) {
      //전체값에서 뺀다.
      total -= numberFromRomanNumeral;
    } else {
      //전체값에 더해준다.
      total += numberFromRomanNumeral;
    }
  }
  return total;
};
```
