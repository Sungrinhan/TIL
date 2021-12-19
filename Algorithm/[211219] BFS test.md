## Question
The number of nodes n and a two-dimensional array with edges is given as a parameter.

Please write a function that returns how many nodes are farthest from node 1.

The furthest node is the node with the largest number of edges when moving to the shortest path.

### Input
Parameter 1: n
number of nodes
number type
Parameter 2: edge
Indicates the edge of each node.
Two-Dimensional Array
Each edges ([ a, b ]) of two-dimensional array are that there is an edge between node a and node b.
### Output
Your function should return an number type
### Constraints
The number of nodes n is more than 2
The edge is bidirectional and has at least one edge
The furthest node is the node with the largest number of edges when moving to the shortest path.
### I/O Example
```js
let edge = [[4,1],[3,4],[1,2],[2,3],[2,5],[5,3]]
let output = test1(5,edge);
console.log(output); // --> 2
```
- - - 
### SOLUTION

```js
function test1(n, edge) {
    return bfs(1, edge, n)
}

// 인자로 시작값, 탐색할 배열, 길이를 받는 BFS 함수 생성
const bfs = (start, arr, end) => {
     
    // 방문을 체크하는 배열을 만들어 준 후, 초기값으로 false를 넣어줍니다.
    // false를 넣어주는 이유는 아무 노드에도 방문하지 않았음을 표시하기 위함입니다.
    const isVisited = new Array(end + 1).fill(false);
    // 각각의 노드가 1번째 노드와 어느정도 거리에 있는지를 표시할 배열 입니다.
    // 초기값으로는 0을 넣어줍니다.
    const distanceArray = new Array(end +1).fill(0);
    // 큐에 start지점을 넣어줍니다.
    const queue = [start];
    // start지점에 방문했다는 표시로 true를 넣어줍니다.
    isVisited[start] = true;
    // 큐가 빌때 까지, 즉 모든 노드를 탐색 할때까지 반복문을 돌립니다.
    while(queue.length !== 0) {
    // 큐에서 탐색을 시작할 기준 노드를 꺼냅니다.
    const head = queue.shift();

    const distance = distanceArray[head] + 1
    // 배열을 돌면서 각 노드를 탐색합니다.
    // 양방향으로 모두 탐색해주어야 합니다. 
    for(let node of arr) {
        // node의 0번째 요소가 head이고 node의 1번째 요소를 방문하지 않았을 경우
        // 큐에 탐색해야할 노드를 넣어 줍니다.
        // 그 후 방문했다는 표시를(true)를 해주고 거리를 등록해줍니다.
        if(node[0] === head && !isVisited[node[1]]) {
            queue.push(node[1]);
            isVisited[node[1]] = true;
            distanceArray[node[1]] = distance
        // node의 1번째 요소가 head이고 node의 0번째 요소를 방문하지 않았을 경우
        // 큐에 탐색해야할 노드를 넣어 줍니다.
        // 그 후 방문했다는 표시를(true)를 해주고 거리를 등록해줍니다.
        } else if (node[1] === head && !isVisited[node[0]]) {
            queue.push(node[0]);
            isVisited[node[0]] = true;
            distanceArray[node[0]] = distance
       }
    }
 }
    // 1번 노드에서 가장 먼 거리를 변수에 저장합니다.
    const longestDistance = Math.max.apply(null, distanceArray);
    // filter를 사용하여 distanceArray의 longestDistance만 남겨둔 배열의 길이를 리턴해줍니다.
    return distanceArray.filter((el) => el === longestDistance).length
}
```
