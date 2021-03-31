## 문제 설명
링크드 리스트 뒤집기

단일 링크드 리스트의 ```head```가 주어지면 리스트를 뒤집어라. 그리고 뒤집어진 리스트를 리턴해라.

## 내가 푼 코드
```
public ListNode reverseList(ListNode head) {
    if (head == null || head.next == null) {
        return head;
    }
    
    ListNode currentNode = head;
    ListNode prevNode = null;
    ListNode nextNode = null;
    while (currentNode.next != null) {
        nextNode = currentNode.next;
        currentNode.next = prevNode;
        prevNode = currentNode;
        currentNode = nextNode;
    }
    
    currentNode.next = prevNode;
    head = currentNode;
    
    return head;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)

## Reference
* [문제](https://leetcode.com/problems/reverse-linked-list/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/linkedlist/Q206.java)