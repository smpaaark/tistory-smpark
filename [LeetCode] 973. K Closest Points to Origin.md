## 문제 설명
원점으로부터 K와 가장 가까운 점

```points``` 배열이 주어진다. ```points[i] = [x, y]```는 X-Y 좌표이며 ```k```는 정수이다. 원점 ```(0, 0)```으로부터의 가장 근접한 점을 ```k```개 리턴해라.
두 점사이의 거리는 계산 공식은 ```√(x1 - x2)2 + (y1 - y2)2```이다.
정답의 순서는 상관없으며 정답은 항상 존재한다.

## 내가 푼 코드
```
public int[][] kClosest(int[][] points, int k) {
    PriorityQueue<Point> queue = new PriorityQueue<>((a, b) -> {
        return a.distance - b.distance;
    });
    
    for (int[] point : points) {
        int oDistance = (int)(Math.pow(point[0], 2) + Math.pow(point[1], 2));
        queue.offer(new Point(oDistance, point));
    }
    
    List<Point> temp = new ArrayList<>();
    int index = 0;
    while (!queue.isEmpty()) {
        index++;
        Point tempPoint = queue.poll();
        temp.add(tempPoint);
        if (index == k) {
            break;
        }
    }
    
    int[][] result = new int[temp.size()][2];
    for (int i = 0; i < result.length; i++) {
        result[i] = temp.get(i).point;
    }
    
    return result;
}

static class Point {
    private int distance;
    private int[] point;
    
    public Point(int distance, int[] point) {
        super();
        this.distance = distance;
        this.point = point;
    }

    public double getDistance() {
        return distance;
    }

    public void setDistance(int distance) {
        this.distance = distance;
    }

    public int[] getPoint() {
        return point;
    }

    public void setPoint(int[] point) {
        this.point = point;
    }

    @Override
    public String toString() {
        return "Point [distance=" + distance + ", point=" + Arrays.toString(point) + "]";
    }
    
}
```
* 시간 복잡도: O(n)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/k-closest-points-to-origin/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/heap/Q973.java)