## 문제 설명
리프 유사 트리

이진 트리 왼쪽부터 오른쪽까지의 모든 리프들을 고려해라. 리프들의 값은 리프의 순서를 형성한다.

예를 들면, 위 그림에서(문제 링크 참조) 리프 값의 순서는 (6, 7, 4, 9, 8)이다.
이진트리는 리프 값의 순서가 같으면 유사 리프로 여겨진다. 
만약 ```root1```과 ```root2```가 유사 리프라면 ```true```를 리턴해라.

## 내가 푼 코드
```
public boolean leafSimilar(TreeNode root1, TreeNode root2) {
    List<Integer> list1 = new ArrayList<>();
    List<Integer> list2 = new ArrayList<>();
    dfs(root1, list1);
    dfs(root2, list2);
    return similarCheck(list1, list2);
}

private boolean similarCheck(List<Integer> list1, List<Integer> list2) {
    if (list1.size() != list2.size()) {
        return false;
    }
    
    for (int i = 0; i < list1.size(); i++) {
        if (list1.get(i) != list2.get(i)) {
            return false;
        }
    }
    
    return true;
}

private void dfs(TreeNode node, List<Integer> list) {
    if (node.left == null && node.right == null) {
        list.add(node.val);
        return;
    }
    
    if (node.left != null) {
        dfs(node.left, list);
    }
    
    if (node.right != null) {
        dfs(node.right, list);
    }
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/leaf-similar-trees/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/dfs/Q872.java)