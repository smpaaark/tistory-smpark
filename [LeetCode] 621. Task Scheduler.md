## 문제 설명
작업 스케쥴러

char형 배열 ```tasks```이 주어지고, 이것은 CPU가 해야할 작업 리스트이다. 여기서 문자는 각각 다른 작업이다. 작업은 무작위로 수행된다. 각 작업은 한번에 한개씩만 수행된다. 각 시간마다 CPU는 작업이 수행되거나 수행되지 않을 수 있다. 

동일한 두 작업 사이의 냉각 기간을 나타내는 음이 아닌 정수 ```n```이 있다. (배열 안의 같은 문자). 즉, 동일한 두 작업 사이에 최소한 ```n``` 단위의 시간이 있어야 한다.

CPU가 지정된 모든 작업을 완료하는 데 걸리는 최소 단위 수를 리턴해라.

## 내가 푼 코드
```
class MyCircularDeque {
		
    private int[] array;
    private final int qSize;
    
    /** Initialize your data structure here. Set the size of the deque to be k. */
    public MyCircularDeque(int k) {
        this.array = new int[k];
        for (int i = 0; i < k; i++) {
            this.array[i] = -1;
        }
        
        this.qSize = k;
    }
    
    /** Adds an item at the front of Deque. Return true if the operation is successful. */
    public boolean insertFront(int value) {
        if (this.isFull()) {
            return false;
        }
        
        for (int i = this.qSize - 1; i > 0; i--) {
            if (this.array[i - 1] != -1) {
                this.array[i] = this.array[i - 1];
            }
        }
        
        this.array[0] = value;
        
        return true;
    }
    
    /** Adds an item at the rear of Deque. Return true if the operation is successful. */
    public boolean insertLast(int value) {
        if (this.isFull()) {
            return false;
        }
        
        for (int i = this.qSize - 1; i > 0; i--) {
            if (this.array[i - 1] != -1) {
                this.array[i] = value;
                
                return true;
            }
        }
        
        this.array[0] = value;
        return true;
    }
    
    /** Deletes an item from the front of Deque. Return true if the operation is successful. */
    public boolean deleteFront() {
        if (this.isEmpty()) {
            return false;
        }
        
        this.array[0] = -1;
        
        for (int i = 1; i < this.qSize; i++) {
            if (this.array[i] != -1) {
                this.array[i - 1] = this.array[i];
                this.array[i] = -1;
            }
        }
        
        return true;
    }
    
    /** Deletes an item from the rear of Deque. Return true if the operation is successful. */
    public boolean deleteLast() {
        if (this.isEmpty()) {
            return false;
        }
        
        for (int i = this.qSize - 1; i >= 0; i--) {
            if (this.array[i] != -1) {
                this.array[i] = -1;
        
                return true;
            }
        }
        
        return false;
    }
    
    /** Get the front item from the deque. */
    public int getFront() {
        if (this.isEmpty()) {
            return -1;
        }
        
        return this.array[0];
    }
    
    /** Get the last item from the deque. */
    public int getRear() {
        if (this.isEmpty()) {
            return -1;
        }
        
        for (int i = this.qSize - 1; i >= 0; i--) {
            if (this.array[i] != -1) {
                return this.array[i];
            }
        }
        
        return -1;
    }
    
    /** Checks whether the circular deque is empty or not. */
    public boolean isEmpty() {
        if (this.array[0] == -1) {
            return true;
        }
        
        return  false;
    }
    
    /** Checks whether the circular deque is full or not. */
    public boolean isFull() {
        if (this.array[this.qSize - 1] == -1) {
            return false;
        }
        
        return true;
    }
    
}
```

## Reference
* [문제](https://leetcode.com/problems/design-circular-deque/)
* [내가 푼 코드](https://github.com/smpark1020/leetcode-practice/blob/master/src/leetcode/queue/Q641.java)