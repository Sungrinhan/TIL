Take a two-dimensional array(i.e., an array containing many arrays of equal length) and return all the values in the array.

### Constraints:
The spiral turns clockwise (start left -> right).
All elements of an array contain only numbers.
Empty arrays are not entered.
Based on the entire two-dimensional array, there are no identical elements(the same number).

example:
```js
spiralTraversal([
  [1,2,3],
  [4,5,6],
  [7,8,9]
]);

returns [1, 2, 3, 6, 9, 8, 7, 4, 5]
```


- - -

### MINE
```js
function test3(matrix) {
  // 각 방향마다 row와 col의 변화를 저장
  const RIGHT = [0, 1];
  const DOWN = [1, 0];
  const LEFT = [0, -1];
  const UP = [-1, 0];
  // 각 방향을 위한 lookup table
  const MOVES = [RIGHT, DOWN, LEFT, UP];
  const M = matrix.length;
  const N = matrix[0].length;
  const isValid = (row, col) => row >= 0 && row < M && col >= 0 && col < N;

  let cnt = 0;
  let row = 0,
    col = -1;
  let direction = 0;
  let result = [];
  while (cnt < M * N) {
    const move = MOVES[direction];
    const [rd, cd] = move;

    row = row + rd;
    col = col + cd;
    while (isValid(row, col) && matrix[row][col] !== false) {
      result.push(matrix[row][col]);
      // 한 요소를 두 번 접근하지 않게 하기 위해서, 접근된 요소를 false로 변경한다.
      matrix[row][col] = false;
      row = row + rd;
      col = col + cd;
      cnt++;
    }
    // row, col 이 행렬의 범위를 벗어났기 때문에,
    // 진행된 방향의 반대로 한 칸 이동한다.
    row = row - rd;
    col = col - cd;

    // 각 방향이 순환되기 때문에 모듈러 연산을 사용한다.
    direction = (direction + 1) % 4;
  }
  return result;
}
```
- - -
### OTHERS
```js
function test3(matrix) {

  // TODO: Implement me!
  /* START SOLUTION */
  let results = [];
  let startRowIndex = 0;
  let endRowIndex = matrix.length - 1;
  let startColIndex = 0;
  let endColIndex = matrix[0].length - 1;

  while (startRowIndex <= endRowIndex && startColIndex <= endColIndex) {

    for (let i = startColIndex; i <= endColIndex; i++) {
      results.push(matrix[startRowIndex][i]);
    }
    startRowIndex++;

    for (let j = startRowIndex; j <= endRowIndex; j++) {
      results.push(matrix[j][endColIndex]);
    }
    endColIndex--;

    if (startRowIndex <= endRowIndex) {
      for (let k = endColIndex; k >= startColIndex; k--) {
        results.push(matrix[endRowIndex][k]);
      }
      endRowIndex--;
    }

    if (startColIndex <= endColIndex) {
      for (let m = endRowIndex; m >= startRowIndex; m--) {
        results.push(matrix[m][startColIndex]);
      }
      startColIndex++;
    }

  }

  return results;
  /* END SOLUTION */
};
```
