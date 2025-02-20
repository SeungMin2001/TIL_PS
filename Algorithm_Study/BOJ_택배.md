```py
import sys
sys.setrecursionlimit(100000)
n,m=map(int,sys.stdin.readline().split())
INF=int(1e9)
matrix=[[INF]*(n+1) for _ in range(n+1)]
ans=[[0]*(n+1) for _ in range(n+1)]
key=[0]*(n+1)
for i in range(m):
    a,b,c=map(int,sys.stdin.readline().split())
    matrix[a][b]=c
    matrix[b][a]=c
    ans[a][b]=b
    ans[b][a]=a
for i in range(1,n+1):
    matrix[i][i]=0
    ans[i][i]=INF

def find(start,end):
    if ans[start][end]==end:
        return end
    return find(start,ans[start][end])

for k in range(1,n+1):
    for i in range(1,n+1):
        for j in range(1,n+1):
            if matrix[i][j]>matrix[i][k]+matrix[k][j]:
                if i==k or j==k or i==j:
                    continue
                matrix[i][j]=matrix[i][k]+matrix[k][j]
                if find(i,k)==None:
                    print(i,j,k)
                ans[i][j]=find(i,k)

for i in range(1,n+1):
    for j in range(1,n+1):
        if ans[i][j]==INF:
            print('-',end=' ')
        else:
            print(ans[i][j],end=' ')
    print()

```
<h1>느낀점</h1>
플로이드 워셜 알고리즘 문제였다. 한 노드가 나머지 노드에 대한 최단경로를 전부 가져야하는데 모든 노드가 이를 만족해야한다.
여기에 조건 하나가 추가되야하는데 예를들어 1->5->6 에 경로가 최단경로일때 (1,6)에 해당하는 값은 5가 나와야 한다.
즉 최단경로가 구해질때 어떤 애를 거쳐서 왔냐? 를 묻는 문제였는데 여기서 더 나아가면 최단경로 안에서 거쳐진 노드들이 많을수도 있는데
이중 가장 먼저 지나온 애를 출력해줘야한다. 예를들어 최단경로중 하나가 1->5->6->7 일때 (1,7)에 값은 5가 나와야 한다는 것이다.
그래서 유니온파인드에서 쓰인 find함수를 그대로 사용함으로써 처음으로 지나온 노드를 구해서 ans에 넣어줬더니 바로 문제가 풀렸다.
find()함수를 쓸 생각을 했던게 핵심 포인트였던것 같다.
