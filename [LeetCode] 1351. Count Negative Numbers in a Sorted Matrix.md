## 문제 설명
정렬된 행렬에서 음수의 갯수를 세어라.

행과 열이 모두 내림차순으로 정렬된 ```m x n```행렬이 주어진다. 음수의 갯수를 리턴해라.

## 내가 푼 코드
```
public int countNegatives(int[][] grid) {
    int result = 0;
    for (int i = 0; i < grid.length; i++) {
        if (grid[i][0] < 0) {
            result += grid[i].length;
        } else {
            result += binarySearch(grid[i]);
        }
    }
    
    return result;
}

private int binarySearch(int[] array) {
    int start = 0;
    int end = array.length - 1;
    while (start <= end) {
        int mid = (start + end) / 2;
        if (array[mid] >= 0) {
            start = mid + 1;
        } else if (mid > 0 && array[mid - 1] < 0){
            end = mid - 1;
        } else {
            return array.length - mid;
        }
    }
    
    return 0;
}
```
* 시간 복잡도: O(nlogn)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/count-negative-numbers-in-a-sorted-matrix/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/binarysearch/Q1351.java)