```py
import sys ,heapq, math
queue=[]
n,m=map(int,input().split())
matrix=[[]*(m+1) for i in range(n+1)]
for i in range(m):
    a,b,c=map(int,input().split())
    matrix[a].append((b,c))
    matrix[b].append((a,c))
start1,start2=map(int,input().split())
def dijkstra(node):
    dp=[int(1e9)]*(n+1)
    heapq.heappush(queue,(0,node))
    dp[node]=0
    while queue:
        cost,cur=heapq.heappop(queue)
        if dp[cur]<cost:
            continue
        for i in matrix[cur]:
            val=i[1]+cost
            if dp[i[0]]>val:
                heapq.heappush(queue,(val,i[0]))
                dp[i[0]]=val

    return dp

v1=dijkstra(start1)
v2=dijkstra(start2)
answer=[]
answer2=[]
for x in range(1,n+1):
    data=v1[x]+v2[x]
    if x==start1 or x==start2:
        continue
    if data>=int(1e9):
        continue
    answer.append((data,x))
answer.sort()

for i in range(len(answer)):
    if answer[0][0]==answer[i][0]:
        if v1[answer[i][1]]<=v2[answer[i][1]]:
            answer2.append((v1[answer[i][1]],answer[i][1])) # key point(v1[answer[i][1]] 같이 넘겨주기)

answer2.sort()

if answer2:
    print(answer2[0][1])
else:
    print(-1)

```
<h1>느낀점</h1>
다익스트라 알고리즘 응용문제
그냥 다익스트라 두번 돌려서 각각 두개의 거리테이블 만들어주고 그 테이블 가지고 놀면 풀리는 문제였는데..
하나를 못찾아서 시간이 조금 걸렸던 문제.. 주석으로 key point라고 써놓은 구간인데
조건중 하나인 여러개의 후보들이 나왔을때 지헌과 가장 가까운 애로 선정해라 라는 조건을 보고 거리로 비교를 해야하는데
무의식적으로 노드번호로 가장 가까운 애를 선정해버렸다. 이거 한참 찾았다... 
노드번호가 아니라 거리가 가장 가까운애를 넘겨줘야 하므로 v1 거리테이블로 찾았어야 답이 나왔던 문제
난이도 자체는 평이했던것 같다.
