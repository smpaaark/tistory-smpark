## 문제 설명
숫자를 0으로 줄이기 위한 단계의 수

음이 아닌 정수 ```num```이 주어지고, 이것을 0으로 줄이기 위한 단계의 수를 리턴해라. 만약 현재 수가 짝수이면 2로 나누고, 홀수이면 1을 빼라.

## 내가 푼 코드
```
public int numberOfSteps (int num) {
    int step = 0;
    while (num > 0) {
        if (num % 2 == 0) {
            num >>= 1;
        } else {
            num -= 1;
        }
        
        step++;
    }
    
    return step;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)

## 다른 사람 코드
```
public int numberOfSteps_other(int num) {
    int step = 0;
    while (num > 0) {
        if ((num & 1) == 0) {
            num >>= 1;
        } else {
            num -= 1;
        }
        
        step++;
    }
    
    return step;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)
> 짝수 체크를 비트 연산을 이용하여 ```if ((num & 1) == 0)```로 할 수 있다.

## Reference
* [문제](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-to-zero/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/bit/Q1342.java)