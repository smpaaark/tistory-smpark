## 문제 설명
보석과 돌

보석(jewels) 문자열과 돌(stones) 문자열이 주어진다. stones 문자열의 Character 1개가 1개의 돌이다. 내가 가진 돌 중 보석이 몇 개인지 알고 싶다.

대문자 소문자를 구분한다. ('a'와 'A'는 다르다.)

## 내가 푼 코드
```
public int numJewelsInStones(String jewels, String stones) {
    Set<Character> set = new HashSet<>();
    for (int i = 0; i < jewels.length(); i++) {
        if (!set.contains(jewels.charAt(i))) {
            set.add(jewels.charAt(i));
        }
    }
    
    int result = 0;
    for (int i = 0; i < stones.length(); i++) {
        if (set.contains(stones.charAt(i))) {
            result++;
        }
    }
    
    return result;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## 다른 사람이 푼 코드
```
public int numJewelsInStones_other(String J, String S) {
    if(J == null || J.isEmpty() || S == null || S.isEmpty()) return 0;
    
    int[] dict = new int[128];
    
    for(int i = 0; i < J.length(); i++){
        ++dict[J.charAt(i)];
    }
    
    int count = 0;
    for(int i = 0; i < S.length(); i++){
        if(dict[S.charAt(i)] > 0){
            count++;
        }
    }
    return count;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)
> 나는 Set을 이용하여 풀었으나 다른 사람은 배열과 아스키코드를 이용하여 풀었다. Character 관련 문제는 아스키코드로 푸는 방법도 고려해야겠다.

## Reference
* [문제](https://leetcode.com/problems/jewels-and-stones/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/hashtable/Q771.java)