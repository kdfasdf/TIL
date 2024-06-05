https://school.programmers.co.kr/learn/courses/30/lessons/154538

## 풀이 
처음에 dp로 푸는게 나을까 bfs로 푸는게 나을까 고민했다<br>
하지만 10*2+n과 10*n+2의 결과가 다르므로 bfs로 푸는 것이 더 수월하다 생각하여 bfs로 풀었다<br>
탐색의 진행 방향이 모두 크게 증가하는 쪽이라 방문처리를 따로 할 필요가 없다고 생각했었는데 시간초과가 발생하였고
방문 처리를 통해 중복을 줄여서 통과할 수 있었다.
- Java
```
import java.util.*;
class Solution {
    public void bfs(int x,int y,int n)
    {
        Queue<Integer> q = new LinkedList<>();
        q.add(x);
        dp[x]=0;
        while(!q.isEmpty())
        {
            int now = q. poll();
            if(now==y)
                break;
            if(2*now<=y&&visited[2*now]==0)
            {
                visited[2*now]=1;
                dp[2*now]=Math.min(dp[now]+1,dp[2*now]);
                q.add(2*now);
            }
            if(now*3<=y&&visited[3*now]==0)
            {
                visited[3*now]=1;
                dp[3*now]=Math.min(dp[now]+1,dp[3*now]);
                q.add(3*now);
            }
            if(now+n<=y&&visited[now+n]==0)
            {
                visited[now+n]=1;
                dp[now+n]=Math.min(dp[now]+1,dp[now+n]);
                q.add(now+n);
            }
        }
    }
    static int[] dp;
    static int[] visited;
    public int solution(int x, int y, int n) {
        int answer = 0;
        dp=new int[y+1];
        visited=new int[y+1];
        Arrays.fill(dp,(int)1e9);
        bfs(x,y,n);
        answer=dp[y]!=(int)1e9?dp[y]:-1;
        return answer;
    }
}
```
