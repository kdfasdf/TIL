https://school.programmers.co.kr/learn/courses/30/lessons/181188

## 풀이
처음에는 폭격 미사일이 겹치는 범위를 배열에 저장하고 요격 미사일의 값의 변화가 있는 곳마다 요격 미사일을 두고 격추했을 때 격추된 미사일의 수가(배열에
저장된 값)의 합이 target의 길이랑 같은경우를 구해보려고 했는데 열린구간 닫힌구간 처리가 까다로워서 포기했다<br>
사실 처음 문제를 읽었을 때 백준 회의실 배정 문제와 비슷하다고 생각해 정렬을 떠올렸었으니 정렬로 접근하였다
- 오른쪽 끝 점을 기준으로 정렬
- 하나씩 탐색하면서 지금 폭격 미사일의 왼쪽 끝점이 앞에서 저장한 오른쪽 끝점보다 오른쪽에 있으면 +1
```
import java.util.*;
class Solution {
    public int solution(int[][] targets) {
    int answer = 0;
    Arrays.sort(targets,(o1,o2)->Integer.compare(o1[1],o2[1]));
        
    int cut = -1;

    for (int i=0; i < targets.length; i++) {
        int left = targets[i][0];
        int right = targets[i][1];
        if (left >= cut) {
            answer++;
            cut = right;
        }
    }
        return answer;
    }
}
```
