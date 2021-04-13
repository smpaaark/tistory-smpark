## 문제 설명
두개의 정렬된 리스트 합치기

두개의 정렬된 링크드 리스트를 합쳐라. 그리고 그 리스트를 정렬하여 리턴해라. 리스트는 오름차순으로 정렬되어야 한다.

## 내가 푼 코드
```
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    if (l1 == null && l2 == null) {
        return null;
    }
    
    ListNode newNode = new ListNode(101);
    recursion(l1, l2, newNode);
    
    return newNode.next;
}

private void recursion(ListNode l1, ListNode l2, ListNode newNode) {
    if (l1 == null && l2 == null) {
        return;
    } 
    
    ListNode temp1 = null;
    ListNode temp2 = null;
    if (l1 != null && l2 == null) {
        newNode.next = new ListNode(l1.val);
        temp1 = l1.next;
    } else if (l1 == null && l2 != null) {
        newNode.next = new ListNode(l2.val);
        temp2 = l2.next;
    } else {
        if (l1.val < l2.val) {
            newNode.next = new ListNode(l1.val);
            temp1 = l1.next;
            temp2 = l2;
        } else {
            newNode.next = new ListNode(l2.val);
            temp1 = l1;
            temp2 = l2.next;
        }
    }
    
    recursion(temp1, temp2, newNode.next);
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/merge-two-sorted-lists/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/recursion/Q21.java)