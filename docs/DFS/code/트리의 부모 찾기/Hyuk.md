## 동혁 코드

```js
// 제출
// const fs = require("fs");
// const input = fs.readFileSync("/dev/stdin").toString().trim().split("\n");

// 받아올 때
let input = require("fs")
  .readFileSync("baekjoon/inputs/s2-11725.txt")
  .toString()
  .split("\r\n");

const N = Number(input[0]);
const graph = {};
const visited = {};
const parents = new Array(N).fill(0);

for (let i = 1; i < N; i++) {
  const [a, b] = input[i].split(" ").map(Number);
  if (!graph[a]) graph[a] = []; // 인접 배열 존재 x
  if (!graph[b]) graph[b] = [];

  graph[a].push(b);
  graph[b].push(a);
}

function dfs(startNode) {
  visited[startNode] = true;

  for (let next of graph[startNode]) {
    if (!visited[next]) {
      parents[next - 1] = startNode;
      dfs(next);
    }
  }
}

dfs(1);

console.log(parents.slice(1).join("\n"));
```
