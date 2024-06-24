https://school.programmers.co.kr/learn/courses/30/lessons/64061

## 풀이
문제 그대로 구현하면 되는 문제<br>
바구니는 컬렉션 프레임워크를 사용하지않고 배열로 구현해보았다
- Java
```
import java.util.*;
class Solution {

    static int answer=0;
    public int solution(int[][] board, int[] moves) {
        int bsize=board.length;
        int[] bucket = new int[900];
        for(int i=0;i<moves.length;i++)
        {
            int column=moves[i]-1;
            for(int j=0;j<bsize;j++)
            {
                if(board[j][column]!=0)
                {
                    System.out.println(board[j][column]);
                    for(int k=0;k<bucket.length;k++)
                    {
                        if(bucket[k]==0)
                        {    
                            bucket[k]=board[j][column];
                            board[j][column]=0;
                            if(k>=1&&bucket[k]==bucket[k-1])
                            {
                                bucket[k]=0;
                                bucket[k-1]=0;
                                answer+=2;
                            }
                            break;
                        }
                    }
                    break;
                }
            }
        }
        return answer;
    }
}
```
