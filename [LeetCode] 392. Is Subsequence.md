## 문제 설명
Subsequence 인가??

두개의 문자열 ```s```와 ```t```가 주어진다. ```s```가 ```t```의 subsequence인지 확인해라.

문자열의 subsequence는 원래 문자열로부터 위치와 상관없이 몇개의 문자가 삭제된 새로운 문자열이다. (예를들어, ```"abc"```는 ```"abcde"```의 subsequence이다. 반면에 ```"aec"```의 subsequence는 아니다.)

## 내가 푼 코드
```
public boolean isSubsequence(String s, String t) {
    if (s == null || s.trim().isEmpty()) {
        return true;
    }
    
    char[] sArray = s.toCharArray();
    char[] tArray = t.toCharArray();
    for (int sIndex = 0, tIndex = 0; sIndex < s.length() && tIndex < t.length(); ) {
        if (sArray[sIndex] == tArray[tIndex]) {
            sIndex++;
            tIndex++;
        } else {
            tIndex++;
        }
        
        if (sIndex == sArray.length) {
            return true;
        }
    }
    
    return false;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/is-subsequence/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/dp/Q392.java)