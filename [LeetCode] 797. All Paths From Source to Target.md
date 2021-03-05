## 문제 설명
소스에서 타겟으로의 모든 경로   

0 ~ n-1 까지의 라벨이 달린 n개의 노드가 주어지고 방향성 비순환 그래프로 이루어져 있다. 이때 0부터 n-1 노드까지 갈 수 있는 모든 경우의 수를 찾고 순서 상관 없이 반환해라.

그래프는 다음 규칙을 따른다: graph[i]는 i 노드에서 갈 수 있는 모든 노드를 갖고 있다. (즉, i 노드부터 graph[i][j] node까지의 방향성 엣지가 있는 것이다.)

## 내가 푼 코드
```
public int findJudge(int N, int[][] trust) {
    if (N < 2) {
        return N;
    }
    
    List<Integer>[] graph = new ArrayList[N + 1];
    for (int i = 1; i < graph.length; i++) {
        graph[i] = new ArrayList<>();
    }
    
    Map<Integer, Integer> map = new HashMap<>();
    for (int[] array : trust) {
        graph[array[0]].add(array[1]);
        map.put(array[1], map.getOrDefault(array[1], 0) + 1);
    }
    
    for (int i = 1; i < graph.length; i++) {
        if (graph[i].size() == 0 && map.getOrDefault(i, 0) == N - 1) {
            return i;
        }
    }
    
    return -1;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/find-the-town-judge/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/graph/Q997.java)