## 문제 설명
하위배열의 최대값

정수형 배열 ```nums```가 주어진다. 가장 큰 합을 갖는 (최소 숫자 한개 이상을 포함하는)연속 하위 배열을 찾고, 그 하위배열의 모든 요소의 합을 리턴해라.

## 내가 푼 코드
```
public int maxSubArray(int[] nums) {
    return recursion(nums, 0, nums.length - 1);
}

private int recursion(int[] nums, int start, int end) {
    if (start == end) {
        return nums[start];
    }
    
    if (start > end) {
        return Integer.MIN_VALUE;
    }
    
    int mid = (start + end) / 2;
    
    int leftMax = recursion(nums, start, mid - 1);
    int rightMax = recursion(nums, mid + 1, end);
    
    int tempLeftMax = 0;
    int sum = 0;
    for (int i = mid - 1; i >= start; i--) {
        sum += nums[i];
        if (sum > tempLeftMax) {
            tempLeftMax = sum;
        }
    }
    
    int tempRightMax = 0;
    sum = 0;
    for (int i = mid + 1; i <= end; i++) {
        sum += nums[i];
        if (sum > tempRightMax) {
            tempRightMax = sum;
        }
    }
    
    int midSumMax = tempLeftMax + tempRightMax + nums[mid];
    
    return Math.max(Math.max(leftMax, rightMax), midSumMax);
}
```
* 시간 복잡도: O(n²)
* 공간 복잡도: O(n)
> 분할 정복으로 풀려고 했는데 결국 스스로 풀지 못했다. 그래서 다른 사람 코드를 참고했는데 이해하는데 한참 걸렸다. 이 문제를 풀고 나서야 어느정도 분할 정복과 재귀에 감이 좀 잡힌 것 같다.

## Reference
* [문제](https://leetcode.com/problems/maximum-subarray/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/divideconquer/Q53.java)