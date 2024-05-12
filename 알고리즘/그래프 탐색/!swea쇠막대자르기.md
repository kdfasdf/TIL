https://swexpertacademy.com/main/code/problem/problemDetail.do?problemLevel=4&contestProbId=AV5LtJYKDzsDFAXc&categoryId=AV5LtJYKDzsDFAXc&categoryType=CODE&problemTitle=&orderBy=RECOMMEND_COUNT&selectCodeLang=ALL&select-1=4&pageSize=10&pageIndex=1

## 풀이 
문제 조건에 맞는 경로 중 최장 경로와 그 최장경로의 출발점(최장 경롤를 가지는 출발점이 여러 점일 떄는 출발점 번호가 가장 작은 것)을 구하는 문제
처음에 BFS로 풀었을 때는 모든 점에대해서 bfs를 수행하여 시간초과가 발생했다. 다른 출발점에서 시작하는 경로를 통해 이미 방문 처리가 된 점에서는 bfs를 수행할 필요가 없었고 해당 조건을 넣어주니 통과
(1 -> 2 -> 3) bfs를 수행했으면 2를 출발점으로 하는 bfs는 수행할 필요가 없다는 이야기

- python
```
def bfs(x,y):
    q=[]
    q.append([x,y])
    visited[x][y]=1
    tx=0
    ty=0
    while q:
        tx,ty=q.pop(0)
        for i in range(4):
            nx=tx+dx[i]
            ny=ty+dy[i]
            if 0<=nx<n and 0<=ny<n and data[tx][ty]+1==data[nx][ny] : #vistied[nx][ny]==0 을 쓰면 안되는데 지금 bfs의 출발점이  다른 점에서 출발한 bfs의 중간 경로일 수 있기 떄문
                visited[nx][ny]=visited[tx][ty]+1
                q.append([nx,ny])
    return visited[tx][ty]

dx=[-1,1,0,0]
dy=[0,0,-1,1]
t=int(input())
for test in range(1,t+1):
    data=[]
    n=int(input())
    maxDis=-1e9
    minRoom=1e9
    visited=[[0]*n for i in range(n)]
    distance=[[0]*n for i in range(n)]
    for i in range(n):
        data.append(list(map(int,input().split())))
    for i in range(n):
        for j in range(n):
            if visited[i][j]==0:
            	distance[i][j]=bfs(i,j)
            if maxDis<distance[i][j]:
                maxDis=distance[i][j]
                minRoom=data[i][j]
            if maxDis == distance[i][j] and  minRoom>data[i][j]:
                minRoom=data[i][j]
    print('#{}'.format(test),minRoom,maxDis)
```
