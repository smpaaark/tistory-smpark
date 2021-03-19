## 문제 설명
직원 중요성

직원의 고유 ID, 중요한 값, 부하 직원들의 ID를 포함하는 직원 정보 자료 구조가 주어진다.
예를 들어, 직원1은 직원2의 리더이고, 직원2는 직원3의 리더이다. 그들은 각각 15, 10, 5라는 중요한 값을 갖고 있다. 직원1은 [1, 15, [2]]라는 자료구조를 갖고 있고, 직원2는 [2, 10, [3]], 직원3은 [3, 5, []]을 갖고 있다. 여기서 직원3은 직원1의 부하 직원이지만 직접적인 관계를 맺지는 않는다.

이제 한 회사의 직원 정보와 직원 ID가 주어진다. 주어진 직원을 포함한 부하 직원의 중요 값의 합을 리턴해라.

## 내가 푼 코드
```
public int getImportance(List<Employee> employees, int id) {
    int sum = 0;
    Queue<Employee> q = new LinkedList<>();
    Map<Integer, Employee> map = new HashMap<>();
    for (Employee employee : employees) {
        map.put(employee.id, employee);
    }
    
    q.offer(map.get(id));
    
    while (!q.isEmpty()) {
        Employee employee = q.poll();
        sum += employee.importance;
        
        for (Integer num :employee.subordinates) {
            q.offer(map.get(num));
        }
    }
    
    return sum;
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n²)

## Reference
* [문제](https://leetcode.com/problems/employee-importance/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/bfs/Q690.java)