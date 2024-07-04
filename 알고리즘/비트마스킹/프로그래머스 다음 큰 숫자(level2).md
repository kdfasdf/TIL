https://school.programmers.co.kr/learn/courses/30/lessons/12911
## 풀이
bitCount메서드를 알면 쉽게 풀리는 문제
```
class Solution {
    public int solution(int n) {
        int compare=n+1;
        int answer = 0;
        while(Integer.bitCount(compare)!=Integer.bitCount(n))
        {
            compare+=1;
        }
        answer=compare;
        return answer;
    }
}
```
