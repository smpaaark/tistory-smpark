## 문제 설명
N번째 트리보나치 수

트리보나치 수는 다음과 같이 정의된다.
T0 = 0, T1 = 1, T2 = 1, and Tn+3 = Tn + Tn+1 + Tn+2 for n >= 0.
```n```이 주어지면 Tn 값을 리턴해라.

## 내가 푼 코드
```
public int tribonacci(int n) {
    if (n == 0) {
        return 0;
    } else if (n == 1 || n == 2) {
        num[n] = 1;
        return 1;
    }
    
    int result  = 0;
    result += num[n - 3] > 0 ? num[n - 3] : tribonacci(n - 3);
    result += num[n - 2] > 0 ? num[n - 2] : tribonacci(n - 2);
    result += num[n - 1] > 0 ? num[n - 1] : tribonacci(n - 1);
    
    num[n] = result;
    
    return result;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/n-th-tribonacci-number/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/recursion/Q1137.java)