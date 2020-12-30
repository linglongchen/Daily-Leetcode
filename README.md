# Daily-Leetcode


我是陈汤姆，一个正在成长的技术菜鸡，目前除了不缺女朋友，什么都缺，想要进入大厂拿高薪的普通本科生，虽然很菜，但是还是在进步。这里记录自己刷题的日常，以便以后自己继续查阅。


希望能跟一起热爱技术的人一起进入，一起努力，升职加薪！

- ###  Offer 09. 用两个栈实现队列
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )
 

示例 1：
```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]

输出：[null,null,3,-1]
```

示例 2：
```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]

输出：[null,-1,null,null,5,2]
```
提示：
```
<= values <= 10000
最多会对 appendTail、deleteHead 进行 10000 次调用
```
题解：
```
//栈的特性为：先进后出，队列特性为：先进先出
//使用两个栈，第一个栈先进后出的结果放入第二个栈，这样第一个栈后出的在第二个栈中就先出
//这样就实现了基本的队列效果，先进先出
class CQueue {
    Deque<Integer> stack1;
    Deque<Integer> stack2;

    public CQueue() {
        stack1 = new LinkedList<Integer>();
        stack2 = new LinkedList<Integer>();
    }
    
    public void appendTail(int value) {
        stack1.push(value);
    }
    
    public int deleteHead() {
        //判断第二个栈的情况,如果第二个栈为空则遍历第一个栈将第一个栈的元素放入第二个栈
        if(!stack2.isEmpty()){
            return stack2.pop();
        }
        if(stack1.isEmpty()){
            return -1;
        }else{
            while(!stack1.isEmpty()){
                stack2.push(stack1.pop());
            }
        }
        return stack2.pop();
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */

```
- 
