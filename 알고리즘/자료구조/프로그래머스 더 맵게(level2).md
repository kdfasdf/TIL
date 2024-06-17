https://school.programmers.co.kr/learn/courses/30/lessons/42626
## 풀이
문제 그대로 구현하는데 우선순위큐 사용법만 알면 쉽게 풀리는 문제<br>
밑에 다른 사람 풀이에 훨씬 깔끔한 코드가 있어 가져왔다
- Java
```
import java.util.*;
class Solution {
    public int solution(int[] scoville, int K) {
        int answer = 0;
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for(int a:scoville)
        {
            pq.add(a);
        }
        while(!pq.isEmpty())
        {
            int temp = pq.poll();
            if(temp>=K)
                break;
            if(pq.isEmpty())
            {
                answer=-1;
                break;
            }
            int temp2=pq.poll();
            int nfood=temp+2*temp2;
            pq.add(nfood);
            answer+=1;
        }
        return answer;
    }
}
```
- Java(다른 사람 풀이)
```
import java.util.PriorityQueue;

class Solution {
    public int solution(int[] scoville, int K) {
         PriorityQueue<Integer> pqScov = new PriorityQueue<>();
         for (int s: scoville) {
             pqScov.add(s);
         }

         int cnt = 0;
         while (pqScov.size() > 1 && pqScov.peek() < K) {
             pqScov.add(pqScov.remove() + pqScov.remove() * 2);
             cnt++;
         }

         return pqScov.peek() >= K ? cnt : -1;
    }
}
```
