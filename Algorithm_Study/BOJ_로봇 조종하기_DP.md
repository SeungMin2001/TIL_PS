```py
# dp,bfs 2가지 방법
#-----------bfs----------------
# from collections import deque
# X=[0,1,0] # right,down,left
# Y=[1,0,-1]
# queue=deque()
# check=[[0]*(m+1) for _ in range(n+1)]
# queue.append((1,1,matrix[1][1]))
# key=-1000000000
# check[1][1]=1
# while queue:
#     x,y,cnt=queue.pop()
#     print(matrix[x][y])
#     if key<cnt:
#         key=cnt
#     for i in range(3):
#         a=x+X[i]
#         b=y+Y[i]
#         if a>n or b>m or a<1 or b<1:
#             continue
#         if check[a][b]==0:
#             check[a][b]=1
#             queue.append((a,b,cnt+matrix[a][b]))
# print(key)
# ----------------- check 관련 문제 해결 불가. ---------
#----------------dp-----------------
n,m=map(int,input().split())
matrix=[[] for _ in range(n+1)]
ins=[]
dp=[[-999]*(m+1) for _ in range(n+1)]

a=b=c=0

for _ in range(m+1):
    ins.append(0)
matrix[0]=ins
for i in range(1,n+1):
    matrix[i]=list(map(int,input().split()))
    matrix[i].insert(0,0)

for i in range(1,m+1): # first line
    if i==1:
        dp[1][i]=matrix[1][i]
    else:
        dp[1][i]=matrix[1][i]+dp[1][i-1]
for i in range(2,n+1):
    t1=[0]*(m+1)
    t2=[0]*(m+1)
    for j in range(1,m+1):# ->
        if j==1:
            t1[j]=matrix[i][j]+dp[i-1][j]
        else:
            t1[j]=matrix[i][j]+max(dp[i-1][j],t1[j-1])
    for k in range(m,0,-1):# <-
        if k==m:
            t2[k]=max(dp[i][k],matrix[i][k]+dp[i-1][k])
        else:
            t2[k]=max(matrix[i][k]+dp[i-1][k],matrix[i][k]+t2[k+1])
    for r in range(1,m+1):
         dp[i][r]=max(t1[r],t2[r])
# for i in range(n+1):
#     print(dp[i])
print(dp[n][m])
```
<h1>느낀점</h1>
일단 처음에 든 생각은 DP,BFS 두가지 방안이 떠올랐다.
그래서 BFS로 처음 접근해봤는데 check부분에서 막혔다. 즉 방문처리를 해주는 과정에서 뭔가 계속 잘 안됬다. 이 문제와 BFS의 논리가 틀렸던것같다.
그래서 DP로 풀기로 하였다. 처음에는 이중포문으로 단순히 돌면서 DP를 계산해줬는데 생각해보니 다른 경우의 수도 발생할수 있다는것을 알았다. 예를들어
5 5칸일때 1,5 -> 2,1로 갈텐데 여기서 계산되는건 max(1,5) 하나밖에 없기때문에 2,1입장에서는 1,1에서 아래로 내려오는 경우의수만 저장된다. 하지만
1,1 -> 1,2 -> 2,2 -> 2,1 이렇게 돌아서 오는 경우도 충분히 가능하기때문에 dp계산을 단순히 하면 안된다고 생각했다.
그래서 첫번째칸은 어처피 오른쪽으로밖에 못가니까 한가지방향으로 계산때리고<br>
두번째 라인부터는 왼쪽으로 간거,오른쪽으로 간거 두개를 돌려서 각각의 좌표값중 더 큰 값을 넣어주기로 했다.
이렇게 해주면 최고로 높은 값들이 저장될수 있기때문에 정답을 맟출수 있었다.
