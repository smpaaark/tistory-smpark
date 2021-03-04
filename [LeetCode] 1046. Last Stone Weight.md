## 문제 설명
돌의 무게가 담겨있는 배열이 주어진다. 이때 가장 무게가 많이 나가는 2개의 돌을 충돌시키는데 2개 돌의 무게가 같으면 모두 사라지고, 무게가 다르면 큰 무게에서 작은 무게를 뺀 무게만큼의 돌로 남게 된다. 이 과정을 반복하여 마지막에 남는 돌의 무게를 반환해라.

## 내가 푼 코드
```
public int lastStoneWeight(int[] stones) {
    PriorityQueue<Integer> q = new PriorityQueue<>(Collections.reverseOrder());
    for (int num : stones) {
        q.offer(num);
    }
    
    while (q.size() > 1) {
        int result = q.poll() - q.poll();
        if (result > 0) {
            q.offer(result);
        }
    }
    
    return !q.isEmpty() ? q.poll() : 0;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/last-stone-weight/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/heap/Q1046.java)