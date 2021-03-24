## 문제 설명
규칙을 만족하는 아이템의 갯수

```items```배열이 주어지고, ```items[i] = [type, color, name]```이다. 또한, ```ruleKey```와 ```ruleValue``` 문자열이 주어진다.

```i```번째 아이템은 다음 중 1가지를 만족한다:
* ```ruleKey == "type"```이고 ```ruleValue == typei```이다.
* ```ruleKey == "color"```이고 ```ruleValue == colori```이다.
* ```ruleKey == "name"```이고 ```ruleValue == namei```이다.

규칙을 만족하는 아이템의 갯수를 리턴해라.

## 내가 푼 코드
```
private static final Map<String, Integer> map = new HashMap<>();
	
public Q1773() {
    map.put("type", 0);
    map.put("color", 1);
    map.put("name", 2);
}

public int countMatches(List<List<String>> items, String ruleKey, String ruleValue) {
    int count = 0;
    for (List<String> list : items) {
        if (list.get(map.get(ruleKey)).equals(ruleValue)) {
            count++;
        }
    }
    
    return count;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(1)


## Reference
* [문제](https://leetcode.com/problems/count-items-matching-a-rule/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/string/Q1773.java)