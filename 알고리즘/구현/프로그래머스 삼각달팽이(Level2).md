https://school.programmers.co.kr/learn/courses/30/lessons/68645
## 풀이
프로그래머스 적응용 문제
- Java
```
import java.util.Arrays;
class Solution{
    static int[] dx={1,0,-1};
    static int[] dy= {0,1,-1};
    
    public int[] solution(int n){
        int[][] data= new int[n][n];
        int[][] visited= new int[n][n];
        int move=0;
        int sx=0;
        int sy=0;
        int count=1;
        int index=0;
        int loop=(int)n*(n+1)/2;
        data[sx][sy]=1;
        int[] result = new int[loop];
        visited[sx][sy]=1;
        while(count<loop){
            int nx=sx+dx[move];
            int ny=sy+dy[move];
            if(0<=nx&&nx<n&&0<=ny&&ny<n&&visited[nx][ny]==0)
            {
                count+=1;
                visited[nx][ny]=1;
                data[nx][ny]=count;
                sx=nx;
                sy=ny;
            }   
            else{
                move+=1;
                if(move==3)
                    move=0;
                }
                
            }
      
        for (int i=0;i<n;i++)
          for(int j=0;j<n;j++)
              if (i>=j){
                 result[index]=data[i][j];
                 index+=1;
                        }
        return result;
        }
}

```
