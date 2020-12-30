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
- ### 剑指 Offer 48. 最长不含重复字符的子字符串
请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

示例 1:

```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```
示例 2:

```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```
示例 3:

```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```
题解：
```
//思路：可以使用hashmap解决该问题，依次遍历s然后查询hashmap中是否有重复的，如果有则重新开始计算
//如果没有则增加长度
//注意s为空格的情况，所以index需要设置为-1，保证空格的情况也符合标准
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character,Integer> tmp = new HashMap<>();
        int index=-1;
        int res = 0;
        for(int j = 0;j<s.length();j++){
            if(tmp.containsKey(s.charAt(j))){
                index = Math.max(index,tmp.get(s.charAt(j)));
            }
            tmp.put(s.charAt(j),j);
            res = Math.max(res,j-index);
        }
        return res;
    }
}
```
