## 문제 설명
배열이 주어졌을 때 각 index의 값에 누적 합계의 값을 저장하여 반환한다.

## 내가 푼 코드
```
public int[] runningSum(int[] nums) {
    for (int i = 1; i < nums.length; i++) {
        nums[i] += nums[i - 1];
    }

    return nums;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)

## Reference
* [문제](https://leetcode.com/problems/running-sum-of-1d-array/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/array/Q1480.java)