https://school.programmers.co.kr/learn/courses/30/lessons/1844?language=java

## 풀이
bfs 기본 문제

- Java
```
import java.util.*;
class Node{
    int x;
    int y;
    Node(int x, int y){
        this.x=x;
        this.y=y;
    }
}

class Solution {
    
    static int[] dx = {-1,1,0,0};
    static int[] dy={0,0,-1,1};
    static int[][] visited;
    public int solution(int[][] maps) {
        int answer = 0;
        int row=maps.length;
        int column=maps[0].length;
        visited=new int[row+1][column+1];
        
        Queue<Node> q = new LinkedList<>();
        q.add(new Node(0,0));
        visited[0][0]=1;
        while(!q.isEmpty())
        {
            Node now = q.poll();
            int x=now.x;
            int y=now.y;
            for(int i=0; i<4;i++)
            {
                int nx=x+dx[i];
                int ny=y+dy[i];
                if(0<=nx&&nx<row &&0<=ny&&ny<column&&visited[nx][ny]==0&&maps[nx][ny]==1){
                    visited[nx][ny]=visited[x][y]+1;
                    q.add(new Node(nx,ny));
                }
            }
        }
        if(visited[row-1][column-1]!=0)
            answer=visited[row-1][column-1];
        else
            answer=-1;
        return answer;
    }
}
```
