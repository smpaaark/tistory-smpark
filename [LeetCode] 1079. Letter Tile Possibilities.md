## 문제 설명
편지 타일 가능성

```n``` ```tiles```를 갖고있고, 각 타일은 ```tiles[i]```에 해당하는 문자가 새겨져 있다.
만들 수 있는 모든 ```tiles```의 조합 갯수를 리턴해라.

## 내가 푼 코드
```
public int numTilePossibilities(String tiles) {
    char[] charArray = tiles.toCharArray();
    Set<String> set = new HashSet<>();
    Map<Character, Integer> map = new HashMap<>();
    for (char c : charArray) {
        if (map.containsKey(c)) {
            map.put(c, map.get(c) + 1);
        } else {
            map.put(c, 1);
        }
    }
    
    for (int i = 0; i < charArray.length; i++) {
        map.put(charArray[i], map.get(charArray[i]) - 1);
        backTracking(String.valueOf(charArray[i]), charArray, set, map);
        map.put(charArray[i], map.get(charArray[i]) + 1);
    }
    
    return set.size();
}

private void backTracking(String currentLetter, char[] charArray, Set<String> set, Map<Character, Integer> map) {
    if (currentLetter.length() == charArray.length) {
        if (!set.contains(currentLetter)) {
            set.add(currentLetter);
        }
        
        return;
    }
    
    if (!set.contains(currentLetter)) {
        set.add(currentLetter);
    }
    
    for (int i = 0; i < charArray.length; i++) {
        if (map.get(charArray[i]) > 0) {
            map.put(charArray[i], map.get(charArray[i]) - 1);
            backTracking(currentLetter + charArray[i], charArray, set, map);
            map.put(charArray[i], map.get(charArray[i]) + 1);
        }
    }
}
```
* 시간 복잡도: ??
* 공간 복잡도: O(n)
> 백트래킹 시간복잡도 계산이 어렵다...공부해보자..

## Reference
* [문제](https://leetcode.com/problems/n-th-tribonacci-number/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/backtracking/Q1079.java)