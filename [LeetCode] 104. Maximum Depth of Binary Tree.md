## 문제 설명
이진 트리의 가장 큰 깊이

```root```라는 이진 트리가 주어지고, 깊이의 최대값을 반환해라.

이 이진 트리 깊이의 최대값은 루트 노드부터 가장 먼 자식 노드까지의 노드 수이다.

## 내가 푼 코드
```
public int maxDepth(TreeNode root) {
    recursion(root, 1);
    
    return this.maxDepth;
}

private void recursion(TreeNode root, int currentDepth) {
    if (root == null) {
        return;
    }
    
    if (currentDepth > this.maxDepth) {
        this.maxDepth = currentDepth;
    }
    
    recursion(root.left, currentDepth + 1);
    recursion(root.right, currentDepth + 1);
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/recursion/Q104.java)