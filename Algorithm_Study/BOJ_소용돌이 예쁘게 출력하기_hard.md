```py
r1,c1,r2,c2=map(int,input().split()) #r1,c1,r2,c2
#1 ,3 ,5 (2n-1)
#2 ,4 ,6 (2n)
#2 ,4 ,6 (2n)
#3 ,5 ,7 (2n+1)
if r1==0 and r2==0 and c1==0 and c2==0:
    print(1)
    exit(0)
val=max(abs(r1),abs(c1),abs(r2),abs(c2))
#리스트로 구현 범위가 -5000부터 5000이므로 대략 5001,5001을 0,0으로 놓고 계산하면 됨
# 2n+1(val==n)
matrix=[]
mmm=0
a=(2*val+1)*(2*val+1)
cnt=0
x,y=0,0
if r1<=x<=r2 and c1<=y<=c2:
    matrix.append((x,y,1))
    mmm+=1
y+=1
if r1 <=x<=r2 and c1<=y<=c2:
    matrix.append((x,y,2))
    mmm+=1
key=3
n=1
sss=0

num=((r2-r1)+1)*((c2-c1)+1)
while True:
    for i in range(2*n-1):# Up
        x-=1
        if r1<=x<=r2 and c1<=y<=c2:
            matrix.append((x,y,key))
            mmm+=1
        key = int(key) + 1
    if mmm>=num:
        break
    for i in range(2*n):  #Left
        y-=1
        if r1<=x<=r2 and c1<=y<=c2:
            matrix.append((x, y, key))
            mmm+=1
        key = int(key) + 1
    if mmm>=num:
        break
    for i in range(2*n):  #Down
        x+=1
        if r1<=x<=r2 and c1<=y<=c2:
            matrix.append((x, y, key))
            mmm+=1
        key = int(key) + 1
    if mmm>=num:
        break
    for i in range(2*n+1):#Right
        y+=1
        if r1<=x<=r2 and c1<=y<=c2:
            matrix.append((x,y,key))
            mmm+=1
        key = int(key) + 1
    if mmm>=num:
        break
    n+=1
matrix.sort(reverse=True)
test=list(matrix)
test=sorted(test,key=lambda x :x[2],reverse=True)
first=test[0][2]
while True:
    first=first//10
    cnt+=1
    if first==0:
        break
for i in range(r2-r1+1):
    for j in range(c2-c1+1):
        last=matrix.pop()
        data=last[2]

        data=str(data).rjust(cnt,' ')
        print(data,end=' ')
    print()
```
<h1>느낀점</h1>
너무 빡셌음....
시간이 매우 많이 걸렸고 짜잘짜잘한 오류들이 너무 많이 발생해서 그거 잡는거에 시간이 많이 들어감
오류들을 전부 정리하는것보단 다시한번 더 풀어보는게 좋을것 같아서 오류들은 기입 안할거임
처음에는 matrix 리스트에 전부 담은 다음 출력할때 조건에 맞게 일부분만 출력하려 했지만 메모리초과+시간초과 맞아버림
그래서 matrix에 저장하지 않고 무한반복 돌면서 조건에 맞는 애들만 Matrix.append() 해줬음 무작정 넣어주고 출력할때 정리해서 출력하는 방향으로 짬
