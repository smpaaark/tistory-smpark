## 문제 설명
원형 디큐 설계

원형 디큐를 설계해라.
원형 디큐는 다음 오퍼레이션을 지원해야한다.:
* ```MyCircularDeque(k)```: 생성자, 크기가 k인 디큐를 생성한다.
* ```insertFront()```: 디큐의 맨 앞에 아이템을 추가한다. 오퍼레이션이 성공하면 true를 리턴한다.
* ```insertLast()```: 디큐의 맨 뒤에 아이템을 추가한다. 오퍼레이션이 성공하면 true를 리턴한다.
* ```deleteFront()```: 디큐의 맨 앞 아이템을 삭제한다. 오퍼레이션이 성공하면 true를 리턴한다.
* ```deleteLast()```: 디큐의 맨 뒤 아이템을 삭제한다. 오퍼레이션이 성공하면 true를 리턴한다.
* ```getFront()```: 디큐의 맨 앞 아이템을 꺼낸다. 디큐가 비어있으면 -1을 리턴한다.
* ```getRear()```: 디큐의 맨 뒤 아이템을 꺼낸다. 디큐가 비어있으면 -1을 리턴한다.
* ```isEmpty()```: 디큐가 비어있는지 확인한다.
* ```isFull()```: 디큐가 꽉 차있는지 확인한다.

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