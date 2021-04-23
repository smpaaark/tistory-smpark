## 문제 설명
정렬된 배열을 이진 탐색 트리로 전환하기

오름차순으로 정렬된 정수형 배열 ```nums```가 주어진다. 이것을 height-balanced 이진 탐색 트리로 변환해라.
height-balanced 이진 탐색 트리는 모든 노드의 두 하위 트리의 깊이가 둘 이상 차이가 나지 않는 이진 트리이다.

## 내가 푼 코드
```
public TreeNode sortedArrayToBST(int[] nums) {
    int middleIndex = (nums.length - 1) / 2;
    TreeNode headNode = new TreeNode(nums[middleIndex]);
    
    headNode.left = dfs(0, middleIndex - 1, nums);
    headNode.right = dfs(middleIndex + 1, nums.length - 1, nums);
    
    return headNode;
}


private TreeNode dfs(int startIndex, int endIndex, int[] nums) {
    if (startIndex > endIndex) {
        return null;
    }
    
    int middleIndex = (startIndex + endIndex) / 2;
    
    TreeNode node = new TreeNode(nums[middleIndex]);
    node.left = dfs(startIndex, middleIndex - 1, nums);
    node.right = dfs(middleIndex + 1, endIndex, nums);
    
    return node;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/dfs/Q108.java)