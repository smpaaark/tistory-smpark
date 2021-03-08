## 문제 설명
좋은 쌍의 수

정수형 nums 배열이 주어진다.   
nums[i] == nums[j]이고 i < j인 (i, j)쌍은 좋다고 여겨진다.

좋은 쌍의 수를 반환해라.

## 내가 푼 코드
```
public int numIdenticalPairs(int[] nums) {
    Map<Integer, List<Integer>> map = new HashMap<>();
    int result = 0;
    for (int i = 0; i < nums.length; i++) {
        if (map.containsKey(nums[i])) {
            result += map.get(nums[i]).size();
            map.get(nums[i]).add(i);
        } else {
            List<Integer> list = new ArrayList<>();
            list.add(i);
            map.put(nums[i], list);
        }
    }
    
    return result;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## 다른 사람이 푼 코드
```
public int numIdenticalPairs_other(int[] nums) {
    int[] hash = new int[101];
    for(int n : nums) hash[n]++;
    int res = 0;
    for(int i = 1; i <= 100; i++) {
        if(hash[i] >= 2) res += hash[i] * (hash[i] - 1) / 2;
    }
    return res;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)
> 나는 맵과 리스트를 이용하여 풀었으나 다른 사람 코드를 찾아보니 입력 값이 1~100으로 한정되어있기 때문에 배열만을 사용하여 풀었다. 앞으로 문제를 풀 때 입력값을 고려하여 풀어야겠다.

## Reference
* [문제](https://leetcode.com/problems/number-of-good-pairs/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/hashtable/Q1512.java)