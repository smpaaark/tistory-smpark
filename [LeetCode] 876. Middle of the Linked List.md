## 문제 설명
링크드리스트의 head 노드가 주어지면 중간 노드를 반환해야 한다. 이 때 노드의 개수가 짝수일 경우 두번째 중간 노드를 반환한다.

## 내가 푼 코드
```
public ListNode middleNode(ListNode head) {
    Map<Integer, ListNode> map = new HashMap<>();
    int index = 0;
    
    ListNode currentNode = head;
    while (currentNode != null) {
        map.put(index++, currentNode);
        currentNode = currentNode.next;
    }
    
    return map.get(index / 2);
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/middle-of-the-linked-list/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/linkedlist/Q876.java)