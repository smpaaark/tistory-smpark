## 문제 설명
주식 사고 팔기 최적의 시간

prices 배열이 주어진다. 이때 prices[i]는 i날짜의 주식 가격이다.
너는 한 날짜에 주식을 사고 다른 한 날짜에 주식을 팔아서 최대 이익을 남기길 원한다.
이 거래로부터 너가 성취할 수 있는 최대 이익 값을 리턴해라. 만약 조금의 이익도 남기지 못할 경우에는 0을 리턴해라.

## 내가 푼 코드
```
public int maxProfit(int[] prices) {
    int minBuy = prices[0];
    int maxProfit = 0;
    for (int i = 1; i < prices.length; i++) {
        maxProfit = Math.max(maxProfit, prices[i] - minBuy);
        minBuy = Math.min(minBuy, prices[i]);
    }
    
    return maxProfit;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)

## Reference
* [문제](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/dp/Q121.java)