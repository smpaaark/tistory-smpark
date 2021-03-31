## 문제 설명
배열 섞기

```[x1,x2,...,xn,y1,y2,...,yn]``` 형태로 ```2n```개의 요소로 구성된 ```nums```배열이 주어진다.   
```[x1,y1,x2,y2,...,xn,yn]``` 형태로 리턴해라.

## 내가 푼 코드
```
public int[] shuffle(int[] nums, int n) {
    int[] resultArray = new int[nums.length];
    int xIndex = 0;
    int yIndex = nums.length / 2;
    for (int i = 0; i < resultArray.length; i++) {
        if (i % 2 == 0) {
            resultArray[i] = nums[xIndex++];
        } else {
            resultArray[i] = nums[yIndex++];
        }
    }
    
    return resultArray;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## 다른 사람 코드
```
public int[] shuffle_other(int[] nums, int n) {
    int[] shuffled = new int[nums.length];
    for(int i = 0; i < n; i++){
        shuffled[i * 2] = nums[i];
        shuffled[i * 2 + 1] = nums[i + n];
    }
    
    return shuffled;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)
> 시간/공간 복잡도는 같지만 아래코드는 반복문을 n/2 만큼만 돌게 풀었다.

## Reference
* [문제](https://leetcode.com/problems/shuffle-the-array/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/array/Q1470.java)