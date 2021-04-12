## 문제 설명
현재 숫자보다 작은 수의 갯수

```nums``` 배열이 주어진다. 각 ```nums[i]``` 값보다 작은 숫자가 몇개인지 찾아야 한다. 즉, ```nums[i]```의 값에 따라 ```j != i```이면서 ```nums[j] < nums[i]```인 갯수를 세어야 한다.
정답을 배열로 리턴해라.

## 내가 푼 코드
```
public int[] smallerNumbersThanCurrent(int[] nums) {
    Map<Integer, Integer> map = new TreeMap<>();
    for (int num : nums) {
        if (map.containsKey(num)) {
            map.put(num, map.get(num) + 1);
        } else {
            map.put(num, 1);
        }
    }
    
    int count = 0;
    for (int num : map.keySet()) {
        int newCount = count + map.get(num);
        map.put(num, count);
        count = newCount;
    }
    
    for (int i = 0; i < nums.length; i++) {
        nums[i] = map.get(nums[i]);
    }
    
    return nums;
}
```
* 시간 복잡도: O(nlogn)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/how-many-numbers-are-smaller-than-the-current-number/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/hashtable/Q1365.java)