## 문제 설명
아이들이 현재 가지고 있는 사탕의 개수를 저장한 배열과 여분의 사탕 개수가 주어진다. 각 아이들에게 여분의 개수를 줬을 때 최대 개수의 사탕을 가지고 있는지 판단한다.

## 내가 푼 코드
```
public List<Boolean> kidsWithCandies(int[] candies, int extraCandies) {
    int maxNum = Integer.MIN_VALUE;
    for (int num : candies) {
        if (num > maxNum) {
            maxNum = num;
        }
    }
    
    List<Boolean> result = new ArrayList<>();
    for (int num : candies) {
        result.add(num + extraCandies >= maxNum ? true : false);
    }
    
    return result;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/array/Q1431.java)