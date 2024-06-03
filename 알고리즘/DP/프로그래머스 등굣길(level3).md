https://school.programmers.co.kr/learn/courses/30/lessons/42898#

## 풀이
처음에 조건을 여러개로 분리해서 틀렸던 문제 좀 더 간소하게 고쳐서 통과했지만 좀 더 연구가 필요하다
- 자료구조
- dp 테이블 : 결과 구해야 하므로 초기에 0으로 초기화 후 1행, 1열 웅덩이가 없는 경우 1로 초기화(웅덩이 만나면 그 이후는 1로 초기화 x)
- visited : dp 테이블과 같은 크기의 배열로 웅덩이를 표시한다

- 알고리즘
- 웅덩이의 위치에 -1 할당(visited[x][y]에 -1 할당(x,y는 웅덩이의 좌표)
- 행 단위로 dp 테이블을 채워나가는데 웅덩이라면 건너뛴다
- 웅덩이가 아니라면 왼쪽과 위쪽 dp 테이블의 값을 더한다

- 틀렸던 부분
```
if(visited[i][j]!=-1&&visited[i-1][j]!=-1&&visited[i][j-1]!=-1)
                {
                    dp[i][j]=(dp[i-1][j]+dp[i][j-1])%1000000007;
                }
                else if (visited[i-1][j]==-1 || visited[i][j-1]==-1){//위 혹은 왼쪽이 웅덩이
                    int temp = visited[i-1][j]==-1? dp[i][j-1] : dp[i-1][j];
                    dp[i][j]=temp;
                }
                else if(visited[i][j]==-1){//현재 위치가 웅덩이
                    continue;
                }
```
가장 위 행부터 채워나가는데 웅덩이가 아닌 경우에 정상적으로 왼쪽과 위쪽의 값을 더해나간다. 
만약 왼쪽과 윗쪽 둘 중 하나라도 웅덩이라면 웅덩이가 아닌쪽의 값을 현재 위치에 할당해준다(둘다 웅덩이인 경우 아무거나 할당해도 상관 없음)
그리고 현재 위치가 웅덩이이면 넘어간다 채점하면 95점 코드인데 틀린 하나의 테스트 케이스가 무엇인지 모르겠다

- 고친 부분
```
                if(visited[i][j]!=-1)
                {
                    dp[i][j]=(dp[i-1][j]+dp[i][j-1])%1000000007;
                }
                else if(visited[i][j]==-1){//현재 위치가 웅덩이
                    continue;
                }
```
웅덩이는 어차피 0으로 초기화 되어 있으므로 왼쪽과 위쪽에 있을 때는 그냥 더해줘도 상관 없다.

- Java(정답 코드)
```
class Solution {
    static int[][] dp;
    static int[][] visited;
    public int solution(int m, int n, int[][] puddles) {
        int answer = 0;
        dp= new int[n][m];
        visited=new int[n][m];
        if (puddles[0].length ==2){
        for(int i=0;i<puddles.length;i++)
        {
            int py= puddles[i][0]-1; // m
            int px = puddles[i][1]-1; //n
            visited[px][py]=-1;
        }}
        for(int i=0;i<n;i++){
            if(visited[i][0]==-1)
                break;
            dp[i][0]=1;
        }
        for(int j=0;j<m;j++)
        {   
            if (visited[0][j]==-1)
                break;
            dp[0][j]=1;
        }
        for(int i=1;i<n;i++)
        {
            for(int j=1;j<m;j++)
            {
                if(visited[i][j]!=-1)
                {
                    dp[i][j]=(dp[i-1][j]+dp[i][j-1])%1000000007;
                }
                else if(visited[i][j]==-1){//현재 위치가 웅덩이
                    continue;
                }
            }
        }
        answer=dp[n-1][m-1]%1000000007;
        return answer;
    }
}
```
