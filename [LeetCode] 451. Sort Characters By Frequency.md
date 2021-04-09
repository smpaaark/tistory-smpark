## 문제 설명
빈도에 의한 문자 정렬

문자열이 주어진다. 문자가 포함된 갯수 기준 내림차순으로 정렬해라.

## 내가 푼 코드
```
public String frequencySort(String s) {
    PriorityQueue<CharCount> queue = new PriorityQueue<>((a, b) -> {
        return b.count - a.count;
    });
    
    char[] array = s.toCharArray();
    Map<Character, Integer> map = new HashMap<>();
    for (char c : array) {
        if (map.containsKey(c)) {
            map.put(c, map.get(c) + 1);
        } else {
            map.put(c, 1);
        }
    }
    
    for (char c : map.keySet()) {
        queue.offer(new CharCount(c, map.get(c)));
    }
    
    StringBuilder sb = new StringBuilder();
    while (!queue.isEmpty()) {
        CharCount temp = queue.poll();
        for (int i = 0; i < temp.count; i++) {        		
            sb.append(temp.c);
        }
    }
    
    return sb.toString();
}

static class CharCount {
    
    private char c;
    private int count;
    
    public CharCount(char c, int count) {
        super();
        this.c = c;
        this.count = count;
    }
    
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/sort-characters-by-frequency/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/heap/Q451.java)