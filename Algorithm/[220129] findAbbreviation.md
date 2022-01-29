## findAbbreviation
### 문제
두 개의 문자열 strA, strB를 입력받아 아래에 정의된 작업들을 통해 두 문자열을 동일하게 만들 수 있는지 확인해야 합니다.

작업1: strA의 소문자 한개를 대문자로 변경
작업2: strA의 소문자 한개를 제거
### 입력
인자 1: strA
string 타입의 알파벳 문자열
strA.length는 100 이하
인자 2: strB
string 타입의 알파벳 대문자 문자열
strB.length는 100 이하
### 출력
boolean 타입을 리턴해야 합니다.
### 주의사항
작업의 수와 순서는 상관없습니다.
greedy 알고리즘(매칭이 된다고 바로 매칭으로 간주)이 해결하지 못하는 입력이 있을 수 있습니다.
### 입출력 예시
```js
let output = findAbbreviation('AbcDE', 'ABDE');
console.log(output); // --> true ('b'를 대문자로 변경, 'c'를 제거)

output = findAbbreviation('AbcDE', 'AFDE');
console.log(output); // --> false
```

- - -

### Solution
```js
// memoization
function findAbbreviation(strA, strB) {
  const N = 100;
  // 중복 계산을 제거하기 위한 memo 배열
  // 계산되지 않은 상태를 -1로 초기화한다.
  const memo = [];
  for (let i = 0; i < N; i++) memo.push(Array(N).fill(-1));

  const isLower = (chr) => chr.toUpperCase() !== chr;

  const aux = (leftIdx, rightIdx) => {
    // 이미 계산한 적이 있는 경우, 저장된 값을 사용한다.
    if (memo[leftIdx][rightIdx] !== -1) return memo[leftIdx][rightIdx];

    // base case
    if (rightIdx === strB.length)
      return strA.substring(leftIdx).split('').every(isLower);
    else if (leftIdx === strA.length) return false;

    // recursive case
    if (isLower(strA[leftIdx])) {
      if (strA[leftIdx].toUpperCase() !== strB[rightIdx]) {
        // 중복 계산을 피하기 위해 계산의 결과를 저장한다.
        memo[leftIdx + 1][rightIdx] = aux(leftIdx + 1, rightIdx);
        return memo[leftIdx + 1][rightIdx];
      }
      memo[leftIdx + 1][rightIdx + 1] = aux(leftIdx + 1, rightIdx + 1);
      memo[leftIdx + 1][rightIdx] = aux(leftIdx + 1, rightIdx);
      return memo[leftIdx + 1][rightIdx + 1] || memo[leftIdx + 1][rightIdx];
    } else {
      if (strA[leftIdx] !== strB[rightIdx]) return false;
      memo[leftIdx + 1][rightIdx + 1] = aux(leftIdx + 1, rightIdx + 1);
      return memo[leftIdx + 1][rightIdx + 1];
    }
  };

  return aux(0, 0);
}
```
