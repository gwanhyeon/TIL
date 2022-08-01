# 그래프 인접행렬 및 인접리스트(DFS,BFS)

## 1. 그래프
그래프의 정의를 살펴보면 G=(V,E)가 성립하게 됩니다. G: 그래프, V: 정점, E: 간선을 의미합니다.

## 2. 경로
만약 A->C, A->B, C->B, E->B, C->E, C->D, D->E의 정점과 간선으로 연결된 그래프가 있다고 생각하겠습니다. 이때 정점 A->B로 가는 경로는 몇가지 일까요?
총 4가지 입니다.

```markdown
A->B
A->C->E->B
A->C->D->E->B
A->C->B
```

의 경로가 나오게 됩니다.

## 3. 방향이 있는 그래프
A->C 로 가는 같은 간선에 방향이 있을경우 이것을 방향이 있는 그래프라고 합니다.

## 4. 방향이 없는 그래프
A-C 로 가는 간선에 방향이 없는 경우를 방향이 없는 그래프 라고 합니다.

## 5. 두 정점 사이에 그래프
두 정점 사이에 그래프는 간선이 여러개 존재할 수도 있습니다.

## 6. 순환 루프
자기자신으로 하는 순환하는 간선이 존재할 수도 있습니다.

## 7. 단순 경로와 단순 사이클
경로/사이클에서 같은 정점을 두번 이상 방문하지 않는 경로/사이클을 뜻합니다. 특별한 말이 없다면 일반적으로 사용할 경로와 사이클을 단순 경로/사이클이라고 합니다.

## 8. 차수(Degree)
하나의 정점에 연결되어 있는 간선의 개수를 뜻합니다.
예를 들면 1-5, 2-5, 4,5 정점간의 간선으로 이루어진 그래프가 있다고 생각하겠습니다.
지금 현재 5번 정점과 연결되어 있는 간선의 개수는 3개가 됩니다. 즉, Degree차수의 값이 3개라고 생각하시면 됩니다.

## 9. 가중치
그래프는 가중치의 값을 갖습니다. 정점과 정점사이의 간선에 가중치가 부여될 수도 있는데요. 만약 아무런 표시가 없다면 1이라는 값으로 주어진다고 생각하시면 됩니다.

## 10. 그래프의 표현(인접행렬, 인접 리스트)
그래프의 표현의 종류는 인접행렬과 인접리스트로 나누어지게 됩니다. 해당 설명에서는 i->j 로 연결된 정점과 간선이 있다고 생각하겠습니다. 이것은 A[i] = j 와 연결된 정점을 행렬이나 링크드 리스트로 나타냅니다.

인접행렬은 말 그대로 행렬을 사용하여 인접한것이 있는지 없는지를 판단하는 행렬입니다.

> case1) 인접행렬

`A[i][j] = A[j][i] = 1`
와 같이 서로 연결되어 있는것들을 행렬형식으로 처리할 수 있습니다.

인접리스트는 연결리스트를 사용하여 그래프를 표현하는 방식입니다.
i->j 로 연결된 리스트가 있다고 가정하면 이것을 인접리스트로 표현하면 다음과 같습니다.

> case2) 인접리스트

`A[i] = {j}`
이렇게 표현할 수 있습니다. 이것의 의미하는 바는 어떻게 될까요? i의 정점에 연결된 j 정점입니다.

이해를 돕기위해서 1->2 가중치 1, 1->3 가중치2 이라고 해보면

> case 3) 인접리스트 - 가중치

`A[1] = {2,3}`
으로 표현 할 수 있습니다.
하지만, 그래프는 가중치가 존재할 수도있겠죠? 이럴때는 어떻게할까요?

`A[1] = {{2,1},{3,2}}`
과 같이 나타낼 수 있습니다.

## 11. 인접 리스트 VS 인접 행렬 시간복잡도 및 특징
시간복잡도의 차이점으로는 인접 리스트로 표현된 그래프: O(V+E), 인접 행렬로 표현된 그래프: O(V^2)로 나타낼 수 있습니다.

즉, 그래프 내에 적은 숫자의 간선만을 가지는 희소 그래프의 경우 인접 행렬보다 `인접 리스트를 사용하는 것이 시간복잡도면에서 뛰어납니다.`

## 12. 깊이 우선 탐색(DFS)

DFS는 말 그대로 깊이를 우선탐색하는 기법입니다. 진행시 깊이우선 계속해서 값이 있으면 최대깊이까지 들어가는것을 뜻합니다. 구현은 Stack이나 Recursive를 이용해서 갈 수 있는 만큼 최대 -> 갈수 없으면 이전 정점으로 돌아갑니다.

## 13. 넓이 우선 탐색(BFS)
BFS는 하나의 정점에서 갈 수 있는 모든정점을 방문하고 다음 깊이로 들어가게 됩니다.
큐를 이용하여 갈 수 있는 정점 모두 Queue -> insert를 해준후 먼저 넣고 -> Queue pop() 의 형식으로 이루어 집니다.

각각의 그래프 탐색 방식이 다르기 때문에, 구현하는 방법도 너무나도 다릅니다.
보통 DFS를 사용하게 되면 Stack을 사용하거나 재귀호출을 이용한 구현을 하게 되며, BFS를 사용하게 된다면 Queue를 이용하는 방식이라고 알고 계셔야합니다.



## 14. 인접리스트를 이용한 DFS,BFS 풀이
인접행렬과 인접리스트 이용한 백준 DFS BFS 1260번 문제를 예시로 가져와봤습니다.

[boj1260](https://www.acmicpc.net/problem/1260)

인접행렬
인접행렬을 이용한 풀이입니다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

/* Queue는 LinkedList 로 선언되어야한다
DFS 진행시 반드시 ArrayList나 LinkedList에 대한 값을 초기화 시켜주어야한다.
 */
public class 인접행렬 {
    static boolean[] check;
    static int[][] A;
    static int n;
    static int m;
    static int start;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        start = Integer.parseInt(st.nextToken());

        check = new boolean[n+1];
        A = new int[n+1][n+1];
        for(int i=0; i<m; i++){
            st = new StringTokenizer(br.readLine(), " ");
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());
            A[x][y] = 1;
            A[y][x] = 1;
        }
        //인접행렬시에는 정렬이 필요 없다!! 인접리스트만 필요하다.
        //자식이 여러개라면 노드 번호가 작은 것 먼저 방문하므로 오름차순으로 정렬
        dfs(start);
        Arrays.fill(check,false);
        System.out.println();
        bfs(start);
    }
    static void dfs(int x) {
        check[x] = true;
        System.out.print(x + " ");

        // 2. 인접 행렬
        for(int i=1; i<=n; i++){
            if(!check[i] && A[x][i] == 1){
                dfs(i);
            }
        }
    }
    static void bfs(int v) {
        Queue<Integer> q = new LinkedList<>();
        check[v] = true;
        q.offer(v);

        // 2. 인접 행렬
        while(!q.isEmpty()){
            int x = q.poll();
            System.out.print(x + " ");
            for(int i=1; i<=n; i++){
                if(!check[i] && A[x][i] == 1){
                    check[i] =true;
                    q.offer(i);
                }
            }
        }
    }
}
```
인접리스트
인접리스트를 이용한 풀이입니다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

/* Queue는 LinkedList 로 선언되어야한다
DFS 진행시 반드시 ArrayList나 LinkedList에 대한 값을 초기화 시켜주어야한다.
 */
public class DFSBFS_LIST1260 {
    static boolean[] check;
    static ArrayList<ArrayList<Integer>> A = new ArrayList<>();
    static int n;
    static int m;
    static int start;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        start = Integer.parseInt(st.nextToken());
        check = new boolean[n+1];

        for(int i=0; i<=n; i++){
            A.add(new ArrayList<Integer>());
        }

        for(int i=0; i<m; i++){
            st = new StringTokenizer(br.readLine(), " ");
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());
            A.get(x).add(y);
            A.get(y).add(x);
        }
        //자식이 여러개라면 노드 번호가 작은 것 먼저 방문하므로 오름차순으로 정렬을 해줬다.
        for(int i=0; i<=n; i++) {
            Collections.sort(A.get(i));
        }
        dfs(start);
        check = new boolean[n+1];
        System.out.println();
        bfs(start);
    }
    static void dfs(int x) {
        check[x] = true;
        System.out.print(x + " ");

        // 2. 인접 리스트
        for(int i=0; i<A.get(x).size(); i++){
            int y = A.get(x).get(i);
            if(!check[y]){
                dfs(y);
            }
        }
    }
    static void bfs(int v) {
        Queue<Integer> q = new LinkedList<>();
        check[v] = true;
        q.offer(v);
        // 2. 인접리스트
        while(!q.isEmpty()){
            int x = q.poll();
            System.out.print(x + " ");
            for(int i=0; i<A.get(x).size(); i++){
                int y = A.get(x).get(i);
                if(!check[y]){
                    check[y] = true;
                    q.offer(y);
                }
            }
        }
    }
}
```