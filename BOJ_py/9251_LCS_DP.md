```py
a=list(input())
b=list(input())
dp=[[0]*(len(b)+1) for _ in range(len(a)+1)] #key a와b의 순서 중요 for문과 행열이 서로 바껴서 오류

for i in range(1,len(a)+1):
    for j in range(1,len(b)+1):
        if a[i-1]==b[j-1]:
            dp[i][j]=dp[i-1][j-1]+1
        else:
            dp[i][j]=max((dp[i-1][j],dp[i][j-1]))


print(dp[len(a)][len(b)])
```
<h1>느낀점</h1>
DP배열 사용해서 푸는 문제. LCS문제의 점화식을 따로 알고있으면 좋을듯 하다
점화식은 두 문자열을 비교하면서 문지가 다른경우: dp[i][j]=max(dp[i-1][j],dp[i][j-1])
같은경우: Dp[i][j]=dp[i-1][j-1]+1
이 점화식을 가지고 dp배열을 채워나가면 된다.
최장공통집합의 길이는 dp배열중 가장 끝부분에 위치하게 된다 
