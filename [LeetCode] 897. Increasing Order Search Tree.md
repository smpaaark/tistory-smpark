## 문제 설명
오름차순 탐색 트리

이진 탐색 트리인 ```root```가 주어진다. 이 트리의 가장 왼쪽 노드가 루트가 되도록 오름차순으로 재배열해라. 그리고 모든 노드는 오른쪽 자식 노드만 갖는다.

## 내가 푼 코드
```
public TreeNode increasingBST(TreeNode root) {
    TreeNode result = new TreeNode();
    recursion(root, result);
    return result.right;
}

private TreeNode recursion(TreeNode currentNode, TreeNode result) {
    if (currentNode == null) {
        return result;
    }
    
    TreeNode temp = recursion(currentNode.left, result);
    temp.right = new TreeNode(currentNode.val);
    return recursion(currentNode.right, temp.right);
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/increasing-order-search-tree/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/recursion/Q897.java)