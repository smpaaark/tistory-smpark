## 문제 설명
작업 스케쥴러

char형 배열 ```tasks```이 주어지고, 이것은 CPU가 해야할 작업 리스트이다. 여기서 문자는 각각 다른 작업이다. 작업은 무작위로 수행된다. 각 작업은 한번에 한개씩만 수행된다. 각 시간마다 CPU는 작업이 수행되거나 수행되지 않을 수 있다. 

동일한 두 작업 사이의 냉각 기간을 나타내는 음이 아닌 정수 ```n```이 있다. (배열 안의 같은 문자). 즉, 동일한 두 작업 사이에 최소한 ```n``` 단위의 시간이 있어야 한다.

CPU가 지정된 모든 작업을 완료하는 데 걸리는 최소 단위 수를 리턴해라.

## 내가 푼 코드
```
public int leastInterval(char[] tasks, int n) {
    int[] counts = new int[26];
    for (char c : tasks) {
        counts[c - 'A']++;
    }
    
    Queue<Integer> queue = new PriorityQueue<>((a ,b) -> b - a);
    for (int count : counts) {
        if (count > 0) {
            queue.offer(count);
        }
    }
    
    int maxTask = queue.poll();
    int idle = (maxTask - 1) * n;
    
    while (!queue.isEmpty()) {
        int temp = Math.min(queue.peek(), maxTask - 1);
        if (idle - temp >= 0) {
            idle -= Math.min(queue.poll(), maxTask - 1);
        } else {
            idle = 0;
            break;
        }
    }
    
    return tasks.length + idle;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)
> 이 문제 해결하는데 몇일은 걸린 것 같다. 물론 요즘 너무 바빠서 공부하는 시간이 부족했던 것도 있지만 문제 자체가 너무 어려웠다...

## Reference
* [문제](https://leetcode.com/problems/task-scheduler/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/queue/Q621.java)