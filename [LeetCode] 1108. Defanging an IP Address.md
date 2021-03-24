## 문제 설명
IP 주소 변경

유효한 (IPv4)IP ```address```가 주어지고, 변형된 버전의 IP 주소를 리턴해라.
변형된 IP 주소는 모든 ```"."```이 ```"[.]"```으로 대체된다.

## 내가 푼 코드
```
public String defangIPaddr(String address) {
    return address.replaceAll("\\.", "[.]");
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)
> 시간/공간 복잡도가 맞는지 모르겠다. String 관련 메서드들의 시간/공간 복잡도를 좀 더 공부해야겠다.

## Reference
* [문제](https://leetcode.com/problems/defanging-an-ip-address/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/string/Q1108.java)