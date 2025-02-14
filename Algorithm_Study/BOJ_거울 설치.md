```py
from collections import deque
from sys import stdin
input=stdin.readline
n=int(input())
queue=deque()
start=[]
matrix=[[] for _ in range(n+2)]
for i in range(n):
    data=list(input())
    matrix[i] = data
for i in range(n):
    for j in range(n):
        if matrix[i][j]=='#':
            start.append((i,j))

def go(x,y,direction):
    ans=[]
    if direction=='down':
        for i in range(x+1,n):
            if i == start[1][0] and y == start[1][1]:
                return 999
            if matrix[i][y]=='!':
                ans.append((i,y))
            if matrix[i][y]=='*':
                break
    if direction == 'up':
        for i in range(x-1,-1,-1):
            if i == start[1][0] and y == start[1][1]:
                return 999
            if matrix[i][y]=='!':
                ans.append((i, y))
            if matrix[i][y]=='*':
                break
    if direction == 'left':
        for i in range(y-1,-1,-1):
            if x == start[1][0] and i == start[1][1]:
                return 999
            if matrix[x][i]=='!':
                ans.append((x,i))
            if matrix[x][i]=='*':
                break
    if direction == 'right':
        for i in range(y+1,n):
            if x==start[1][0] and i==start[1][1]:
                return 999
            if matrix[x][i]=='!':
                ans.append((x,i))
            if matrix[x][i]=='*':
                break

    return ans
last=100000000
def bfs(res):
    check = [[0] * (n + 2) for _ in range(n + 2)]
    global last
    if res==1: queue.append((start[0][0], start[0][1], 'up', 0))
    if res==2: queue.append((start[0][0], start[0][1], 'down', 0))
    if res==3: queue.append((start[0][0], start[0][1], 'left', 0))
    if res==4: queue.append((start[0][0], start[0][1], 'right', 0))
    check[start[0][0]][start[0][1]]=1
    while queue:
        a,b,key,cnt=queue.pop()
        new=go(a,b,key)
        if new==999:
            if last>cnt:
                last=cnt
            continue
        if len(new)==0:
            continue
        for k in range(len(new)-1,-1,-1):
            x,y=new[k]
            if check[x][y]==0 or check[x][y]>cnt:
                check[x][y]=cnt
                if key=='up' or key=='down':
                    queue.append((x, y, 'left', cnt + 1))
                    queue.append((x, y, 'right', cnt + 1))
                if key=='left' or key=='right':
                    queue.append((x, y, 'up', cnt + 1))
                    queue.append((x, y, 'down', cnt + 1))
for i in range(1,5):
    bfs(i)
print(last)
```
<h1>느낀점</h1>
골3 치고는 생각보다 빡셌음....
일단 BFS로 접근했고 현재노드->다음노드 이 과정에서 방향이 위,아래였다면 다음노드에 왼,오 를 저장 반대일경우 위,아래 저장
이러는 이유는 거울조건이 45도 기울어졌다고 나오기 때문. 즉 오는 방향에 수직방향으로 두갈래만 갈수있음
이걸 전부 queue에 담고 BFS돌리면서 cnt최소인 지점 찾으면 풀리는 문제였는데
내가 아무리 반례를 찾아서 돌리고 생쇼를 해도 틀렸던 이유가 check부분이였음.....
일단 check를 무조건 해야함. 무한사이클이 생기기 떄문에. 단 check를 일반 bfs처럼 해버리면 최솟값 못찾음
그래서 ans.append를 reverse를 해서 돌렸더니 모든 반례는 통과하는데 계속 틀렸다고 나오는거임. 그래서 check논리중 어딘가 틀린게 존재하다고 생각해서
아에 논리를 바꿈
0,1값으로 넣어주는게 아니라 cnt값을 넣어주고 check값이 0이거나 현재 cnt가 기존에 check값보다 작다면 통과시켜주는거임
이러면 최솟값갱신+check 두개의 기능을 동시에 해줄수 있기 때문에 정답처리 됬음
