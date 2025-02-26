```py
import sys
from collections import deque
t=int(sys.stdin.readline())
def topological(indegree,matrix,n,dp,key):
    queue=deque()
    ans=[]
    queue.append(1)
    for i in range(1,n+1):
        if indegree[i]==0:
            queue.append(i)
            dp[i]=data[i]
    while queue:
        now=queue.pop()
        ans.append(now)
        for i in matrix[now]:
            dp[i]=max(dp[now]+data[i],dp[i])
            indegree[i]-=1
            if indegree[i]==0:
                queue.append(i)
    return dp[key]

for _ in range(t):
    n,k=map(int,sys.stdin.readline().split())
    data=list(map(int,sys.stdin.readline().split()))
    data.insert(0,0)
    matrix=[[] for _ in range(n+1)]
    indegree=[0]*(n+1)
    for i in range(k):
        a,b=map(int,sys.stdin.readline().split())
        matrix[a].append(b)
        indegree[b]+=1
    key=int(sys.stdin.readline())
    dp = [0] * (n + 1)
    print(topological(indegree,matrix,n,dp,key))
```
<h1>느낀점</h1>
위상정렬 + dp문제 였는데 처음에 그냥 생각나는대로 얕은생각으로 이것저것 코드짜서 해봤는데 당연히 실패
그래서 위상정렬로 방향을 틈
위상정렬 구하는건 쉬움
이제 여기에 dp를 응용해야하는데 위상정렬을 구하면서 indegree 즉 전입차수가 0인애를 발견하면 dp계산을 바로 해주면 됨
현재 dp값과 방금 들어온 경로의 Dp값 두개중 큰 애를 넣어주면 되는데 방금 들어온 애는 data값 + 전 노드에 dp값이 됨
이런 점화식을 갖고 위상정렬을 돌린뒤 문제에서 주어진 노드에 해당하는 dp값을 출력하면 끝. 
