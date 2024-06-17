https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWqU0zh6rssDFARG

## 풀이
해시셋에 넣어주어 중복을 없애고
우선순위큐에 먼저 길이 오름차순, 길이가 같으면 사전순으로 오름차순이 되도록 담아주면 되는 문제

- Java
```
import java.util.Scanner;
import java.io.FileInputStream;
import java.util.*;
import java.io.*;

class Solution
{
    public static void main(String args[]) throws Exception
    {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        int test=Integer.parseInt(br.readLine());
        for(int a=1;a<=test;a++){
            System.out.println("#"+a);
            int loop=Integer.parseInt(br.readLine());
            HashSet<String> set = new HashSet<>();
            PriorityQueue<String> pq = new PriorityQueue<>(
                    new Comparator<String>() {
                        @Override
                        public int compare(String t, String other){
                            if (t.length()>other.length())
                                return 1;
                            else if(t.length()<other.length())
                                return -1;
                            else
                                return t.compareTo(other);

                        }
                    }
                    );
            for(int i=0;i<loop;i++)
            {
                set.add(br.readLine());
            }
            Iterator<String> it = set.iterator();
            while(it.hasNext())
                pq.add(it.next());
            while(!pq.isEmpty())
                System.out.println(pq.poll());
        }
    }
}
```
