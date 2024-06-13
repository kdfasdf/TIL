https://school.programmers.co.kr/learn/courses/30/lessons/169199

## 풀이
bfs로풀이 한 방향으로 가면 그 방향으로 장애물 까지 쭉 가다가 장애물을 만나면 만나기 전 좌표를 표시해가면서 G를 찾는 문제
- Java
```
import java.util.*;
class Node{
    int x;
    int y;
    public Node (int x, int y)
    {
        this.x=x;
        this.y=y;
    }
}
class Solution {
    static void bfs(int startx, int starty)
    {
        Queue<Node> q = new LinkedList<>();
        q.add(new Node(startx,starty));
        visited[startx][starty]=1;
        while(!q.isEmpty())
        {
            Node now = q.poll();
            int x=now.x;
            int y =now.y;
            
            System.out.println(x+" "+y+" "+visited[x][y]);
            if(board1[x][y]=='G'){
                answer=visited[x][y];
                System.out.println(x+" "+y+" "+visited[x][y]);
                break;
            }
            for(int i = 0;i<4;i++)
            {
                int tx=x+dx[i];
                int ty = y+dy[i];
                while(true)
                {
                    if(0<=tx&&tx<row&&0<=ty&&ty<column&&board1[tx][ty]!='D')
                    {
                        tx+=dx[i];
                        ty+=dy[i];
                    }else{
                        tx-=dx[i];
                        ty-=dy[i];
                        break;
                    }
                }
                if(visited[tx][ty]==0)
                {
                    q.add(new Node(tx,ty));
                    visited[tx][ty]=visited[x][y]+1;
                }
            }
        }
    answer-=1;
    }
    static int[] dx = {-1,1,0,0};
    static int[] dy ={0,0,-1,1};
    static int[][] visited;
    static char[][] board1;
    static int row;
    static int column;
    static int answer;
    
    public int solution(String[] board) {
        row = board.length;
        column=board[0].length();
        board1 = new char[row][column];
        visited = new int[row][column];
        int i=0;
        int j=0;
        int startx=0;
        int starty=0;
        for(String s : board)
        {
            for(char a : s.toCharArray()){
                board1[i][j]=a;
                if(a=='R')
                {
                    startx=i;
                    starty=j;
                }
                j++;
            }
            j=0;
            i+=1;
        }
        bfs(startx,starty);
        return answer;
    }
}
```
