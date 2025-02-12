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
```
