## closestPairOfPoints
### 문제
좌표평면 상의 다양한 점들을 입력받아 가장 가까운 두 점 사이의 거리를 리턴해야 합니다.

### 입력
인자 1: points
배열을 요소로 갖는 배열
points.length는 40,000 이하
points[i]는 number 타입을 요소로 갖는 배열
points[i].length는 2
points[i]의 요소는 차례대로 좌표평면 위의 y좌표, x좌표
points[i][j]는 0 이상 10,000 이하의 정수
### 출력
number 타입을 리턴해야 합니다.
### 주의사항
points는 y좌표나 x좌표 등으로 정렬되어 있지 않습니다.
두 점 사이의 거리를 계산하는 함수 calculateDistance가 주어집니다. 두 점 간 거리는 반드시 이 함수를 이용해서 계산해야 합니다.
함수 calculateDistance는 소수점 계산을 피하기 위해 두 점 사이의 거리에 100을 곱한 후 반올림하여 정수 부분만 취합니다. 최단 거리도 이 기준으로 판단합니다.
### 입출력 예시
```js
let points = [
  [0, 0],
  [1, 3],
  [2, 2],
];
let output = closestPairOfPoints(points);
console.log(output); // --> 141 ([1, 3], [2, 2])
/*
3 |  x
2 |     x
1 |       
0 | x 
------------
    0 1 2 3 
*/

points = [
  [0, 0],
  [0, 1],
  [0, 3],
  [0, 5],
];
output = closestPairOfPoints(points);
console.log(output); // --> 100 ([0, 0], [0, 1])
/*
5 | x
4 | 
3 | x
2 |     
1 | x     
0 | x 
------------
    0 1 2 3 
*/
```

- - -

### Solution
```js
// divide and conquer: O(N * logN)
const closestPairOfPoints = function (points) {
  const bruteForce = (start, end, sorted) => {
    // naive solution과 동일한 로직
    // 모든 쌍을 비교한다. 3개 이하에 대해서만 호출되므로 크게 비효율적이지 않다.
    let min = Number.MAX_SAFE_INTEGER;
    for (let src = start; src <= end; src++) {
      for (let dst = src + 1; dst <= end; dst++) {
        const dist = calculateDistance(sorted[src], sorted[dst]);
        min = Math.min(min, dist);
      }
    }
    return min;
  };

  const closestCrossing = (mid, sorted, min) => {
    // 가운데(mid)를 기준으로
    const strip = [];
    const midX = sorted[mid][1];
    let lIdx = mid - 1;
    let rIdx = mid + 1;

    // 왼쪽과 오른쪽 부분에서 가장 가까운 두 점 사이의 거리가 min으로 주어진다.
    // 가운데를 기준으로 오직 x좌표만을 기준으로 min보다 가까운 좌표만 고려한다.
    // y좌표가 같다고 가정하면, 최소한 이 조건(x좌표 기준 min 이하)을 만족해야하기 때문이다.
    // y좌표가 같을 경우 두 점 사이의 거리는 x축 좌표 간의 거리다.
    // 단, 소수점 계산을 피하기 위해 두 점 사이의 거리에 100을 곱하고 있으므로 동일한 기준을 적용해야 한다.

    // sorted는 x축을 기준으로 정렬되어 있기 때문에,
    // mid를 기준으로 가까운 거리부터 최소 기준(min보다는 가까워야 함)을 만족할 때까지만 탐색을 하면 된다.
    while (
      rIdx < sorted.length &&
      Math.abs(midX - sorted[rIdx][1]) * 100 < min
    ) {
      rIdx++;
    }
    while (lIdx >= 0 && Math.abs(midX - sorted[lIdx][1]) * 100 < min) {
      lIdx--;
    }

    // while 탈출하기 위한 조건을 보면,
    // lIdx는 1을 더해야 하고, rIdx는 1을 줄여야 한다.
    // 아래 구간에 대해서 brute force를 적용한다.
    for (let i = lIdx + 1; i < rIdx; i++) {
      for (let j = i + 1; j < rIdx; j++) {
        min = Math.min(min, calculateDistance(sorted[i], sorted[j]));
      }
    }
    return min;
  };

  const closestFrom = (start, end, size, sorted) => {
    if (size <= 3) {
      // 최소 두 개 이상의 점이 있어야 거리를 계산할 수 있다.
      //  1) 모든 점의 개수가 4개일 경우, 각각 2개로 나눌 수 있다.
      //  2) 모든 점의 개수가 5개일 경우, 각각 2, 3개로 나눌 수 있다. 3개인 경우 더 나눌 수 없다.
      return bruteForce(start, end, sorted);
    }
    // 가운데를 기준으로 분할한 뒤 재귀적으로 문제를 해결한다.
    const mid = Math.floor((start + end) / 2);
    // 왼쪽, 오른쪽으로 나뉜 부분에서 각각 가장 가까운 두 점 사이의 거리를 구한다.
    const minLeft = closestFrom(start, mid, mid - start + 1, sorted);
    const minRight = closestFrom(mid + 1, end, end - mid, sorted);

    // 전체 영역에서 가장 가까운 두 점 사이의 거리는 아래 중 하나다.
    //  1) 위에서 구한 두 거리(minLeft, minRight)
    //  2) 가운데를 가로지르는 두 점 사이의 거리
    // 먼저 1)중에서 더 짧은 거리를 구한다. 최종 정답은 이보다 작거나 같아야 한다.
    let min = Math.min(minLeft, minRight);
    return closestCrossing(mid, sorted, min);
  };

  // x좌표를 기준으로 정렬한다.
  const sorted = mergeSort(points.slice(0), (item) => item[1]);
  return closestFrom(0, sorted.length - 1, sorted.length, sorted);
};
```
