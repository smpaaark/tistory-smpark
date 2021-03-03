## 문제 설명
두 개의 이진 트리가 주어진다. 두 트리를 병합한 결과를 반환한다. 병합되는 노드의 값은 양 노드의 합이 된다.

## 내가 푼 코드
```
public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
    if (root1 == null && root2 == null) {
        return null;
    }
    
    Queue<TreeNode> root1Q = new LinkedList<>();
    Queue<TreeNode> root2Q = new LinkedList<>();
    
    root1 = root1 != null ? root1 : new TreeNode();
    root1Q.offer(root1);
    root2Q.offer(root2 != null ? root2 : new TreeNode());
    
    while (!root1Q.isEmpty()) {
        TreeNode currentNode1 = root1Q.poll();
        TreeNode currentNode2 = root2Q.poll();
        currentNode1.val += currentNode2.val;
        
        if (currentNode1.left != null && currentNode2.left != null) {
            root1Q.offer(currentNode1.left);
            root2Q.offer(currentNode2.left);
        } else if (currentNode1.left != null && currentNode2.left == null) {
            currentNode2.left = new TreeNode();
            root1Q.offer(currentNode1.left);
            root2Q.offer(currentNode2.left);
        } else if (currentNode1.left == null && currentNode2.left != null) {
            currentNode1.left = new TreeNode();
            root1Q.offer(currentNode1.left);
            root2Q.offer(currentNode2.left);
        }
        
        if (currentNode1.right != null && currentNode2.right != null) {
            root1Q.offer(currentNode1.right);
            root2Q.offer(currentNode2.right);
        } else if (currentNode1.right != null && currentNode2.right == null) {
            currentNode2.right = new TreeNode();
            root1Q.offer(currentNode1.right);
            root2Q.offer(currentNode2.right);
        } else if (currentNode1.right == null && currentNode2.right != null) {
            currentNode1.right = new TreeNode();
            root1Q.offer(currentNode1.right);
            root2Q.offer(currentNode2.right);
        }
    }
    
    return root1;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## 다른 사람이 푼 코드
```
private TreeNode mergeTrees_other(TreeNode root1, TreeNode root2) {
    if (root1 == null) {
        return root2;
    }
    
    if (root2 == null) {
        return root1;
    }
    
    root1.val += root2.val;
    
    root1.left = mergeTrees_other(root1.left, root2.left);
    root1.right = mergeTrees_other(root1.right, root2.right);
    
    return root1;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)
* 나는 큐를 이용하여 풀었고, 다른 사람이 푼 코드는 재귀를 이용하여 풀었다. 재귀로 푸는 게 코드가 더 깔끔하다.

## Reference
* [문제](https://leetcode.com/problems/merge-two-binary-trees/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/tree/Q617.java)