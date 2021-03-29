## 문제 설명
균형있는 문자열에서 한 문자열 자르기

균형있는 문자열은 ```'L'```과 ```'R'```을 같은 갯수로 갖고 있는 문자열이다.
균형있는 ````'s'```이 주어지고, 가장 많은 양의 균형있는 문자열이 되게 잘라라.
잘려진 균형있는 문자열의 최대 수를 리턴해라.

## 내가 푼 코드
```
public int balancedStringSplit(String s) {
    int rCount = 0;
    int lCount = 0;
    int result = 0;
    for (char c : s.toCharArray()) {
        if (c == 'R') {
            rCount++;
        } else if (c == 'L') {
            lCount++;
        }
        
        if (rCount == lCount) {
            result++;
            rCount = 0;
            lCount = 0;
        }
    }
    
    return result;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)

## Reference
* [문제](https://leetcode.com/problems/split-a-string-in-balanced-strings/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/greedy/Q1221.java)