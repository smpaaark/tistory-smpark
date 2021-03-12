## 문제 설명
문자열 섞기

문자열 ```s```와 같은 길이의 정수형 배열 ```indices```가 주어진다.   
문자열 ```s```의 i번째 문자가 ```indices[i]```값의 위치로 섞일 예정이다.   
섞인 문자열 결과를 리턴해라.

## 내가 푼 코드
```
public String restoreString(String s, int[] indices) {
    char[] newString = new char[s.length()];
    for (int i = 0; i < s.length(); i++) {
        newString[indices[i]] = s.charAt(i);
    }
    
    return new String(newString);
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## 다른 사람이 푼 코드
```
public String restoreString(String s, int[] indices) {
    char[] ca = s.toCharArray();
    for(int i = 0; i < ca.length; ++i) {
        while(indices[i] != i) {
            swap(ca, i, indices[i]);
            swap(indices, i, indices[i]);
        }
    }
    return new String(ca);
}

void swap(char[] ca, int i, int j) {
    char c = ca[i];
    ca[i] = ca[j];
    ca[j] = c;
}

void swap(int[] a, int i, int j) {
    int v = a[i];
    a[i] = a[j];
    a[j] = v;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)
> 나도 처음에 swap으로 풀라고 시도했으나 이상하게 답이 나오지 않았다. 그래서 char[ ]을 만드는 방법으로 풀었는데 알고보니 문자열을 swap할때 indices배열도 같이 swap을 해줬어야 했다.

## Reference
* [문제](https://leetcode.com/problems/shuffle-string/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/sort/Q1528.java)