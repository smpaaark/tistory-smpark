## 문제 설명
이진 탐색 트리와 수의 범위가 low와 high로 주어진다. 해당 범위의 숫자들의 합을 반환해라.

## 내가 푼 코드
```
public int rangeSumBST(TreeNode root, int low, int high) {
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    
    int sum = 0;
    while (!q.isEmpty()) {
        TreeNode currentNode = q.poll();
        if (rangeCheck(currentNode.val, low, high)) {
            sum += currentNode.val;
        }
        
        if (currentNode.left != null) {
            q.offer(currentNode.left);
        }
        
        if (currentNode.right != null) {
            q.offer(currentNode.right);
        }
    }
    
    return sum;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## 다른 사람이 푼 코드
```
public int rangeSumBST_other(TreeNode root, int low, int high) {
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    
    int sum = 0;
    while (!q.isEmpty()) {
        TreeNode currentNode = q.poll();
        if (currentNode != null) {
            if (rangeCheck(currentNode.val, low, high)) {
                sum += currentNode.val;
            }
            
            if (low < currentNode.val) {
                q.offer(currentNode.left);
            }
            
            if (currentNode.val < high) {
                q.offer(currentNode.right);
            }
        }
    }
    
    return sum;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)
* 나는 왼쪽 노드와 오른쪽 노드를 큐에 넣을 때 null 체크만 했는데 위의 풀이는 low와 high를 이용하여 체크했다. 이 코드가 방문하지 않아도 되는 노드를 걸러낼 수 있어서 더 효율적이다.

## Reference
* [문제](https://leetcode.com/problems/range-sum-of-bst/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/tree/Q938.java)