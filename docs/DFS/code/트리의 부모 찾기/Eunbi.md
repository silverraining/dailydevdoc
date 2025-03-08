## 은비 코드

```js
let input = require("fs")
  .readFileSync("./inputs/DFS-s2.txt")
  .toString()
  .split("\r\n");

// console.log(input);
/*
[
  '7',   '1 6',
  '6 3', '3 5',
  '4 1', '2 4',
  '4 7'
]
*/

/*
       1
      / \
     6   4
    /   / \
   3   2   7
  /
 5
 */

const N = Number(input[0]);
let graph = Array.from({ length: N + 1 }, () => []);

// 트리의 간선은 N-1개이므로 해당 줄만 처리
for (let i = 1; i <= N - 1; i++) {
  let [a, b] = input[i].split(" ").map(Number);
  graph[a].push(b);
  graph[b].push(a);
}

let parent = Array(N + 1).fill(0);
let visited = Array(N + 1).fill(false);

function dfsRecursive(node) {
  visited[node] = true;

  for (let next of graph[node]) {
    if (!visited[next]) {
      parent[next] = node;
      dfsRecursive(next);
    }
  }
}

dfsRecursive(1);

console.log(parent.slice(2).join("\n"));
```
