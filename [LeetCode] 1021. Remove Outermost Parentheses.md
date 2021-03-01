## 문제 설명
괄호 쌍이 문자열로 주어진다. 이때 유효한 괄호 쌍에 대한 가장 바깥쪽 괄호 쌍들을 제거한 후 문자열을 반환해야 한다.

## 내가 푼 코드
```
public String removeOuterParentheses(String S) {
    Stack<Character> stack = new Stack<>();
    StringBuilder sb = new StringBuilder();
    
    for (int i = 0; i < S.length(); i++) {
        char c = S.charAt(i);
        if (stack.isEmpty()) {
            stack.push(c);
        } else if (c == '(') {
            sb.append(c);
            stack.push(c);
        } else if (c == ')' && stack.size() > 1) {
            sb.append(c);
            stack.pop();
        } else {
            stack.pop();
        }
    }
    
    return sb.toString();
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/remove-outermost-parentheses/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/stack/Q1021.java)