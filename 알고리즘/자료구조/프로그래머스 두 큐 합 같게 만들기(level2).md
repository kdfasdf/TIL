https://school.programmers.co.kr/learn/courses/30/lessons/118667
## 풀이
각 배열에 대한 큐를 선언하고 각 배열의 원소를 각각의 큐에 저장한<br>
두 큐의 합을 비교하여 더 큰쪽의 원소를 하나 빼서 반대쪽에 삽입하는 과정을 반복해서 두 큐의 합이 같아질 때를 찾는다
처음에 while문 조건 안을 (sum1!=sum2)를 넣어서 틀렸던 문제(처음에 주어진 두 배열의 합이 같은 경우를 생각을 안했다)
- Java
```
import java.util.*;
class Solution {
    public long solution(int[] queue1, int[] queue2) {
        long answer=-1;
        Queue<Integer> q1 =new LinkedList<>();
        Queue<Integer> q2 = new LinkedList<>();
        long sum1=0;
        long sum2=0;
        for(int i=0;i<queue1.length;i++)
        {
            q1.add(queue1[i]);
            sum1+=queue1[i];
            q2.add(queue2[i]);
            sum2+=queue2[i];
        }
        long count=0;
        while(count<queue1.length*4){    
            if(sum1>sum2)
            {
                int temp=q1.poll();
                sum1-=temp;
                sum2+=temp;
                q2.add(temp);
                count+=1;
            }
            else if(sum1<sum2)
            {
                int temp=q2.poll();
                sum1+=temp;
                sum2-=temp;
                q1.add(temp);
                count+=1;
            }
            if(sum1==sum2)
            {
                answer=count;
                break;
            }  
        }
        return answer;
    }
}
```
