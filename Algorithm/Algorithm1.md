# BFS & DFS

### 그래프를 탐색하는 방법에는 크게 BFS(Breadth First Search), DFS(Depth First Search)의 2가지가 있다.

## 1) BFS(Breadth First Search)
+ 현재 정점에서 갈 수 있는 모든 정점들을 탐색하는 방식
+ Queue를 사용
+ 정점들을 Queue에 push할 때 아직 방문하지 않은 경우 push
+ Queue에 push하는 순간 방문한 정점으로 체크
+ 만약, 그래프의 간선의 가중치가 없거나 모두 1이라면 최단 경로를 찾아주는 알고리즘이 된다.(예를 들어 출발점에서 동서남북 이동이 가능하여 도착점까지의 최단 경로 구하는 문제)

##### Pseudo-code

```c
void BFS(){
  Initialize Q queue to be empty
  Q.push(시작점)
  visit[시작점]=True
  while(!Q.empty()){
    now=Q.pop()
    for(vertex next: adjacent to now){
      if(visit[next]==False){
        Q.push(next)
        visit[next]=True
      }
    }
  }
}
```

## 2) DFS(Depth First Search)
+ 현재 정점에서 끝까지 갈 수 잇는 정점까지 먼저 깊게 탐색하는 방식
+ 일반적으로 재귀함수를 사용하여 구현하며 Stack을 사용하여 구현하기도 한다.
+ 정점들을 Stack에 push할 때 아직 방문하지 않은 경우 push
+ Stack에서 pop되는 순간 방문한 정점으로 체크

##### Pseudo-code(Stack)

```c
void DFS(){
  Initialize S stack to be empty
  S.push(시작점)
  while(!S.empty()){
    now=S.pop()
    visit[now]=True
    for(vertex next: adjacent to now){
      if(visit[next]==False){
        S.push(next)
      }
    }
  }
}
```

##### Pseudo-code(재귀)

```c
void DFS(vertex now){
  visit[now]=True
  for(vertex next: adjacent to now){
    if(visit[next]==False){
      DFS(next)
    }
  }
}
```
