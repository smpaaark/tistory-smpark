## 문제 설명
행렬에서 가장 약한 행 K개

```1```(군인)과 ```0```(시민)으로 이루어진 ```m x n```인 이진 행렬 ```mat```가 주어진다. 군인들은 시민의 앞에 위치한다. 각 행에서 모든 ```1```은 모든 ```0```의 왼쪽에 위치할 예정이다.

만약 다음 조건 중 하나가 만족한다면 ```i```행은 ```j```행보다 약하다.
* ```i```행의 군인 수는 ```j```행의 군인 수 보다 적다.
* 군인의 수가 같으면 ```i < j```이다.

약한 행부터 강한 행까지 정렬된 ```k```개의 행을 리턴해라.

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