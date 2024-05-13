https://swexpertacademy.com/main/code/problem/problemDetail.do?problemLevel=4&contestProbId=AV15B1cKAKwCFAYD&categoryId=AV15B1cKAKwCFAYD&categoryType=CODE&problemTitle=&orderBy=RECOMMEND_COUNT&selectCodeLang=ALL&select-1=4&pageSize=10&pageIndex=1
## 풀이
bfs를 활용한 문제
가장 먼 거리에 있는 노드 중 가장 값이 큰 노드의 번호를 출력하는 문제<br>
bfs 큐를 돌릴 때 거리변수를 추가로 두어 돌리고 거리배열에 노드들을 추가한다
- python
```
def bfs(start):
    q=[]
    distance=0
    q.append([start,distance])
    visited[start]=1
    result[distance].append(start) 
    while q:
        now,dist =q.pop(0)
        result[dist].append(now) # 그 거리에 해당하는 노드들을 저장
        for i in graph[now]:
            if visited[i]==0:
                visited[i]=1
                q.append([i,dist+1])

for test in range(1,10+1):
    n,m=map(int,input().split())
    data=list(map(int,input().split()))
    graph=[[] for i in range(max(data)+1)]
    visited=[0]*(max(data)+1)
    result=[[] for i in range(101)]  #거리 배열 사람 연결 관계는 100명까지이므로
    for i in range(0,len(data),2):
        graph[data[i]].append(data[i+1])
    bfs(m)
    for i in range(len(result)-1,-1,-1):   # 뒤에서 부터 탐색 
        if len(result[i])!=0:
            print('#{}'.format(test),max(result[i]))
            break
```
