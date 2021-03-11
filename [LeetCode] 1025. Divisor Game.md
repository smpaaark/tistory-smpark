## 문제 설명
약수 게임

Alice와 Bob이 번걸아가며 게임을 하고, Alice가 먼저 시작한다.

처음에 칠판에 N이라는 숫자가 주어진다. 각 플레이어 차례에 다음과 같이 행동한다:
* 0 < x < N과 N % x == 0 을 만족하는 x를 선택한다.
* 칠판의 숫자 N을 N - x로 바꾼다.

또한, 플레이어가 자기 차례에 위 조건에 만족하는 행동을 할 수 없다면 패배한 것이다.
두명 모두 최적의 행동을 한다고 가정하고 Alice가 이겼다면 True를 리턴해라.

## 내가 푼 코드
```
public boolean divisorGame(int N) {
    return (N % 2 == 0) ? true : false;
}
```
* 시간 복잡도: O(1)
* 공간 복잡도: O(1)

## Reference
* [문제](https://leetcode.com/problems/divisor-game/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/dp/Q1025.java)