## 문제 설명
소스에서 타겟으로의 모든 경로   

0 ~ n-1 까지의 라벨이 달린 n개의 노드가 주어지고 방향성 비순환 그래프로 이루어져 있다. 이때 0부터 n-1 노드까지 갈 수 있는 모든 경우의 수를 찾고 순서 상관 없이 반환해라.

그래프는 다음 규칙을 따른다: graph[i]는 i 노드에서 갈 수 있는 모든 노드를 갖고 있다. (즉, i 노드부터 graph[i][j] node까지의 방향성 엣지가 있는 것이다.)

## 내가 푼 코드
```
private List<List<Integer>> result = new ArrayList<>();

public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
		
    for (int i = 0; i < graph[0].length; i++) {
        boolean[] visit = new boolean[graph.length];
        ArrayList<Integer> path = new ArrayList<Integer>();
        path.add(0);
        visit[0] = true;
        dfs(graph[0][i], graph.length - 1, graph, visit, path);
    }
    
    return this.result;
}

private void dfs(int currentLabel, int lastLabel, int[][] graph, boolean[] visit, List<Integer> path) {
    if (visit[currentLabel]) {
        return;
    }
    
    if (currentLabel == lastLabel) {
        path.add(currentLabel);
        this.result.add(new ArrayList<>(path));
        return;
    }
    
    visit[currentLabel] = true;
    path.add(currentLabel);
    for (int i = 0; i < graph[currentLabel].length; i++) {
        if (!visit[graph[currentLabel][i]]) {
            dfs(graph[currentLabel][i], lastLabel, graph, visit, path);
            visit[graph[currentLabel][i]] = false;
            path.remove(path.size() - 1);
        }
    }
}
```
* 시간 복잡도: O(V + E)
* 공간 복잡도: O(E)
> DFS로 풀었는데 시간/공간 복잡도 계산이 어려워서 검색해본 결과 위와 같다고 한다. 여기서 V는 그래프의 길이, E는 모든 엣지의 수라고 한다. 이부분은 좀 더 공부가 필요할 듯 하다.

## Reference
* [문제](https://leetcode.com/problems/all-paths-from-source-to-target/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/graph/Q797.java)