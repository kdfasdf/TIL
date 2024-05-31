https://school.programmers.co.kr/learn/courses/30/lessons/87946

## 풀이
메서드 이름은 백트래킹으로 썼지만 dfs이다.<br>
이 문제에서는 초기 현재 피로도가 주어지고 최소 피로도와 소모 피로도가 주어진다<br>
각 던전의 최소 필요도와 소모 피로도가 다르므로 어느 던전부터 탐색하느냐에 따라 탐색할 수 있는 던전의 수가 다르다
따라서 dfs로 탐색할 때 탐색 범위를 던전 배열 전체를 탐색해주고 현재 피로도와 방문처리를 비교하여 모든 경우를 탐색한다
- Java
```
import java.util.*;
class Solution {
    static int[] visited;
    static int gk;
    static int answer;
    public static void backtracking(int depth,int[][]dungeons)
    {
        answer=Math.max(answer,depth);
        if(depth==dungeons.length){
            return;
        }
        for(int i=0;i<dungeons.length;i++)
        {
            if(gk>=dungeons[i][0]&&visited[i]==0){
            visited[i]=1;
            gk-=dungeons[i][1];
            backtracking(depth+1,dungeons);
            gk+=dungeons[i][1];
            visited[i]=0;
            }
            else{
                continue;
            }
        }
    }
    public int solution(int k, int[][] dungeons) {
        gk=k;
        visited=new int[dungeons.length+1];
        backtracking(0,dungeons);
        return answer;
    }
}
```
