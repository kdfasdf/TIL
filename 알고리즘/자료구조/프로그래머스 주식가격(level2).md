https://school.programmers.co.kr/learn/courses/30/lessons/42584#

## 풀이 
swea에서 백만 장자 프로젝트를 dp 로 풀었는데 문제가 비슷하다고 생각해서 dp로 접근했으나 오랜 고민 끝에 dp로 푸는 것이 불가능 하다고 결론내렸다. 이유는 아래와 같은 케이스 떄문이다
[3,5,3,2,0]<br>
매우 힘드니 틀린 코드에 대한 설명은 나중에 추가 <br>
시간복잡도 문제 때문에 2중 for문으로 풀지 않으려 했으나 1초뒤 가격이 떨어지는 상황에 반복문을 break 해주면 O(nlogn)이므로 통과되었다

- Java(dp 시도 코드)
```
class Solution {
    public int[] solution(int[] prices) {
        int[] answer = new int[prices.length];
        int compare=(int)1e9;
        int cindex=0;
        for(int i=prices.length-1;i>=0;i--)
        {
            if(i==prices.length-1)
            {
                answer[i]=0;
                compare=prices[i];
                cindex=i;
            }
            else{
                answer[i]=prices[i]<=compare?answer[cindex]+cindex-i:price[i]>price[i+1]?1:cindex-i;
                compare=prices[i]<=compare?prices[i]:price[i]>price[i+1]?price[i+1]:compare;
                cindex=prices[i]<=compare?i:price[i]>price[i+1]?i+1:cindex;
            }
        }
        return answer;
    }
}
```
- Java
```
import java.util.*;
class Solution {
    public int[] solution(int[] prices) {
        int[] answer = new int[prices.length];
    
        for(int i=0;i<prices.length;i++){
            for(int j=i+1;j<prices.length;j++){
                answer[i]++;
                if (prices[i] > prices[j]) break;
            }
        }
        return answer;
    }
}
```
