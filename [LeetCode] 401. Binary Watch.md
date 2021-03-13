## 문제 설명
이진수 시계

이진수 시계는 위쪽에 0~11시를 표현할 수 있는 4개의 불빛을 갖고 있고, 아래쪽에 0~59분을 표현할 수 있는 6개의 불빛을 갖고 있다. 

각 불빛은 0 또는 1을 표현하며 최하위 비트가 오른쪽이다.

## 내가 푼 코드
```
public List<String> readBinaryWatch(int num) {
    List<String> resultList = new ArrayList<>();
    backTracking(0, 0, num, 0, 0, resultList);
    return resultList;
}

private void backTracking(int index, int count, int num, int hour, int minute, List<String> resultList) {	
    if (count == num) {
        if (hour < 12 && minute < 60) {
            addList(hour, minute, resultList);
        }
        return;
    }
    
    for (int i = index; i < binaryWatch.length; i++) {
        if (i <= 3) {
            backTracking(i + 1, count + 1, num, hour + binaryWatch[i], minute, resultList);
        } else {
            backTracking(i + 1, count + 1, num, hour, minute + binaryWatch[i], resultList);
        }
    }
}

private void addList(int hour, int minute, List<String> resultList) {
    StringBuilder sb = new StringBuilder();
    sb.append(hour);
    sb.append(":");
    sb.append(minute < 10 ? "0" + minute : minute);
    resultList.add(sb.toString());
}
```
* 시간 복잡도: O(n²)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/binary-watch/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/backtracking/Q401.java)