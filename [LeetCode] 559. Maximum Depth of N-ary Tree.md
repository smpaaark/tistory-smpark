## 문제 설명
N-ary 트리의 최대 깊이

n-ary 트리가 주어지면 그것의 최대 깊이를 찾아라.
최대 깊이는 루트 노드부터 제일 먼 자식 노드까지의 가장 긴 경로의 노드 수이다.
Nary-Tree 각 그룹의 자식 노드는 null로 구분되어 삽입된다.(예제 참고)

## 내가 푼 코드
```
public int[] kWeakestRows(int[][] mat, int k) {
    PriorityQueue<Mat> q = new PriorityQueue<Mat>();

    for (int i = 0; i < mat.length; i++) {
        q.offer(new Mat(getSoldierCount(mat[i]), i));
    }
    
    int[] result = new int[k];
    for (int i = 0; i < k; i++) {
        result[i] = q.poll().index;
    }
    
    return result;
}

private int getSoldierCount(int[] array) {
    int start = 0;
    int end = array.length;
    while (start <= end) {
        int mid = (start + end) / 2;
        if (array[mid] == 1 && mid + 1 == array.length) {
            return mid + 1;
        } else if (array[mid] == 1 && array[mid + 1] == 0) {
            return mid + 1;
        } else if (array[mid] == 1) {
            start = mid + 1;
        } else {
            end = mid - 1;
        }
    }
    
    return 0;
}


static class Mat implements Comparable<Mat>{
    
    private int soldierCount;
    private int index;
    
    public Mat(int soldierCount, int index) {
        super();
        this.soldierCount = soldierCount;
        this.index = index;
    }

    public int getSoldierCount() {
        return soldierCount;
    }
    
    
    public void setSoldierCount(int soldierCount) {
        this.soldierCount = soldierCount;
    }
    
    public int getIndex() {
        return index;
    }
    
    public void setIndex(int index) {
        this.index = index;
    }

    @Override
    public int compareTo(Mat mat) {
        if (this.soldierCount > mat.soldierCount) {
            return 1;
        } else if (this.soldierCount == mat.soldierCount) {
            if (this.index > mat.index) {
                return 1;
            }
        }
        
        return -1;
    }

    @Override
    public String toString() {
        return "Mat [soldierCount=" + soldierCount + ", index=" + index + "]";
    }
```
* 시간 복잡도: O(nlogn)
* 공간 복잡도: O(n)

## Reference
* [문제](https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/binarysearch/Q1337.java)