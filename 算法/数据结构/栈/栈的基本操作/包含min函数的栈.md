# 包含min函数的栈
[AcWing 41. 包含min函数的栈](https://www.acwing.com/problem/content/description/90/)

# 解题思路1
再开一个栈存前缀最小值

# Code
```cpp
class MinStack {
public:
    /** initialize your data structure here. */
    stack<int> stk;
    stack<int> stk_min;
    
    MinStack() {
        
    }
    
    void push(int x) {
        stk.push(x);
        if (stk_min.empty()) stk_min.push(x);
        else stk_min.push(min(stk_min.top(), x));
    }
    
    void pop() {
        stk.pop();
        stk_min.pop();
    }
    
    int top() {
        return stk.top();
    }
    
    int getMin() {
        return stk_min.top();
    }
    
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```

# 解题思路2
我们除了维护基本的栈结构之外，还需要维护一个单调栈，来实现返回最小值的操作。
下面介绍如何维护单调栈：

- 当我们向栈中压入一个数时，如果该数 $≤$ 单调栈的栈顶元素，则将该数同时压入单调栈中；否则，不压入，**这是由于栈具有先进后出性质，所以在该数被弹出之前，栈中一直存在一个数比该数小，所以该数一定不会被当做最小数输出**。
- 当我们从栈中弹出一个数时，如果该数等于单调栈的栈顶元素，则同时将单调栈的栈顶元素弹出。
- 单调栈由于其具有单调性，所以它的栈顶元素，就是当前栈中的最小数。


# Code
```cpp
class MinStack {
public:
    /** initialize your data structure here. */
    stack<int> stackValue;
    stack<int> stackMin;
    MinStack() {

    }

    void push(int x) {
        stackValue.push(x);
        if (stackMin.empty() || stackMin.top() >= x)
            stackMin.push(x);
    }

    void pop() {
        if (stackMin.top() == stackValue.top()) stackMin.pop();
        stackValue.pop();
    }

    int top() {
        return stackValue.top();
    }

    int getMin() {
        return stackMin.top();
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```