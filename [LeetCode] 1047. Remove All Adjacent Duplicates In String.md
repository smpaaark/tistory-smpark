## 문제 설명
주어진 문자열에서 인접한 문자열을 제거한다. 이때 인접한 문자열을 제거한 후의 문자열에서도 인접한 문자열이 있을 경우 제거해야 한다.

## 내가 푼 코드
```
public String removeDuplicates(String S) {
    Stack<Character> stack = new Stack<>();
    
    for (int i = S.length() - 1; i >= 0; i--) {
        if (stack.isEmpty() || stack.peek() != S.charAt(i)) {
            stack.push(S.charAt(i));
        } else {
            stack.pop();
        }
    }
    
    StringBuilder sb = new StringBuilder();
    while (!stack.isEmpty()) {
        sb.append(stack.pop());
    }
    
    return sb.toString();
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/stack/Q1047.java)