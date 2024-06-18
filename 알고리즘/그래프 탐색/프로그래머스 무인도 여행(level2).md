https://school.programmers.co.kr/learn/courses/30/lessons/154540

## 풀이 
bfs 기본 문제
- Java
```
import java.util.*;
class Node{
    int row;
    int column;
    Node(int row, int column)
    {
        this.row=row;
        this.column=column;
    }
}

class Solution {
    static int[][] visited;
    static int[][] graph;
    static PriorityQueue<Integer> temp = new PriorityQueue<>();
    static int[] dx={-1,1,0,0};
    static int[] dy={0,0,-1,1};
    static int row;
    static int column;
    static int bfs(int startx,int starty)
    {
        int connect=0;
        Queue<Node> q = new LinkedList<>();
        q.add(new Node(startx,starty));
        visited[startx][starty]=1;
        connect=graph[startx][starty];
        while(!q.isEmpty()){
            Node temp = q.poll();
            int x= temp.row;
            int y = temp.column;
            for(int i=0;i<4;i++)
            {
                int nx=x+dx[i];
                int ny=y+dy[i];
                if(0<=nx&&nx<row&&0<=ny&&ny<column&&visited[nx][ny]==0&&graph[nx][ny]!=0)
                {   
                    visited[nx][ny]=1;
                    connect+=graph[nx][ny];
                    q.add(new Node(nx,ny));
                }   
            }
        }
        return connect;
    }
    public int[] solution(String[] maps) {
        row = maps.length;
        column=maps[0].length();
        visited=new int[row][column];
        graph = new int[row][column];
        for(int i=0; i<row;i++){
            for(int j=0;j<column;j++)
            {
                if(maps[i].charAt(j)!='X')
                    graph[i][j]=maps[i].charAt(j)-'0';
                else
                    graph[i][j]=0;
            }
        }
        for(int i=0; i<row;i++){
            for(int j=0;j<column;j++)
            {
                if(graph[i][j]!=0&&visited[i][j]==0)
                    temp.add(bfs(i,j));
            }
        }
        if (temp.size()==0)
        {
            int[] answer = {-1};
            return answer;
        }            
        else{
        int answer[] = new int[temp.size()];
            int index=0;
        while(!temp.isEmpty())
        {answer[index]=temp.poll();
        index++;
        }
         return answer;
        }
    }
}
```
