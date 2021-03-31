## 문제 설명
링크드 리스트의 노드 삭제

단일 링크드 리스트의 노드를 삭제하기 위한 함수를 작성해라. ```head```노드는 주어지지 않고, 삭제될 노드가 주어진다.
삭제될 노드는 리스트의 꼬리 노드는 반드시 아니다.

## 내가 푼 코드
```
public void deleteNode(ListNode node) {
    node.val = node.next.val;
    node.next = node.next.next;
}
```
* 시간 복잡도: O(1)
* 공간 복잡도: O(1)

## Reference
* [문제](https://leetcode.com/problems/delete-node-in-a-linked-list/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/linkedlist/Q237.java)