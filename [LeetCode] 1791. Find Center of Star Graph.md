## 문제 설명
별 그래프의 중앙을 찾아라

```1```부터 ```n```까지의 노드로 구성된 비연결 별그래프가 있다. 별 그래프는 중앙에 한개의 노드가 있고 정확하게 ```n-1```개의 엣지가 중앙 노드로부터 다른노드와 연결되어 있다.

```edges``` 정수형 2차배열이 주어지고 각 ```edges[i] = [u, v]```는 ```u```노드와 ```v```노드사이의 엣지를 나타낸다. 별 그래프의 중앙 노드를 리턴해라.

## 내가 푼 코드
```
public int findCenter(int[][] edges) {
    Set<Integer> set = new HashSet<>();
    for (int[] edge : edges) {
        for (int i = 0; i < 2; i++) {
            if (set.contains(edge[i])) {
                return edge[i];
            } else {
                set.add(edge[i]);
            }
        }
    }
    
    return 0;
}
```
* 시간 복잡도: O(1)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/find-center-of-star-graph/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/graph/Q1791.java)