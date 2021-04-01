## 문제 설명
야구 게임

이상한 규칙이 있는 야구게임을 하고 있다. 게임은 여러개의 라운드로 구성되어 있으며, 과거 라운드의 점수가 미래 라운드의 점수에 영향을 줄 수도 있다.

게임이 시작되면 0점으로 시작한다. ```ops``` 문자열 배열이 주어지고, ```ops[i]```의 값에 따라 점수가 적용된다.
1. 정수 ```x``` - ```x```점이 기록된다.
2. ```"+"``` - 이전 2개의 점수를 합한 점수가 기록된다. 항상 이전에 2개의 점수가 있는 것이 보장된다.
3. ```"D"``` - 이전 점수의 2배의 점수가 기록된다. 항상 이전에 점수가 있는 것이 보장된다.
4. ```"C"``` - 이전 점수가 무효화 된다. 즉 이전 점수를 삭제한다. 항상 이전에 점수가 있는 것이 보장된다.

모든 점수의 합을 리턴해라.

## 내가 푼 코드
```
public int calPoints(String[] ops) {
    Stack<Integer> stack = new Stack<>();
    for (String op : ops) {
        if ("+".equals(op)) {
            int sumNum = 0;
            int[] temp = new int[2];
            for (int i = 0; i < 2; i++) {
                temp[i] = stack.pop();
                sumNum += temp[i];
            }
            
            for (int i = 1; i >= 0; i--) {
                stack.push(temp[i]);
            }
            
            stack.push(sumNum);
        } else if ("D".equals(op)) {
            stack.push(stack.peek() * 2);
        } else if ("C".equals(op)) {
            stack.pop();
        } else {
            stack.push(Integer.parseInt(op));
        }
    }
    
    int sum = 0;
    while (!stack.isEmpty()) {
        sum += stack.pop();
    }
    
    return sum;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/baseball-game/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/stack/Q682.java)