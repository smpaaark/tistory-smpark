## 문제 설명
가장 부자인 고객의 재산

```m x n```인 정수형 2차원 배열 ```accounts```가 주어진다. 이때 ```accounts[i][j]```는 ```i```고객이 ```j```은행에 갖고있는 재산이다. 가장 부자인 고객의 재산을 리턴해라.

고객의 재산은 그 고객이 모든 은행에 갖고 있는 재산의 합이다. 가장 부자인 고객은 이 재산의 합이 가장 큰 고객이다.

## 내가 푼 코드
```
public int maximumWealth(int[][] accounts) {
    int maximumWealth = 0;
    for (int[] account : accounts) {
        int sum = 0;
        for (int amount : account) {
            sum += amount;
        }
        
        maximumWealth = Math.max(maximumWealth, sum);
    }
    
    return maximumWealth;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)

## Reference
* [문제](https://leetcode.com/problems/richest-customer-wealth/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/array/Q1672.java)