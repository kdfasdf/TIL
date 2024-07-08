https://school.programmers.co.kr/learn/courses/30/lessons/142085
## 풀이
이 문제에서 고려할 점은 다음과 같다
- 적의 수가 가장 많을 때 무적권? ->x
- n이 enemy[i]보다 작다면 그냥 써야함
우선순위 큐를 적절히 사용하면 위 두가지 경우를 간단하게 해결할 수 있는데 enemy[i]를 하나씩 우선순위 큐에 담으면서 우선순위 큐의 크기가 k보다 커지면 n에 대한 뺄셈 연산을 시작한다 결과적으로는 정답 구간에서 가장 큰 enemy[i] 때 무적권을 사용하는 상황이 된다
```
import java.util.*;

class Solution {
    public int solution(int n, int k, int[] enemy) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        int sum = 0;
        int count=0;
        for (int i = 0; i < enemy.length; i++) {
            pq.add(enemy[i]);
            if(pq.size()>k)
            {
                n-=pq.poll();   
            }
            if (n<0) {
                return i;
            }
        }
        return enemy.length;
    }
}
```
