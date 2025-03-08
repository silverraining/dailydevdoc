## 새하 코드

```js
// var input = require("fs").readFileSync("/dev/stdin").toString().trim().split("\n");
let input = require("fs")
  .readFileSync("DFS/inputs/s2-11725.txt")
  .toString()
  .split("\r\n");

/*
console.log(input)

[
  '7',   '1 6',
  '6 3', '3 5',
  '4 1', '2 4',
  '4 7'
]
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

// DFS를 재귀로 구현 (대형 입력의 경우 스택 오버플로우 주의)
function dfsRecursive(node) {
  visited[node] = true;

  for (let next of graph[node]) {
    if (!visited[next]) {
      parent[next] = node;
      dfs(next);
    }
  }
}

function dfsStack(node) {
  let stack = [node];

  while (stack.length > 0) {
    let pop = stack.pop();
    if (visited[pop]) continue;

    visited[pop] = true;
    for (let g of graph[pop]) {
      if (visited[g]) continue;
      parent[g] = pop;
      stack.push(g);
    }
  }
}

// dfsRecursive(1);
dfsStack(1);

for (let i = 2; i <= N; i++) {
  console.log(parent[i]);
}
// console.log(parentsArr.slice(2).join("\n"));
```
