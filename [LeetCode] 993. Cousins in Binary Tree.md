## 문제 설명
이진 트리 사촌

이진 트리에서 루트 노드는 깊이가 ```0```이고, 각각의 깊이가 ```k```인 노드의 자식 노드들은 깊이가 ```k+1```이다.
만약 노드끼리 깊이가 같다면 이진 트리의 두 노드는 사촌이다. 그러나 부모가 다르다. 
유일한 값들을 가진 이진 트리의 ```root```가 주어지고, ```x```와 ```y```값을 가진 다른 두 노드가 주어진다.

만약 ```x```와 ```y```값을 가진 두 노드가 사촌이면 ```ture```를 리턴해라.

## 내가 푼 코드
```
public boolean isCousins(TreeNode root, int x, int y) {
    Queue<TreeNode> q = new LinkedList<>(); // 공간 n
    Map<Integer, Integer> map = new HashMap<>(); // 공간 n
    q.offer(root);
    map.put(root.val, 0);
    
    while (!q.isEmpty()) { // 시간 n
        TreeNode currentNode = q.poll();
        if (currentNode.left != null && currentNode.right != null) {
            if ((currentNode.left.val == x && currentNode.right.val == y) || (currentNode.left.val == y && currentNode.right.val == x)) {
                return false;
            }
        }
        
        if (currentNode.left != null) {
            q.offer(currentNode.left);
            map.put(currentNode.left.val, map.get(currentNode.val) + 1);
        }
        
        if (currentNode.right != null) {
            q.offer(currentNode.right);
            map.put(currentNode.right.val, map.get(currentNode.val) + 1);
        }
    }
    
    if (map.get(x) == map.get(y)) {
        return true;
    }
    
    return false;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/cousins-in-binary-tree/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/bfs/Q993.java)