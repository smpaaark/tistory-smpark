## 문제 설명
마을의 판사를 찾아라.   
한 마을에는 N명의 사람이 있고, 사람마다 1~N까지의 라벨이 각각 붙어있다. 이들 중에 단 한명만 판사라는 소문이 있다.   
   
이 마을에 판사가 존재하는 조건은 다음과 같다.   
1. 판사는 아무도 믿지 않는다.
2. 판사를 제외한 모든 사람은 판사를 믿는다.
3. 1과 2를 만족하는 사람은 정확하게 1명 있다.

trust[i] = [a, b] 배열이 주어진다. 이것은 a는 b를 믿는다는 의미이다.   
만약 이 마을에 판사가 존재한다면 판사의 라벨 번호를 반환하고, 존재하지 않는다면 -1을 반환해라.

## 내가 푼 코드
```
public int findJudge(int N, int[][] trust) {
    if (N < 2) {
        return N;
    }
    
    List<Integer>[] graph = new ArrayList[N + 1];
    for (int i = 1; i < graph.length; i++) {
        graph[i] = new ArrayList<>();
    }
    
    Map<Integer, Integer> map = new HashMap<>();
    for (int[] array : trust) {
        graph[array[0]].add(array[1]);
        map.put(array[1], map.getOrDefault(array[1], 0) + 1);
    }
    
    for (int i = 1; i < graph.length; i++) {
        if (graph[i].size() == 0 && map.getOrDefault(i, 0) == N - 1) {
            return i;
        }
    }
    
    return -1;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)


## Reference
* [문제](https://leetcode.com/problems/find-the-town-judge/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/graph/Q997.java)