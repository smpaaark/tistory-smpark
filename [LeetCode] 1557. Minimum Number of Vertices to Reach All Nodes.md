## 문제 설명
모든 노드에 도달하기 위한 꼭지점의 최소값

방향 비순환 그래프가 주어진다. ```0```부터 ```n-1```까지 이루어진 ```n```개의 꼭지점이 주어지고, ```edges```배열이 주어지는데 여기서 ```edges[i] = [from, to]```는 ```from```노드에서 ```to```노드로 방향이 가리킨다는 의미이다. 

그래프의 모든 노드에 연결할 수 있는 가장 작은 꼭짓점 집합을 찾아라. 정답은 항상 존재한다.

정답 순서는 무작위로 리턴해도 된다.

## 내가 푼 코드
```
public List<Integer> findSmallestSetOfVertices(int n, List<List<Integer>> edges) {
    boolean[] visit = new boolean[n];
    for (List<Integer> edge : edges) {
        if (!visit[edge.get(1)]) {
            visit[edge.get(1)] = true;
        }
    }
    
    List<Integer> result = new ArrayList<>();
    for (int i = 0; i < visit.length; i++) {
        if (!visit[i]) {
            result.add(i);
        }
    }
    
    return result;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/minimum-number-of-vertices-to-reach-all-nodes/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/graph/Q1557.java)