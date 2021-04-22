## 문제 설명
산 배열의 정상 인덱스

아래와 같은 속성을 가진 배열을 산 배열 ```arr```라고 부른다.
* ```arr.length >= 3```
* ```0 < i < arr.length - 1```인 ```i```가 존재한다.
  * ```arr[0] < arr[1] < ... arr[i-1] < arr[i]```
  * ```arr[i] > arr[i+1] > ... > arr[arr.length - 1]```

정수형 배열 ```arr```가 주어지고 항상 산 배열이다. ```arr[0] < arr[1] < ... arr[i - 1] < arr[i] > arr[i + 1] > ... > arr[arr.length - 1]```를 만족하는 ```i```를 리턴해라.

## 내가 푼 코드
```
public int peakIndexInMountainArray(int[] arr) {
    int start = 0;
    int end = arr.length - 1;
    
    while (true) {
        int mid = (start + end) / 2;
        
        if (arr[mid - 1] < arr[mid] && arr[mid] < arr[mid + 1]) {
            start = mid;
        } else if (arr[mid - 1] > arr[mid] && arr[mid] > arr[mid + 1]){
            end = mid;
        } else {
            return mid;
        }
        
    }
}
```
* 시간 복잡도: O(logn)
* 공간 복잡도: O(1)

## Reference
* [문제](https://leetcode.com/problems/peak-index-in-a-mountain-array/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/binarysearch/Q852.java)