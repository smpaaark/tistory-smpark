## 문제 설명
유일한 요소의 합

정수형 배열 ```nums```가 주어진다. 배열의 유일한 요소는 배열에서 정확히 1개씩만 존재한다.
```nums```배열에서 유일한 요소들의 합을 리턴해라.

## 내가 푼 코드
```
public int sumOfUnique(int[] nums) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int num : nums) {
        if (map.containsKey(num)) {
            map.put(num, map.get(num) + 1);
        } else {
            map.put(num, 1);
        }
    }
    
    int result = 0;
    for (int key : map.keySet()) {
        if (map.get(key) == 1) {
            result += key;
        }
    }
    
    return result;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/sum-of-unique-elements/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/hashtable/Q1748.java)