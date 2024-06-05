https://school.programmers.co.kr/learn/courses/30/lessons/42746
## 풀이
numbers[i]와 numbers[i+1]에 대해서 numbers[i]+numbers[i+1]와 numbers[i+1]+numbers[i]중 첫번째 의 합이 사전순으로 뒤라면 numbers[i]가 앞에 오고 두번째의 합이 사전순으로 뒤라면 number[i+1]이 앞으로 오도록 정렬하면 된다.
정렬 후 이를 이으면 가장 큰 수를 구할 수 있다.
- Java
```
import java.util.Arrays;

public class Solution {
    public String solution(int[] numbers) {
        String answer;
        String[] arr = new String[numbers.length];

        for (int i = 0; i < arr.length; i++) {
            arr[i] = String.valueOf(numbers[i]);
        }
        Arrays.sort(arr, (o1, o2) -> (o2 + o1).compareTo(o1 + o2));
        if (arr[0].equals("0")) {
           return "0";
        }
        StringBuilder temp = new StringBuilder();
        for (int i = 0; i < arr.length; i++) {
            temp.append(arr[i]);
        }

        answer=temp.toString();
        return answer;
    }
}
```
