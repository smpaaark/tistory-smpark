## 문제 설명
XORed 배열 암호화

음이 아닌 정수 ```n```으로 이루어진 숨겨진 정수배열 ```arr```가 있다.

그것은 길이가 ```n - 1```인 다른 배열 ```encoded```로 암호화된다. ```encoded[i] = arr[i] XOR arr[i + 1]```이다. 예를 들어 ```arr = [1, 0, 2, 1]```이면 ```encoded = [1, 2, 3]```이다.

너에게 ```encoded``` 배열이 주어진다. 또한, ```arr```의 첫번째 값인 정수 ```first```도 주어진다. ```(=arr[0])```

원래 배열인 ```arr```를 리턴해라. 정답은 항상 존재하며 유일하다.

## 내가 푼 코드
```
public int[] decode(int[] encoded, int first) {
    int[] arr = new int[encoded.length + 1];
    arr[0] = first;
    
    for (int i = 1; i < arr.length; i++) {
        arr[i] = arr[i - 1] ^ encoded[i - 1];
    }
    
    return arr;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/decode-xored-array/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/bit/Q1720.java)