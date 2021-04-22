## 문제 설명
두 배열의 교점

정수형 배열 ```nums1```과 ```nums2```가 주어진다. 두 배열의 교점을 리턴해라. 결과의 각 원소는 중복이 없으며, 순서도 상관없다.

## 내가 푼 코드
```
public int[] intersection(int[] nums1, int[] nums2) {
    Set<Integer> set = new HashSet<>();
    
    int[] setArray = nums1;
    int[] searchArray = nums2;
    if (nums1.length > nums2.length) {
        setArray = nums2;
        searchArray = nums1;
    } 
    
    for (int num : setArray) {
        if (!set.contains(num)) {
            set.add(num);
        }
    }
    
    Set<Integer> resultSet = new HashSet<>();
    for (int num : searchArray) {
        if (set.contains(num) && !resultSet.contains(num)) {
            resultSet.add(num);
        }
    }
    
    int[] result = new int[resultSet.size()];
    int index = 0;
    for (int num : resultSet) {
        result[index++] = num;
    }
    
    return result;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/intersection-of-two-arrays/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/binarysearch/Q349.java)