https://school.programmers.co.kr/learn/courses/30/lessons/12953

## 풀이
입력값 범위가 크지 않기 때문에 아래와 같이 최소공배수를 구했다(말로 풀어 설명하기 어렵다)
보편적인 풀이는 유클리드 호제법을 사용하는데 문제 풀 때 유클리드 호제법이 기억이 안났다.(호제법 풀이 첨부)
n개의 최소공배수를 구할 때 차례대로 2개씩 a*b=G*L을 해나가주면 된다

- 2
|2|6|8|14|
|--|--|--|--|
|2|2|2^3|2| 

->2^3 선택

- 3
|2|6|8|14|
|--|--|--|--|
|1|3|1|1| 

-> 3 선택

- 7
|2|6|8|14|
|--|--|--|--|
|1|1|1|7|

->7 선택

결과: 8*3*7=168

- java
```
import java.util.*;
class Solution {
    public int solution(int[] arr) {
        int answer=1;
        int loop=Arrays.stream(arr).max().getAsInt();
        for(int i=2; i<=loop;i++){
            int num=0;
            int temp=0;
            for(int j=0;j<arr.length;j++)
            {   
                temp=0;
                while(true) {
                    if (arr[j] % i == 0) {
                        arr[j] /= i;
                        temp += 1;
                    } else {
                        break;
                    }
                }
                num=Math.max(num,temp);
            }
            if (num!=0){
                answer*=Math.pow(i,num);}
        }
        return answer;
    }
}
```

- 유클리드 호제법
```
import java.util.*;
class Solution {
     public int gcd(int a, int b) {
        if (a > b)
            return (a % b == 0) ? b : gcd(b, a % b);
        else
            return (b % a == 0) ? a : gcd(a, b % a);
    }

    public int solution(int[] arr) {
        int answer = arr[0];
        int g=1;
        for (int i = 1; i < arr.length; i++) {
            g = gcd(answer, arr[i]);
            answer = answer*arr[i]/g;
        }
        return answer;
    }
}
```

