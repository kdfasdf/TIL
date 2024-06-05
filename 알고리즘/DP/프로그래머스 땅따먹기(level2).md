https://school.programmers.co.kr/learn/courses/30/lessons/12913
## 풀이
dp 기본 문제 land 테이블과 dp 테이블을 나눈 후 0행을 dp테이블과 land 테이블을 같은 값으로 초기화한다
이후 1행 0열을 기준으로 했을 때 0행 0열을 제외한 0행 1열,2열,3열 중 가장 큰 값을 가지는 값을 더하면서 땅따먹기를 진행한다.
즉 알골리즘으로 정리하면 다음과 같다
1. dp 테이블 land 테이블 초기화 land의 0행의 값을 dp 테이블 0행에 초기화
2. 1행 부터 모든 열에 대해서 바로 윗칸을 제외하고 가장 큰 값을 가지는 값을 더해감 즉 dp[i][j]는 land[i][j]+Max(dp[i-1][])
- Java
```
class Solution {
    int solution(int[][] land) {
        int answer = 0;
        int[][] dp =new int[land.length][4];
        for(int i=0;i<4;i++)
            dp[0][i]=land[0][i];
        for(int i=1;i<land.length;i++)
        {
            for(int j=0;j<4;j++)
            {
                int temp=0;
                for(int k=0;k<4;k++)
                {   
                    if(j==k) continue;
                    temp=Math.max(temp,dp[i-1][k]);
                }
                dp[i][j]=land[i][j]+temp;
            }
        }
        for(int i=0;i<4;i++)
            answer=Math.max(answer,dp[dp.length-1][i]);
        return answer;
    }
}
```
