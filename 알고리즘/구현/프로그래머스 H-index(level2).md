https://school.programmers.co.kr/learn/courses/30/lessons/42747

## 풀이
문제를 제대로 이해하지 못해서 틀렸던 문제<br>정렬 후
h값은 0~n이고 citations.length에서 0방향으로 조사한다(왜냐하면 h-index의 최대값을 구하는 문제이므로)
citations.length-i 즉 h의 값이 citations[i]의 값보다 작거나 같을 때 정답이다

- 예시

0 3 8 9<br>

i가 0일 때: citations.length-i=4,citations[0]=0 : 4 이상 인용된 논문의 수가 2개(만약 citations[0]>=4였다면 그 뒤에 원소들은 무조건 크므로 h-index였을 것이다)<br>
i가 1일 때: citations.length-i=3,ciations[1]=3 : 3이상 인용된 논문의 수가 3개 (citations[1]>=citations.length-i)


- Java
```
import java.util.*;
class Solution {
    public int solution(int[] citations) {
        int answer = 0;
        //정렬
        //정렬 후 각 요소마다 판별
        //
        Arrays.sort(citations);
        for(int i=0;i<citations.length;i++){
            int compare=citations.length-i;
            if(compare<=citations[i]){
                answer=compare;
                break;
            }
        }
        return answer;
    }
}
```
