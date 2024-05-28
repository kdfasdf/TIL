https://school.programmers.co.kr/learn/courses/30/lessons/131701

## 풀이
시작점을 기준으로 하여 옆칸, 옆옆칸....의 누적합을 set에 저장한다<br>
그러면 그 시작점으로부터의 연속 부분 수열들을 구할 수 있고 set에 저장하는 것이므로  중복을 제거해줄 수 있다.
- Java
```
import java.util.*;
class Solution{
    public int solution(int[] elements){
        int answer=0;
        HashSet set = new HashSet();
        int loop=elements.length;
        for(int i=0;i<loop;i++)
        {
            int temp=0;
            int j=0;
            while(j<loop){
                int index=i+j;
                temp+=elements[index%=elements.length];
                set.add(temp);
                j++;
            }
        }
        answer=set.size();
        return answer;
    }
}
```

