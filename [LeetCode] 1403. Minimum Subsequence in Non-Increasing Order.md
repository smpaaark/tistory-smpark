## 문제 설명
내림차순 최소 Subsequence

```nums```배열이 주어진다. 포함된 원소의 합이 포함되지 않은 원소의 합보다 큰 배열의 Subsequence를 얻어라.

만약 정답이 여러개 있을 경우, 크기가 가장 작은 배열을 리턴해라. 크기가 가장 작은 배열도 여러개일 경우 합이 제일 큰 배열을 리턴해라. Subsequence는 배열로부터 원소를 지우면서 얻을 수 있다.

정답은 유일하다. 정답은 내림차순으로 리턴해라.

## 내가 푼 코드
```
public List<Integer> minSubsequence(int[] nums) {
    PriorityQueue<Integer> queue = new PriorityQueue<>((a, b) -> {return b - a;});
    
    int sum = 0;
    for (int num : nums) {
        sum += num;
        queue.offer(num);
    }
    
    List<Integer> result = new ArrayList<>();
    int tempSum = 0;
    while (!queue.isEmpty()) {
        int tempNum = queue.poll();
        result.add(tempNum);
        if (sum - tempNum >= tempSum + tempNum) {
            sum -= tempNum;
            tempSum += tempNum;
        } else {
            return result;
        }
    }
    
    return result;
}
```
* 시간 복잡도: O(nlogn)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/minimum-subsequence-in-non-increasing-order/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/sort/Q1403.java)