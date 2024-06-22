https://school.programmers.co.kr/learn/courses/30/lessons/135807

## 풀이
한 배열에 대해 그 배열 요소들의 gcd(원소가 n개가 있으면 n개의 수에 대한 GCD)를 구하고 나머지 배열의 원소들에 나누어 떨어지지 않는지 확인하는 문제
- Java
```
class Solution {
    static int compare;
    static int gcds(int[] data)
    {
        compare=data[0];
        for(int i=1;i<data.length;i++)
        {
            compare=gcd(compare,data[i]);
        }
        return compare;
    }
    static int gcd(int a,int b)
    {
        int tempa=a;
        int tempb=b;
        int num=2;
        int result=1;
        while(num<=tempa&&num<=tempb)
        {
            if(tempa%num==0&&tempb%num==0)
            {
                tempa/=num;
                tempb/=num;
                result*=num;
                num=2;
            }
            else{num+=1;}
        }
        return result;
    }
    static int div(int[] datab,int gcda)
    {
        for(int value: datab)
        {
            if(value%gcda==0)
                return 0;
        }
        return gcda;
    }
    public int solution(int[] arrayA, int[] arrayB) {
        int resultA=gcds(arrayA);
        int result1=div(arrayB,resultA);
        int resultB=gcds(arrayB);
        int result2=div(arrayA,resultB);
        int answer = result1==0&&result2==0?0:Math.max(result1,result2);
        return answer;
    }
}
```
