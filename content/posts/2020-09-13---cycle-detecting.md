---
title: "[Algorithm] Cycle Detecting"
date: "2020-09-13T22:40:32.169Z"
template: "post"
draft: false
slug: "why-v-dom"
category: "Javascript"
tags:
  - "Javascript"
  - "React"
  - "Web Development"
description: "가상 돔은 정말 빠를까 ? 가상 돔이 필요한 이유 ?"
socialImage: ""
---

## DFS를 이용한 방법

backedge: 자기 자신 또는 자기 자신의 부모로 향하는 엣지

backedge를 찾는다 ⇒ DFS 재귀 함수를 수행하면서 한번 방문한 노드인데, 그 함수가 리턴되기 전에 그 노드를 또 방문하게 된다면, cycle이 존재하는 것! 

isCyclic 재귀함수 내부에서

- current node를 visited로 체크한 후, recursion stack 배열에 체크한다
- current node에 인접하고, 방문되지 않은 모든 node를 가지고 같은 재귀 함수를 수행한다
    - 여기서 true를 리턴하는 노드가 있으면 true를 리턴한다
- current node에 인접하고, 방문되었고, recursion stack에 들어있는 노드가 있으면 true를 리턴한다
    - 이미 방문 되었다는 건 그 노드에 대해 dfs 가 수행되었다는 뜻인데, 그 이후에도 recursion stack에 들어가 있다는 건 아직 그 dfs가 리턴되지 않은 상태에서 또 다시 방문하게 된 것 ⇒ cycle 존재한다는 것
- recursion stack에서 current node를 뺀다 (false로 바꾼다)

```jsx
// 사이클 없는 그래프인지 판단하기 위한 함수
public boolean isValid(int n, int[][] edges){
	boolean[][] adj = new boolean[n][n];
	// edge 처리
	// adj 처리
	...

	boolean[] visited = new boolean[n];
	boolean[] stack = new boolean[n];
	for(int i=0; i<n; i++){
		if(!visited[i] && isCyclic(adj, i, visited, stack) return false;
	}
	return true;
}

boolean isCyclic(boolean[][] adj, int i, boolean[] visited, boolean[] stack){
	visited[i] = true;
	stack[i] = true;
	for(int j=0; j < adj[i].length; j++){
		if(!visited[j]) {
			if(isCyclic(adj, j, visited, stack) return true;
		} else if(stack[i]) return true;
	}
	stack[i] = false;
	return false;
}
```

## BFS를 이용한 방법

### 1) with topological sort

Topological Sorting을 함께 이용한다 ⇒ 노드 별 유입 edge의 개수를 추적해야한다

사이클이 있다면, topological sort를 수행하여 노드를 방문했을 때 방문되지 않고 남아있는 노드가 존재할 것이다.

사이클이 있는 경우 모든 노드를 다 방문해도 유입 엣지가 지워지지 않는 노드가 있을 것이기 때문!

즉, `(number of vertices present in the topological ordering) != total number of vertices present in the graph` 이면 사이클이 존재할 것이다. 

```java
HashMap<Integer, Set<Integer>> adjList = new HashMap<>();
//adj 및 edgeCount 처리 되었다고 가정, edgeCount는 유입엣지

visitedCount = 0;

for(int i=0; i<n; i++){
	if(edgeCount[i] == 0) queue.add(i);
}

while(!queue.isEmpty()){
	int curr = queue.poll();
	visitedCount ++;
	Set<Integer> adj = null;
	if(adjList.containsKey(curr)) {
		adj = adjList.get(curr);
		// 인접한 노드들 
		for(int num: adj){
			edgeCount[num]--; //curr에서 num으로 유입되는 엣지 지움
			if(edgeCount[num] == 0) queue.add(num);
		}
	}

return visitedCount == n;
```

### Kruskal Algorithm 이용

방문되지 않은 노드들 중 최단 거리의 edge를 가진 노드들, 즉 다음에 방문할 노드 u,v가 같은 root를 가지고 있다면 사이클이 있는 것

(u, v)가 없다고 가정한 상황인데, 이미 두 집합의 루트가 같다

 = root → u, u → root, v → root, root → v가 다 존재한다 (undirected graph)

⇒ u → v가 추가되면 v → u → v 의 path가 만들어진다 ⇒ 사이클이 생긴다 

즉, **두 집합의 FIND 연산 결과가 같으면 두 집합이 연결되어 있다**

```java
for each unvisited edge (u, v) in E
{
    if(Find(u) = Find(v)) // u and v belong to the same set already
    {
        print "Cycle Detected";
        break;
    } else {
        Union(u, v); // put u and v in the same set
    }
}
```