## 문제 설명
KthLargest라는 클래스를 구현한다. 생성자 파라미터로 k와 nums라는 int형 배열이 주어진다. add(int val) 메서드는 val을 추가하면 그동안의 숫자들에 val을 추가한 뒤 k번째로 큰 숫자를 반환한다.

## 내가 푼 코드
```
class KthLargest {
		
    private int k;
    private PriorityQueue<Integer> q = new PriorityQueue<>();
    
    public KthLargest(int k, int[] nums) {
        this.k = k;
        for (int num : nums) {
            this.q.offer(num);
        }
    }
    
    public int add(int val) {
        this.q.offer(val);
        int size = q.size();
        
        while (size-- != k) {
            q.poll();
        }
        
        return q.peek();
    }
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)
> 처음에 최대힙으로 풀었는데 시간 초과가 떴다. 그래서 다른 사람 코드를 참고했더니 최소힙으로 풀면 어차피 작은 값들은 필요 없는 값이므로 poll 하면서 큐의 크기를 줄일 수 있었다. (최대힙으로 풀면 임시 배열이 필요했으나 최소힙으로 풀면 임시 배열이 필요 없어짐)

## Reference
* [문제](https://leetcode.com/problems/kth-largest-element-in-a-stream/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/heap/Q703.java)