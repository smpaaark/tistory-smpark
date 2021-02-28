## 문제 설명
링크드리스트의 head 노드가 주어지고 각 노드에는 0 또는 1인 2진수가 값으로 들어있다. 링크드리스트를 순회하여 2진수를 10진수로 바꿔야 한다.

## 내가 푼 코드
```
public int getDecimalValue(ListNode head) {
		int size = 0;
		ListNode currentNode = head;
		while (currentNode != null) {
			size++;
			currentNode = currentNode.next;
		}
		
		int result = 0;
		currentNode = head;
		while (currentNode != null) {
			size--;
			if (currentNode.val == 1) {
				result += Math.pow(2, size);
			}
			
			currentNode = currentNode.next;
		}
		
		return result;
	}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)

## 다른 사람 코드
```
public int getDecimalValue_other(ListNode head) {
    ListNode currentNode = head;
    StringBuilder sb = new StringBuilder();
    while (currentNode != null) {
        sb.append(currentNode.val);
        currentNode = currentNode.next;
    }
    
    return Integer.parseInt(sb.toString(), 2);
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)
* Integer.parseInt를 이용하여 이진수를 십진수로 바꿀 수 있다는 것을 알게 되었다.

## Reference
* [문제](https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/linkedlist/Q1290.java)
* [다른 사람 코드](https://github.com/ashutosh049/Leetcode-1/blob/master/src/main/java/com/fishercoder/solutions/_1290.java)