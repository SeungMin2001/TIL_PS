```py
matrix=[[] for _ in range(9)]
ans=[]
for i in range(9):
    data=list(map(int,list(input())))
    matrix[i]=data
    for j in range(9):
        if matrix[i][j]==0:
            ans.append((i,j))
def find(x,y): #3*3 9개의 영역중 어딘지 파악
    if x<=2:
        if y<=2:
            return 0,0
        elif y <=5:
            return 0,3
        else:
            return 0,6
    elif x<=5:
        if y <= 2:
            return 3,0
        elif y <= 5:
            return 3,3
        else:
            return 3,6
    else:
        if y <= 2:
            return 6,0
        elif y <= 5:
            return 6,3
        else:
            return 6,6

def check1(x,y,key): #3*3 영역 검사
    a,b=find(x,y)
    for i in range(a,a+3):
        for j in range(b,b+3):
            if key==matrix[i][j]:
                return False
    return True


def check2(x,y,key): # 세로줄,가로줄 검사
    for i in range(9):
        if key==matrix[i][y]:
            return False
    for i in range(9):
        if key==matrix[x][i]:
            return False
    return True

def dfs(ind):
    if ind==len(ans):
        for m in range(9):
            for n in range(9):
                print(matrix[m][n],end='')
            print()
        exit(0)
    x=ans[ind][0]
    y=ans[ind][1]
    for i in range(1,10):
        if check1(x,y,i)==True and check2(x,y,i)==True:
            matrix[x][y]=i
            dfs(ind+1)
            matrix[x][y]=0

dfs(0)

```
<h1>느낀점</h1>
간단한 백트래킹 문제
이 문제에 핵심은 주어진 좌표를 기준으로 3*3과 세로, 가로에서 중복된게 있는지 체크만 잘 구현해준다면 쉽게 풀리는 문제다.
