```py
n=int(input())
sentence=[]
key=-1
answer=[]
check={}
for i in range(n):
    x=input()
    sentence.append(x)
    check[x]=i
    #print(x,i)
sentence.sort()

for i in range(len(sentence)):
    for j in range(i+1,len(sentence)):
        if sentence[i]==sentence[j]:
            continue
        #print(sentence[i],sentence[j])
        if sentence[i][0]==sentence[j][0]:
            if len(sentence[i])>=len(sentence[j]):
                first=sentence[j]
                end=sentence[i]
            else:
                first=sentence[i]
                end=sentence[j]
            cnt=0
            for k in range(len(first)):
                if first[k]==end[k]:
                    cnt+=1
                else:
                    break #key point

            if key<=cnt:
                key=cnt
                if check[sentence[i]]<check[sentence[j]]:
                    answer.append((key,check[sentence[i]],check[sentence[j]],sentence[i],sentence[j]))
                else:
                    answer.append((key,check[sentence[j]],check[sentence[i]],sentence[i],sentence[j]))
answer.sort(key=lambda x:(-x[0],x[1],x[2]))

a=answer[0][3]
b=answer[0][4]
if check[a]<check[b]:
    print(a)
    print(b)
else:
    print(b)
    print(a)

```
<h1>느낀점</h1>
처음엔 Trie 자료구조로 접근하려 했으나 뭔가 복잡해질거같아서 그냥 비교를 진행하면서 조건문 추가하면서 푸는 방향으로 갔다.
로직은 문자열 정렬을 시켜주고 2중 반복문을 돌려준다. 2중반복문 범위는 첫번째 반복은 전체이고 두번째 반복은 첫번째 인덱스부터 전체이다.
그리고 첫글자가 같은애만 비교를 실행하도록 조건문을 넣어주었다. 정렬된 상태이기 때문에 첫글자가 틀리는 순간 뒤에있는 애들도 전부 첫글자가 다른애들이기 때문에 continue를 넣어줄수 있다.
첫글자가 같은 애들끼리만 비교반복문을 실행해주고 cnt에 같은글자수를 카운팅 해준다 여기서 다른글자가 나오면 break를 해줘야 하는데 이걸 안해줘서 몇시간 반례만 찾고다녔다;.....
cnt 세주고 answer 리스트에 cnt내림차순으로 넣어주고 lambda로 2,3번째 원소에 대한 내림차순을 추가적으로 넣어준뒤 정렬 -> answer[0] 잘 출력해주면 끝
그리고 딕셔너리로 문자에 대한 인덱스를 따로 저장시켜놓고 다른 조건에 사용하였다.
인덱스 순서를 기억해야 문제조건에 맞게 출력할수 있기 때문
