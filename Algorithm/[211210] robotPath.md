A robot located at the top left corner of a 5x5 grid is trying to reach the bottom right corner. The robot can move either up, down, left, or right.
but cannot visit the same spot twice. How many possible unique paths are there to the bottom right corner?

make your solution work for a grid of any size.

// A Board class will be useful

- - -

### MINE

너무 어려워서 못풀었다... 답을보고 수도코드로 작성해보았다.
```js
function makeBoard(n) {
  let board = [];
  
  for (let i = 0; i < n; i++) {
    board.push([]);
    for (let j = 0; j < n; j++) {
      board[i].push(false);
    }
  }
  // false 로 가득한 보드를 만드는 함수

  board.togglePiece = function(i, j) {
    this[i][j] = !this[i][j];
  }; // this[i][j] false => true

// 방문했다는 표시를 위해 false => true 로 바꿔주는 토글피스 함수
  board.hasBeenVisited = function(i, j) {
    return !!this[i][j];
  };

  return board;
}
// hasbeenvisited 함수가 무엇 인지를 잘 모르겠다.


function robotPaths(n, board, i, j) {
  // your code here
  // 문제에서  보드가 있다고 했으니 보드를 만든다. make solution work for a grid of any size.
  
    // Initialize these if not provided
  if (!board) {
    board = makeBoard(n);
    i = 0;
    j = 0;
  }
  // No possible paths if you’re off the board
  // or on a piece you shouldn’t be on
  if (!(i >= 0 && i < n && j >= 0 && j < n) || board.hasBeenVisited(i, j)) {
    return 0;
  }
  // i,  j 가 0보다 작거나, 보드의 범위를 벗어났거나 혹은 방문을 했던곳이라면 => 0을 출력한다.
  
  // One possible path if you’re at the
  // end point (the path that led there)
  if (i === n - 1 && j === n - 1) {
    return 1;
  }
  //엔드포인트라면 엔드포인트로 가는 길은 1개이다.
  
// 0[true true false] i row, j col
// 1[true false false]
// 2[false false false]

  board.togglePiece(i, j); // 현재 있는곳을 false 로 바꿔준다.
  // 위치는 위,아래, 왼쪽,오른쪽으로 이동이 가능하므로, 현재위치에서 갈수있는방향 + 한칸 이동했을때 그위치에서 갈수있는 길의 개수를 재귀함수를 통해 합산한다.
  
  let result = robotPaths(n, board, i, j + 1) +
    robotPaths(n, board, i, j - 1) +
    robotPaths(n, board, i + 1, j) +
    robotPaths(n, board, i - 1, j);
    
  // !!Return the board to its original state!!
  // Toggling the piece back to its original state
  // is vital to this solution, as it allows the
  // algorithm to 'backtrack' from this position for
  // subsequent recursive calls.

  board.togglePiece(i, j);
  //여기서 이해가 안갔던 부분중 하나이다. 일단 [i][j] 위치에서 갈 수 있는 길의 개수를 구하면, 보드를 초기상태로 돌려야 한다. 왜냐? result에서는 4방향에서의 다음 재귀함수가 진행되는데
  // 만약 togglePiece 함수로 인해서 초기화가 되지않으면 방문하지 않았지만 재귀함수로 인해 true 로 바뀌는 위치가 있기 때문이다. 

  return result;
  /* END SOLUTION */
};

```
