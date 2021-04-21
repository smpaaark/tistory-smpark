## 문제 설명
연속된 배열로 부터 산술 진행을 할 수 있는지 여부

숫자 배열 ```arr```가 주어진다. 연속된 두 개의 숫자 간의 차이가 같은 배열을 산술 진행 배열이라고 불린다.

해당 배열이 산술 진행 배열이면 ```true```, 아니면 ```false```를 리턴해라.

## 내가 푼 코드
```
public boolean canMakeArithmeticProgression(int[] arr) {
    PriorityQueue<Integer> queue = new PriorityQueue<>();
    for (int num : arr) {
        queue.offer(num);
    }
    
    int differrence = queue.poll() - queue.peek();
    int before = queue.poll();
    while (!queue.isEmpty()) {
        int temp = before - queue.peek();
        if (temp != differrence) {
            return false;
        }
        before = queue.poll();
    }
    
    return true;
}
```
* 시간 복잡도: O(nlogn)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/can-make-arithmetic-progression-from-sequence/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/sort/Q1502.java)