# 155 Min Stack

```java/*
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.
Example:
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
*/

// 双栈。stackData存取所有数据，stackMin存取每一步的最小值。

class MinStack {

    private Stack<Integer> stackData;
    private Stack<Integer> stackMin;

    /** initialize your data structure here. */
    public MinStack() {
        stackData = new Stack<Integer>();
        stackMin = new Stack<Integer>();
    }

    public void push(int x) {
        if (stackMin.isEmpty()) {
            stackMin.push(x);
        } else if (x <= stackMin.peek()) {
            stackMin.push(x);
        }
        stackData.push(x);
    }

    public void pop() {
        int value = stackData.pop();
        if (value == stackMin.peek()) {
            stackMin.pop();
        }
    }

    public int top() {
        return stackData.peek();
    }

    public int getMin() {
        return stackMin.peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */

```
