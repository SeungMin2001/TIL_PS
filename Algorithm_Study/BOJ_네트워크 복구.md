```py
import sys
#from queue import PriorityQueue
import heapq
#queue=PriorityQueue()
queue=[]
n,m=map(int,input().split())
dp=[int(1e9)]*(n+1)
result=[0]*(n+1)

check=[False]*(n+1)
heapq.heappush(queue,(0,1))
matrix=[[] for i in range(n+1)]
for i in range(m):
    a,b,c=map(int,input().split())
    matrix[a].append((b,c))
    matrix[b].append((a,c))
def dijkstra():
    dp[1]=0
    while queue:
        cost,node=heapq.heappop(queue)
        if cost>dp[node]:
            continue
        for val in matrix[node]:
            if dp[val[0]]>val[1]+cost:
                dp[val[0]]=val[1]+cost
                result[val[0]]=node  #현재 노드와 다음노드 저장
                heapq.heappush(queue,(dp[val[0]],val[0]))
dijkstra()
print(n-1)
for i in range(2,n+1):
    print(i,result[i])
```
<h1>느낀점</h1>
간단한 다익스트라 문제였는데 시간을 엄청 씀....
원인모를 런타임에러가 계속나서 한참을 찾다가 뭔가 PriorityQueue를 쓴게 의심되서
PriorItyQueue 대신 heapq를 사용했더니 바로 맞음 하.....
이유는 아직 내 레벨로써는 찾지 못하겠음 쨋든 앞으로 우선순위큐는 당분간 heapq를 사용하도록 하자.
문제는 다익스트라 알고리즘에서 dp table 갱신할때마다 그 노드와 연결되는 노드 이 두개의 노드를 계속 저장시켜준다음
마지막에 다 끝내고 두 노드를 다 출력하면 되는 문제였음
모든 노드를 다 지나면서 최소한의 경로만 출력하는 문제였기 때문에 다익스트라로 최소경로값 구해주고 다 구해짐과 동시에
나와 최소경로값으로 연결된 또다른 노드 이 두개를 쌍으로 저장했다가 출력하면 답이 되기 때문에 간단한 문제였음. 
