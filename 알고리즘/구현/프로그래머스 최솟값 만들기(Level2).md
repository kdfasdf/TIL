https://school.programmers.co.kr/learn/courses/30/lessons/12941

## 풀이
자바에서는 내림차순 정렬이 없기 때문에 둘 다 오름차순으로 정렬하고 긴배열은 앞쪽에서 길이가 짧은 배열은 뒷쪽에서 하나씩 골라 곱한 곱하고 이 값을 더한다. 짧은 배열의 길이만큼 진행해주면 되는 문제
- Java
```
import java.util.Arrays;
class Solution {

    public int solution(int [] A , int [] B) {
        int answer=0;
        Arrays.sort(A);
        Arrays.sort(B);
        if(A.length>B.length)
        {
            for(int i=0;i<B.length;i++)
                answer+=A[i]*B[B.length-1-i];
        }
        else{
            for(int i=0;i<A.length;i++)
                answer+=A[A.length-1-i]*B[i];
        }
        return answer;
    }
}
```
