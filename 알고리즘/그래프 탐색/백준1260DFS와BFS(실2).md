![image](https://github.com/kdfasdf/TIL/assets/96770726/cd5675a1-fd52-4999-869e-26233df79cfa)

- 예제 입력1
```
4 5 1
1 2
1 3
1 4
2 4
3 4
```
- 예제 출력1
```
1 2 4 3
1 2 3 4
```

- 예제 입력2
```
5 5 3
5 4
5 2
1 2
3 4
3 1
```
- 예제 출력2
```
3 1 2 5 4
3 1 4 2 5
```

- 예제 입력3
```
1000 1 1000
999 1000
```

- 예제 출력3
```
1000 999
1000 999
```

## 풀이 
dfs,bfs 기본 연습 문제

- python
```
from collections import deque

def dfs(start):
    visited[start]=True
    result.append(start)
    for i in data[start]:
        if visited[i]==False:
            dfs(i)
    return

def bfs(start):
    q=deque()
    q.append(start)
    visited[start]=True
    result.append(start)
    while q:
        now =q.popleft()
        for i in data[now]:
            if visited[i]==False:
                visited[i]=True
                q.append(i)
                result.append(i)



a,b,c=map(int,input().split())
data=[[] for _ in range(a+1)]
result=[]
visited=[False]*(a+1)
for i in range(b):
    n,m=map(int,input().split())
    data[n].append(m)
    data[m].append(n)
for i in range(a+1):
    data[i].sort()
dfs(c)
print(*result)
result=[]
visited=[False]*(a+1)
bfs(c)
print(*result)
```

- Java
```
import java.io.*;
import java.util.*;

public class Main{
   static ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
   static ArrayList<Integer> result = new ArrayList<>();
   static boolean[] visited;
   static int n;
   static int m;
   static int x;
   static void dfs(int start){
       visited[start]=true;
       result.add(start);
       for (int i=0;i<graph.get(start).size();i++){
            if (visited[graph.get(start).get(i)]==false){
                visited[graph.get(start).get(i)]=true;
                dfs(graph.get(start).get(i));
            }
       }
       return ;
   }
   static void bfs(int start){
       Queue<Integer> q = new LinkedList<>();
       q.add(start);
       visited[start]=true;
       result.add(start);
       while(!q.isEmpty()){
           int now = q.poll();
           for(int i=0;i<graph.get(now).size();i++) {
               if (!visited[graph.get(now).get(i)]) {
                   visited[graph.get(now).get(i)] = true;
                   q.add(graph.get(now).get(i));
                    result.add(graph.get(now).get(i));
               }
           }
       }
       return ;
   }
   public static void main(String[] args) throws IOException {
       BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
       BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
       String[] input = br.readLine().split(" ");
       n=Integer.parseInt(input[0]);
       m = Integer.parseInt(input[1]);
       x = Integer.parseInt(input[2]);
       visited=new boolean[n+1];
       for (int i=0; i<n+1;i++)
       {
           graph.add(new ArrayList<>());
       }
       Arrays.fill(visited,false);

       for(int i=0; i<m;i++)
       {
           input=br.readLine().split(" ");
           int a=Integer.parseInt(input[0]);
           int b=Integer.parseInt(input[1]);
           graph.get(a).add(b);
           graph.get(b).add(a);
       }
       for(int i=0;i<graph.size();i++){
           Collections.sort(graph.get(i));
       }

       dfs(x);
       for(int i=0;i<result.size();i++)
           bw.write(result.get(i)+" ");
       bw.write("\n");
       Arrays.fill(visited,false);
       result.clear();
       bfs(x);
       for(int i=0;i<result.size();i++)
           bw.write(result.get(i)+" ");
       bw.write("\n");
       bw.flush();
       bw.close();

   }
}
```
