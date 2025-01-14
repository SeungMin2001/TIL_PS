```py
import collections

class Node:      # Node 구조 설정 key,child,length
    def __init__(self, key):
        self.key = key
        self.child = {}
        self.length = []

class Trie:
    def __init__(self):
        self.head = Node(None)

    def insert(self, word):
        curr = self.head
        for w in word:
            if w not in curr.child:
                curr.child[w] = Node(w)
            curr.length.append(len(word))
            curr = curr.child[w]
        curr.length.append(len(word))

    def search(self, query):
        curr = self.head
        for q in query:
            if q == "?":
                return curr.length.count(len(query))
            elif q in curr.child:
                curr = curr.child[q]
            # 매칭 되는 단어가 없을 경우
            else:
                return 0


def solution(words, queries):
    answer = []
    rev_words, count_words = [], collections.defaultdict(int) #collections 포함된 기능= 키값이 없어도 오류 안나도록 해주는것(딕셔너리 초기화)

    for word in words:
        rev_words.append(word[::-1])  # 2번 조건 -> 모든단어 뒤집고 다시 저장
        count_words[len(word)] += 1  # 3번 조건 -> 길이 5인 단어가 3번 들어왔으면 {5:3} 이런식으로 저장됨

    trie = Trie()
    rev_trie = Trie()

    # insert
    for word in words: #정상적인 문자들 저장
        trie.insert(word)
    for word in rev_words: #뒤집은 문자들 저장
        rev_trie.insert(word)

    # 3가지 조건에 맞게 search
    for query in queries:
        # 3번 조건
        if query[0] == "?" and query[-1] == "?": #문자열 전체가 "?" 인 경우
            answer.append(count_words[len(query)])
        # 1번 조건
        elif query[-1] == "?": # "?" 이 마지막에 위치하는 경우
            answer.append(trie.search(query))
        # 2번 조건
        elif query[0] == "?": # "?"이 처음에 위치하는 경우
            answer.append(rev_trie.search(query[::-1]))
    return answer
```
<h1>느낀점</h1>
처음 접했던 자료구조..... 매우 힘들었음
트라이는 트리랑 매우 닮아있는 자료구조인데 문자열에 최적화된 자료구조이다.
파이썬에서는 딕셔너리를 사용해서 구현하는데 CPP애 구조체 사용해서 리스트를 구현했던것과 많이 비슷하다고 느꼇다.
쩃든 아이디어는 문자열을 트리처럼 부모와 자식관계를 딕셔너리의 키 와 데이터 구조로 그대로 가져와서 쭉 연결한다.
그리고 이 문자를 다시 search할때도 root부터 쭉 내려가면서 전부 동일하면 true를 반환하는 이런 구조인데
내가 푼 문제는 문자열 길이를 구하는 문제이므로 길이의 대한 정보를 가진 length 리스트를 Node class에 추가했다.
여기서 insert 할때 그 문자의 길이를 length 에 append를 계속 해준다. 즉 apple이 들어오면 a,p,p,l,e 이 5개의 length 값이 다 5가 들어가는 것이다.
그리고 search할때 "?"가 나왔을때 "?"를 포함한 문자열의 길이와 같은 문자열에 개수를 length.count로 찾아낸다. insert할때 길이를 전부 append 했으므로!!!!
이 부분이 매우 인상이 깊었다. Trie 자료구조는 적응 될때까지 관련 문제들을 반복적으로 풀어야 겠다고 생각이 들었고 이 문제에 코드도 주기적으로 봐야겠다고 생각이 들었다.
