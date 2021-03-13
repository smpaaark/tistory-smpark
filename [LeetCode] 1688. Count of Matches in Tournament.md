## 문제 설명
토너먼트의 경기 수

이상한 규칙이 있는 토너먼트의 팀의 수인 정수 ```n```이 주어진다. 

* 만약 현재 팀의 수가 짝수이면 각 팀은 다른 한 팀과 쌍을 이뤄 경기를 한다. 총 ```n / 2```개의 경기가 진행되고 ```n / 2```개의 팀이 다음 라운드에 진출한다.
* 만약 현재 팀의 수가 홀수이면 무작위로 한 팀은 자동으로 다음 라운드에 진출하고 남은 팀들은 쌍을 이뤄 경기를 한다. 총 ```(n - 1) / 2```개의 경기가 진행되고 ```(n - 1) / 2 + 1```개의 팀이 다음 라운드에 진출한다.

이 토너먼트의 우승팀이 결정될 때까지의 총 경기 수를 리턴해라.

## 내가 푼 코드 (반복문)
```
public int numberOfMatches(int n) {
    int count = 0;
    while (n > 1) {
        if (n % 2 == 0) {
            count += n / 2;
            n /= 2;
        } else {
            count += (n - 1) / 2;
            n = (n - 1) / 2 + 1;
        }
    }
    
    return count;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)


## 내가 푼 코드 (BackTracking)
```
public int numberOfMatches_backtracking(int n) {
    return backtracking(n);
}

private int backtracking(int n) {
    if (n == 1) {
        return 0;
    }
    
    if (n % 2 == 0) {
        return (n / 2) + backtracking(n / 2);
    } else {
        return ((n - 1) / 2) + backtracking((n - 1) / 2 + 1);
    }
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/count-of-matches-in-tournament/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/backtracking/Q1688.java)