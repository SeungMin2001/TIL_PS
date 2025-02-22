```py
import sys
from collections import deque
sys.setrecursionlimit(100000)
t=int(sys.stdin.readline())
ans=0
def find(k,array):
    if array[k]==k:
        return k
    return find(array[k],array)
def union(a,b,array):
    a=find(a,array)
    b=find(b,array)
    if a<b:
        array[a]=b
    else:
        array[b]=a
def bfs(k,check):
    global ans
    queue=deque()
    check[k]=1
    queue.append(k)
    ans-=1
    while queue:
        now=queue.pop()
        for i in matrix[now]:
            if check[i]==0:
                check[i]=1
                queue.append(i)
                ans-=1
for _ in range(t):
    n=int(sys.stdin.readline())
    ans=n
    data=list(map(int,sys.stdin.readline().split()))
    matrix=[[] for _ in range(n+1)]
    array=[0]*(n+1)
    check=[0]*(n+1)
    for i in range(1,n+1):
        array[i]=i
    for i in range(n):
        matrix[i+1].append(data[i])
    for i in range(1,n+1):
        for j in matrix[i]:
            if i==j:
                ans-=1
            elif find(i,array)==find(j,array):
                bfs(i,check)
            else:
                union(i,j,array)
    print(ans)
```
<h1>느낀점</h1>
일단 보자마자 그래프 형태로 배열을 저장시킨후 사이클 발생시 사이클에 해당하는 노드들을 체크해주고 체크당한 노드들 개수를 전체개수에서 빼주면서 돌려주면 구할수 있겠다고 생각이 들었다.
그래서 union-find로 사이클을 검사해줬고 사이클 발견시 시작도느로부터 연결된 모든 노드들을 대상으로 BFS를 돌려주었고 거기서 체크되는 노드개수만큼 ans에서 -1 해주었다.
그리고 하나 예외처리를 해줘야했는데 예를들어 (3,3) 처럼 자기자신 좌표를 만났을 경우이다. 이 경우에는 bfs가 돌아가지 않으므로 그냥 ans-1 해주고 넘어가주었다.
이렇게 구현해주니 정답처리가 되었다.
