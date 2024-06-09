https://school.programmers.co.kr/learn/courses/30/lessons/12905

## 풀이 
정사각형의 우측 하단 꼭지점을 기준으로 위와 좌측, 왼쪽 대각선 왼쪽 윗 방향으로 0인지 아닌지 확인한다.
<br>
2x2 기준으로는 1인지 0인지 확인하고 새 블록 중 가장 작은 수+1을 현재 블록에 할당한다(0이 끼어있으면 현재 블록에 1을, 세 블록이 모두 1이면 2를 할당하여 크기를 조정하는 방식)<br>
그렇다면 3x3 기준으로는 위와 왼쪽, 대각선 왼쪽 위 방향이 모두 2이면 현재 블록이 3이 되므로 3x3 블록을 만들 수 있다
- java
```
class Solution
{
    public int solution(int [][]board)
    {
        int answer=0;
        int[][] newBoard = new int[board.length+1][board[0].length+1];//dp용 테이블
        for(int i=0;i<board.length;i++)
            for(int j=0;j<board[i].length;j++)
                newBoard[i+1][j+1]=board[i][j];
        int max=0;
        for(int i=1;i<newBoard.length;i++)
            for(int j=1;j<newBoard[i].length;j++)
            {
                if(newBoard[i][j]==1)
                {
                    int left=newBoard[i-1][j];
                    int up = newBoard[i][j-1];
                    int leftUp=newBoard[i-1][j-1];
                    int min=Math.min(left,Math.min(up,leftUp));
                    newBoard[i][j]=min+1;
                    max=Math.max(max,newBoard[i][j]);
                }
            }
        answer=max*max;
        return answer;
    }
}
```
