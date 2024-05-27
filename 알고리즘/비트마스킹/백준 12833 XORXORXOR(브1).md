![image](https://github.com/kdfasdf/TIL/assets/96770726/f1ef3f3c-76ac-4873-8dbb-5ca152858cce)
- 예제 입력 1
```
13 3 1
```
- 예제 출력 1
```
14
```

## 풀이
xor의 성질을 이용한 문제 c가 짝수이면 a를 출력하고 홀수라면 a xor b를 출력하는 문제
- Java
```
import java.io.*;
import java.util.*;


public class Main{
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] data=br.readLine().split(" ");
        if (Integer.parseInt(data[2])%2==0)
            System.out.println(data[0]);
        else
            System.out.println(Integer.parseInt(data[0])^Integer.parseInt(data[1]));
    }
}
```
