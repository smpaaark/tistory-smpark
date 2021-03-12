## 문제 설명
증감 문자열

문자열```s```가 주어진다. 아래 알고리즘에 맞게 문자열 순서를 재배치 해야한다.

1. 가장 작은 문자를 고르고 결과에 붙여라.
2. 이전에 붙인 문자보다 큰 문자중에 가장 작은 문자를 골라서 결과에 붙여라.
3. 더 이상 문자를 고를 수 없을 때까지 2번 과정을 반복해라.
4. 가장 큰 문자를 결과에 붙여라.
5. 이전에 붙인 문자보다 작은 문자중에 가장 큰 문자를 골라서 결과에 붙여라.
6. 더 이상 문자를 고를 수 없을 때까지 5번 과정을 반복해라.
7. 문자열```s```의 모든 문자를 고를때까지 1~6번 과정을 반복해라.

각 단계에서 가장 작거나 큰 문자가 두 번 이상 나타나는 경우 한개만 선택하여 붙여라.   
알고리즘을 적용한 문자열을 리턴해라.

## 내가 푼 코드
```
public String sortString(String s) {
    int[] array = new int[26];
    for (char c : s.toCharArray()) {
        array[c - 97]++;
    }
    
    int length = s.length();
    StringBuilder sb = new StringBuilder();
    while (length > 0) {
        for (int i = 0; i < array.length; i++) {
            if (array[i] > 0) {
                sb.append((char) (i + 'a'));
                length--;
                array[i]--;
                if (length == 0) {
                    return sb.toString();
                }
            }
        }
        
        for (int i = array.length - 1; i >= 0; i--) {
            if (array[i] > 0) {
                sb.append((char) (i + 'a'));
                length--;
                array[i]--;
                if (length == 0) {
                    return sb.toString();
                }
            }
        }
    }
    
    return sb.toString();
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/increasing-decreasing-string/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/sort/Q1370.java)