## 문제 설명
바이너리 트리가 있을 때 위에서부터 아래로 가장 우측 노드의 값을 리스트로 반환해라.

## 큐를 이용한 풀이
```
public List<Integer> rightSideView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    
    if (root != null) {
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        
        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                TreeNode currentNode = q.poll();
                if (i == size - 1) {
                    result.add(currentNode.val);
                }
                
                if (currentNode.left != null) {
                    q.offer(currentNode.left);
                }
                
                if (currentNode.right != null) {
                    q.offer(currentNode.right);
                }
            }
        }
    }
    
    return result;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## 재귀를 이용한 풀이
```
public List<Integer> rightSideView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    addNumber(result, root, 1);
    return result;
}

private void addNumber(List<Integer> result, TreeNode root, int level) {
    if (root == null) {
        return;
    }
    
    if (level > maxLevel) {
        result.add(root.val);
        this.maxLevel = level;
    }
    
    addNumber(result, root.right, level + 1);
    addNumber(result, root.left, level + 1);
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

> 이번 문제는 혼자 해결하지 못해서 다른 사람들 코드를 참고했다. 재귀를 이용한 풀이와 큐를 이용한 풀이 둘 다 풀어봤는데 큐를 이용한 풀이가 좀 더 효율적인 것 같다.

## Reference
* [문제](https://leetcode.com/problems/binary-tree-right-side-view/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/queue/Q199.java)