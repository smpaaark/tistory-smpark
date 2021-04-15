## 문제 설명
정렬된 모음 문자열의 갯수

정수 ```n```이 주어진다. 길이가 ```n```인 문자열의 갯수를 리턴해라. 모음은 ```(a, e, i, o, u)```로 구성되어있으며, 사전순으로 정렬되어 있다.
문자열 ```s```는 사전순으로 정렬되며 ```s[i + 1]```은 ```s[i]```와 같거나 이후의 문자이다.

## 내가 푼 코드
```
private static String[] vowel = {"a", "e", "i", "o", "u"};

public int countVowelStrings(int n) {
    Set<String> set = new HashSet<>();
    for (int i = 0; i < vowel.length; i++) {
        backTracking(i, vowel[i], n, set);
    }
    
    return set.size();
}

private void backTracking(int startIndex, String currentString, int n, Set<String> set) {
    if (currentString.length() == n) {
        if (!set.contains(currentString)) {
            set.add(currentString);
        }
        
        return;
    }
    
    for (int i = startIndex; i < vowel.length; i++) {
        backTracking(i, currentString + vowel[i], n, set);
    }
}
```
* 시간 복잡도: ??
* 공간 복잡도: O(n)
> 백트래킹 시간복잡도 계산이 어렵다...공부해보자..

## Reference
* [문제](https://leetcode.com/problems/count-sorted-vowel-strings/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/backtracking/Q1641.java)