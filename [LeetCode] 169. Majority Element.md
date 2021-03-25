## 문제 설명
다수결 요소

크기가 ```n```인 배열이 주어진다. 다수결 요소를 리턴해라.
다수결 요소는 ```[n / 2]```이상의 횟수가 들어있는 요소이다. 해당 배열에는 항상 다수결 요소가 존재한다.

## 내가 푼 코드
```
public int majorityElement(int[] nums) {
    int compareSize = nums.length / 2;
    int maxNum = 0;
    Map<Integer, Integer> map = new HashMap<>();
    for (int num : nums) {
        map.put(num, map.getOrDefault(num, 0) + 1);
        if (map.get(num) >= compareSize) {
            maxNum = (map.getOrDefault(maxNum, 0) < map.get(num)) ? num : maxNum;
        }
    }
    
    return maxNum;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## 다른 사람 코드
```
public int majorityElement_other(int[] nums) {
        
    return findMajority(nums, 0, nums.length-1);
}

private int findMajority(int[] nums, int low, int high) {
    if (low == high)
        return nums[low];
    
    int mid = low + (high-low)/2;
    
    int left = findMajority(nums, low, mid);
    int right = findMajority(nums, mid+1, high);
    
    if (left == right)
        return left;
    
    int countLeft = getFreq(nums, left, low, mid);
    int countRight = getFreq(nums, right, mid+1, high);
    if (countLeft > countRight)
        return left;
    return right;
}

private int getFreq(int[] nums, int val, int low, int high) {
    int res = 0;
    
    for (int i = low; i <= high; i++) {
        if (nums[i] == val)
            res++;
    }
    return res;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)
> 분할 정복으로 풀면 공간 복잡도 O(1)로 풀이가 가능하다. 코드를 이해하는데 한참 걸렸다. 분할 정복 문제를 많이 풀어봐야될 것 같다.

## Reference
* [문제](https://leetcode.com/problems/majority-element/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/divideconquer/Q169.java)