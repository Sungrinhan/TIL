## largestRectangularArea
### 문제
히스토그램(histogram)은 표(도수 분포표, 빈도표)로 되어 있는 도수 분포(frequency distribution)를 정보 그림으로 나타낸 것입니다. 예를 들어, 대학교의 한 학과에서 신입생들의 현재 거주 지역을 조사한 결과가 다음과 같다고 가정해 봅시다.

서울 2명, 경기 1명, 대전 4명, 부산 5명, 대구 1명, 광주 3명, 제주도 3명...
이 자료를 히스트그램으로 나타내면 각각 높이 2, 1, 4, 5, 1, 3, 3인 직사각형이 왼쪽부터 그려지게 됩니다. 편의상 직사각형의 너비는 1이라고 가정합니다. 이를 그림으로 나타내면 아래와 같습니다.

6 |
5 |       x
4 |     x x
3 |     x x   x x
2 | x   x x   x x
1 | x x x x x x x
------------------
이 히스토그램 내에서 만들 수 있는 가장 큰 직사각형의 면적은 8입니다 (O로 표시한 부분).

6 |
5 |       x
4 |     O O
3 |     O O   x x
2 | x   O O   x x
1 | x x O O x x x
------------------
이처럼 임의의 히스토그램 내에서 가장 큰 직사각형의 면적을 리턴해야 합니다.

### 입력
인자 1 : histogram
number 타입을 요소로 갖는 배열
histogram[i]는 100,000 이하의 양의 정수
histogram.length는 100,000 이하
### 출력
number 타입을 리턴해야 합니다.
### 입출력 예시
```js
let histogram = [2, 1, 4, 5, 1, 3, 3];
let output = largestRectangularArea(histogram);
console.log(output); // --> 8

let histogram = [6, 2, 5, 4, 5, 1, 6];
let output = largestRectangularArea(histogram);
console.log(output); // --> 12
/*
6 | x           x
5 | x   x   x   x
4 | x   O O O   x
3 | x   O O O   x
2 | x x O O O   x
1 | x x O O O x x
------------------
*/
```

- - -

### Solution
```js
onst largestRectangularArea = function (histogram) {
  const createMinIdxTree = (arr, ts, te) => {
    // 가장 작은 값의 '인덱스'를 구하기 위한 구간 트리
    if (ts === te) return { idx: ts, val: arr[ts] };

    const mid = parseInt((ts + te) / 2);
    const left = createMinIdxTree(arr, ts, mid);
    const right = createMinIdxTree(arr, mid + 1, te);

    return {
      val: Math.min(left.val, right.val),
      idx: left.val < right.val ? left.idx : right.idx,
      left,
      right,
    };
  };
  const tree = createMinIdxTree(histogram, 0, histogram.length - 1);

  const getMinIdx = (ts, te, rs, re, tree) => {
    if (rs <= ts && te <= re) return tree.idx;
    if (te < rs || re < ts) return rs;

    const mid = parseInt((ts + te) / 2);
    const left = getMinIdx(ts, mid, rs, re, tree.left);
    const right = getMinIdx(mid + 1, te, rs, re, tree.right);
    return histogram[left] < histogram[right] ? left : right;
  };

  const getRangeArea = (start, end) => {
    if (start > end) return 0;
    // 현재 구간에서 가장 작은 막대를 찾는다.
    // 가장 작은 막대이므로 구간의 길이 * 높이만큼의 직사각형을 만들 수 있다. (첫번째 후보)
    const minIdx = getMinIdx(0, histogram.length - 1, start, end, tree);

    // 가장 작은 막대를 기준으로 왼쪽, 오른쪽 부분에 존재하는 모든 막대의 높이가 더 크다.
    // 재귀적으로 왼쪽 부분과 오른쪽 부분,
    // 즉 해당 구간에서 가장 작은 막대를 제외해서 만들 수 있는 가장 큰 직사각형의 넓이를 구한다.
    return Math.max(
      (end - start + 1) * histogram[minIdx], // 첫번째 후보
      getRangeArea(start, minIdx - 1),
      getRangeArea(minIdx + 1, end)
    );
  };

  return getRangeArea(0, histogram.length - 1);
};
```
