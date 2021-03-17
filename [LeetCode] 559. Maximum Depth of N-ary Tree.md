## 문제 설명
N-ary 트리의 최대 깊이

n-ary 트리가 주어지면 그것의 최대 깊이를 찾아라.
최대 깊이는 루트 노드부터 제일 먼 자식 노드까지의 가장 긴 경로의 노드 수이다.
Nary-Tree 각 그룹의 자식 노드는 null로 구분되어 삽입된다.(예제 참고)

## 내가 푼 코드
```
private int maxDepth = 0;

public int maxDepth(Node root) {
    if (root == null) {
        return 0;
    }
    
    dfs(root, 1);
    
    return this.maxDepth;
}

private void dfs(Node node, int depth) {
    if (depth > this.maxDepth) {
        this.maxDepth = depth;
    }
    
    if (node.children == null) {
        return;
    }
    
    for (Node child : node.children) {
        dfs(child, depth + 1);
    }
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/maximum-depth-of-n-ary-tree/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/dfs/Q559.java)