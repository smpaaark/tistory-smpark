## 문제 설명
계단을 오르기 위한 최소 비용

정수형 배열 ```cost```가 주어진다. ```cost[i]```는 ``i``번째 계단을 오르기 위한 비용이다. 한번 비용을 지불할 때 1계단 또는 2계단을 오를 수 있다.

또한 ```0```번째 또는 ```1```번째 계단부터 시작할 수 있다.

가장 윗 계단에 도착하기 위한 최소 비용을 리턴해라.

## 내가 푼 코드
```
public int minCostClimbingStairs(int[] cost) {
    int[] dp = new int[cost.length + 1];
    for (int i = 2; i < dp.length; i++) {
        dp[i] = Math.min(dp[i - 2] + cost[i - 2], dp[i - 1] + cost[i - 1]);
    }
    
    return dp[dp.length - 1];
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/min-cost-climbing-stairs/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/dp/Q746.java)