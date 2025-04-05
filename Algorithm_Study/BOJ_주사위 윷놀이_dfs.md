```py
data=list(map(int,input().split()))
matrix=[0]*99
for i in range(1,21):
    matrix[i]=i*2
matrix[21]=13
matrix[22]=16
matrix[23]=19
matrix[24]=22
matrix[25]=24
matrix[26]=28
matrix[27]=27
matrix[28]=26
matrix[29]=25
matrix[30]=30
matrix[31]=35

# 1~20 / 5->21,22,23 / 10->24,25 / 15->26,27,28 / 23,25,28->29 / 29->30,31 / 31,19->20 / 20->32matrix[1~31]
key=0
def dfs(depth,chess,cnt):
    global key
    if depth==10:
        if key<cnt:
            key=cnt
        return
    for i in range(4):
        cur=chess[i]
        if cur==5:
            cur=21
        elif cur==10:
            cur=24
        elif cur==15:
            cur=26
        elif cur == 23 or cur == 25 or cur == 28:
            cur = 29
        elif cur==20:
            cur=33
        elif cur==31:
            cur=20
        else:
            cur+=1
        for _ in range(1,data[depth]):
            if cur>=33:
                break
            if cur==23 or cur==25 or cur==28:
                cur=29
            elif cur==31:
                cur=20
            elif cur==20:
                cur=33
                break
            else:
                cur+=1
        #print(cur)
        if cur==33 or (cur not in chess and cur<33):
            before=chess[i]
            chess[i]=cur
            dfs(depth+1,chess,cnt+matrix[cur])
            chess[i]=before

dfs(0,[0,0,0,0],0)
print(key)
```
<h1>느낀점</h1>
매우 어렵게 푼 문제.....
하루종일 붙들고 간신히 풀었다.
일단 처음에 BFS로 접근했다가 머리가 깨지는줄 알았다... queue에 인자값을 어떻게 넣어줘야할까, 갈림길 조건은 어떻게 해줘야할까 등등으로
그래서 DFS로 방향을 틀었다. 인자값으로는 현재 말에 좌표와 총 합 그리고 10번에 깊이체크용도 이렇게 3개를 넣어주었고
depth는 10이 되면 최댓값 비교하고 리턴해준다 입력데이터가 10개만 들어오기 때문에.
구조는 총 4개의 말을 반복문으로 접근하면서 각각 재귀함수를 파준다.
즉 (1,2,3,4)집합중 하나를 선택하는데 이걸 10번 반복하는 모든 경우의수에 접근하는것이다. 
이 문제는 조건넣어주는게 매우매우 중요하다. 일단 갈림길 3곳 5,10,15에서 멈췄을경우 방향을 틀어주는 조건이 들어가줘야한다.
그리고 19,24,26 다음 25로 갈수있게 조건을 넣어줘야하고 마지막 35와 38 다음 40이 올수있게 하는 조건도 넣어줘야한다 그다음
갈 좌표에 다른 말이 있으면 못가기때문에 이것도 체크해줘야한다. 추가로 도착좌표를 33이라고 놓고 33에는 말이 중복으로 존재할수도 있다.
그리고 도착한말 즉 33에 위차한 말은 더이상 움직이지 못한다. 이 조건들을 전부 추가해줘야 정상적으로 코드가 돌아간다.
하나라도 조건이 빠지면 이상한 값이 나와버린다.<br><br><br>
<b>이 문제는 삼성 코딩테스트 기출문제였다...... 그래서 어려웠던것...</b>
