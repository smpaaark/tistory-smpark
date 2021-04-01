## 문제 설명
스택으로 배열 만들기

```target``` 배열과 정수 ```n```이 주어진다. ```list = {1,2,3..., n}```로 부터 각각 1개씩 숫자를 읽어들일 것이다.
다음 오퍼레이션을 사용하여 ```target``` 배열을 만들어라.:
* Push: ```list```의 첫번째 요소를 읽어서 array에 push 해라.
* Pop: array의 마지막 요소를 삭제해라.
* 만약 target 배열이 이미 완성됐으면 작업을 멈춰라.

target 배열을 만들기 위한 오퍼레이션들을 리턴해라. 정답은 반드시 존재한다.

## 내가 푼 코드
```
public List<String> buildArray(int[] target, int n) {
    List<String> list = new ArrayList<>();
    Stack<Integer> stack = new Stack<>();
    int currentNum = 1;
    int targetIndex = 0;
    while (currentNum <= n && targetIndex < target.length) {
        stack.push(currentNum++);
        list.add("Push");
        
        if (stack.peek() == target[targetIndex]) {
            targetIndex++;
        } else {
            stack.pop();
            list.add("Pop");
        }
    }
    
    return list;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## 다른 사람 코드
```
public List<String> buildArray_other(int[] target, int n) {
    LinkedList<String> res = new LinkedList<>();
    int i = 1;
    for (int num : target) {
        while(i < num && i < n) {
            ++i;
            res.add("Push");
            res.add("Pop");
        }
        ++i;
        res.add("Push");
    }
    return res;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)
> 시간/공간 복잡도는 같지만 아래코드는 스택을 만들지 않고 문제를 해결한 코드이다.

## Reference
* [문제](https://leetcode.com/problems/build-an-array-with-stack-operations/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/stack/Q1441.java)