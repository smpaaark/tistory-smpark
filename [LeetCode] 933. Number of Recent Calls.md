## 문제 설명
RecentCounter 클래스를 구현한다. ping이라는 메서드가 있는데 시간이 파라미터로 주어진다. 이때 시간은 점점 증가한다. 그동안 들어온 ping 중에 [t - 3000, t] 시간에 해당하는 ping의 개수를 반환한다.

## 내가 푼 코드
```
class RecentCounter {
		
    private Queue<Integer> q;
    
    public RecentCounter() {
        q = new LinkedList<>();
    }
    
    public int ping(int t) {
        q.offer(t);
        
        while (!q.isEmpty()) {
            if (q.peek() >= t - 3000 && q.peek() <= t) {
                break;
            } else {
                q.poll();
            }
        }
        
        return q.size();
    }
    
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)

## Reference
* [문제](https://leetcode.com/problems/number-of-recent-calls/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/queue/Q933.java)