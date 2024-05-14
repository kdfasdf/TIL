https://swexpertacademy.com/main/code/problem/problemDetail.do

## 풀이
BFS로 풀이 사다리 게임 규칙을 구현하기 위해 방문처리와 이동할 노드의 족선을 어떻게 해야할지 생각해봐야하는 문제

- python
```
def bfs(i,start):
    q=[]
    q.append([0,i,start])
    distance[0][i]=0
    while q:
        tx,ty,nstart=q.pop(0)
        if tx==99:
            result.append([distance[tx][ty],nstart])
        for i in range(3):
            nx=tx+dx[i]
            ny=ty+dy[i]
            if 0<=nx<100 and 0<=ny<100 and data[nx][ny]!=0 and visited[tx][ty]==0 and visited[nx][ny]==0:
                visited[tx][ty]=1
                distance[nx][ny]=distance[tx][ty]+1
                q.append([nx,ny,nstart])
dx=[0,0,1]
dy=[-1,1,0]
for test in range(1,10+1):
    n=int(input())
    data=[]
    result=[]
    for i in range(100):
        data.append(list(map(int,input().split())))
    for i in range(100):
        if data[0][i]==1:
            visited = [[0] * 100 for i in range(100)]
            distance=[[0] * 100 for i in range(100)]
            bfs(i,i)
    result.sort(key=lambda x: (x[0],-x[1]))
    print('#{}'.format(test),result[0][1])
```
