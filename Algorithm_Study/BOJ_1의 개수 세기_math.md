```py
dp=[0]*129 #64까지의 dp테이블
dp[1]=1
for i in range(2,129):
    dp[i]=bin(i).count('1')+dp[i-1]
a,b=map(int,input().split())

def test(n):
    cnt=0
    while n!=0:
        n=n//2
        cnt+=1
    return cnt

def run(k): #2^(cnt-1)-1 에서 k까지 1의개수 더한 값
    answer=0
    new=k
    key=test(k)

    if new>64:
        while new>64:
            answer+=(new-2**(key-1))+((key-1)*2**(key-2)+1)
            gap = (2**key)-1-new   #3
            new = (2 ** (key - 1) - 1) - gap #문제점 발견. 반환값이 64가 넘어감

            key=test(new)
        return new,answer
    else:
        return new,answer

#new 가 64범위 안에 들어왔을때 dp테이블 활용

x1,x2=run(b)
y1,y2=run(a-1)

print(dp[x1]+x2-(dp[y1]+y2))
```
<img src='https://github.com/SeungMin2001/TIL_PS/blob/main/Algorithm_Study/IMG_0092.jpeg' width="400" height="500">


<h1>느낀점</h1>
매우 수학적인 문제였다. 오랜만에 수학문제 푸는 느낌이 났던 문제
시간도 많이 씀... while 마지막에 key초기화 방식을 못잡아서 이거 하나때메 쌩쇼 다함
내가 풀었던 노트사진을 기록하고 다시 풀때마다 참고 바람
