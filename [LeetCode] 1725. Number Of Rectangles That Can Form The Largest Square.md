## 문제 설명
가장 큰 사각형을 만들 수 있는 직사각형의 갯수

```rectangles[i] = [l, w]```인 ```rectangles``` 배열이 주어지고, ```l```은 길이 ```w```은 너비이다.
길이가 ```k```인 정사각형을 만들기 위해 ```i```번째 직사각형을 자를 수 있다. 이때 ```k <= l```이고 ```k <= w```이다.
예를들어 ```[4, 6]```직사각형을 잘라서 길이가 4인 정사각형을 만들 수 있다.
주어진 직사각형들로부터 만들 수 있는 정사각형의 가장 긴 ```maxLen```을 구하고, ```maxLen```인 정사각형의 갯수를 리턴해라.

## 내가 푼 코드
```
public int countGoodRectangles(int[][] rectangles) {
    int maxLen = 0;
    int result = 0;
    for (int i = 0; i < rectangles.length; i++) {
        int len = Math.min(rectangles[i][0], rectangles[i][1]);
        if (maxLen < len) {
            maxLen = len;
            result = 1;
        } else if (maxLen == len) {
            result++;
        }
    }
    
    return result;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)

## Reference
* [문제](https://leetcode.com/problems/number-of-rectangles-that-can-form-the-largest-square/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/greedy/Q1725.java)