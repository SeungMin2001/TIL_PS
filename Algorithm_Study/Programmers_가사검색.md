```py
def count_leaf(tmp_trie, depth):
    space = [(tmp_trie, k, depth) for k in tmp_trie.keys()]

    cnt = 0
    while len(space) > 0:
        tmp_trie, k, depth = space[0]
        space = space[1:]

        if depth == 0 and k == '@@@':
            cnt += 1
            #print(tmp_trie)
            continue

        if depth > 0 and k != '@@@':
            space.extend([(tmp_trie[k], new_k, depth-1) for new_k in tmp_trie[k].keys() if type(tmp_trie)])

    return cnt

def solution(words, queries):
    answer = []

    fow_trie = {}

    for word in words:
        tmp_trie = fow_trie

        if 'count' not in tmp_trie:
            tmp_trie['count'] = {}

        if len(word) not in tmp_trie['count']:
            tmp_trie['count'][len(word)] = 1
        else:
            tmp_trie['count'][len(word)] += 1

        for i, c in enumerate(word, 1):
            if c not in tmp_trie:
                tmp_trie[c] = {}
            tmp_trie = tmp_trie[c]

            if 'count' not in tmp_trie:
                tmp_trie['count'] = {}

            if (len(word) - i) not in tmp_trie['count']:
                tmp_trie['count'][len(word) - i] = 1
            else:
                tmp_trie['count'][len(word) - i] += 1

            if i == len(word):
                tmp_trie['@@@'] = word

    rev_trie = {}

    for word in words:
        tmp_trie = rev_trie
        word = word[::-1]

        if 'count' not in tmp_trie:
            tmp_trie['count'] = {}

        if len(word) not in tmp_trie['count']:
            tmp_trie['count'][len(word)] = 1
        else:
            tmp_trie['count'][len(word)] += 1

        for i, c in enumerate(word, 1):
            if c not in tmp_trie:
                tmp_trie[c] = {}
            tmp_trie = tmp_trie[c]

            if 'count' not in tmp_trie:
                tmp_trie['count'] = {}

            if (len(word) - i) not in tmp_trie['count']:
                tmp_trie['count'][len(word) - i] = 1
            else:
                tmp_trie['count'][len(word) - i] += 1

            if i == len(word):
                tmp_trie['@@@'] = word

    for query in queries:

        if query[0] == '?':
            query = query[::-1]
            tmp_trie = rev_trie
        else:
            tmp_trie = fow_trie

        cnt = 0
        for i, c in enumerate(query):
            if c == '?':
                if 'count' in tmp_trie:
                    cnt = tmp_trie['count'].get(len(query) - i, 0)
                break

            if c not in tmp_trie:
                break
            tmp_trie = tmp_trie[c]

        answer.append(cnt)

    return answer
```
<h1>느낀점</h1>
매우 어려웠던 문제
트라이 자료구조를 사용해서 푸는 문제였는데 트라이 자료구조를 몰랐던 상태여서 공부를 병행하면서 풀었던 문제
트라이에 대해 추가적인 공부 필요하다고 느낌
이 문제는 주가적으로 풀어봐야함 + 트라이 개념공부
