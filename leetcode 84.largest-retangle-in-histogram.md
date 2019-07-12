# leetcode 84 largest-retangle-in-histogram

不过我就知道，一定有大神用他们极简的代码来切题，下面就是一个。

```cpp
 1 public int largestRectangleArea2(int[] height) {
 2         Stack<Integer> stack = new Stack<Integer>();
 3         int i = 0;
 4         int maxArea = 0;
 5         int[] h = new int[height.length + 1];
 6         h = Arrays.copyOf(height, height.length + 1);
 7         while(i < h.length){
 8             if(stack.isEmpty() || h[stack.peek()] <= h[i]){
 9                 stack.push(i++);
10             }else {
11                 int t = stack.pop();
12                 maxArea = Math.max(maxArea, h[t] * (stack.isEmpty() ? i : i - stack.peek() - 1));
13             }
14         }
15         return maxArea;
16     }
```

[![histogram](https://www.geeksforgeeks.org/wp-content/uploads/histogram1.png)](https://www.geeksforgeeks.org/wp-content/uploads/histogram1.png)

## 

We have discussed a [Divide and Conquer based O(nLogn) solution](https://www.geeksforgeeks.org/largest-rectangular-area-in-a-histogram-set-1/) for this problem. In this post, O(n) time solution is discussed. Like the [previous post](https://www.geeksforgeeks.org/largest-rectangular-area-in-a-histogram-set-1/), width of all bars is assumed to be 1 for simplicity. For every bar ‘x’, we calculate the area with ‘x’ as the smallest bar in the rectangle. If we calculate such area for every bar ‘x’ and find the maximum of all areas, our task is done. How to calculate area with ‘x’ as smallest bar? We need to know index of the first smaller (smaller than ‘x’) bar on left of ‘x’ and index of first smaller bar on right of ‘x’. Let us call these indexes as ‘left index’ and ‘right index’ respectively.
We traverse all bars from left to right, maintain a stack of bars. Every bar is pushed to stack once. A bar is popped from stack when a bar of smaller height is seen. When a bar is popped, we calculate the area with the popped bar as smallest bar. How do we get left and right indexes of the popped bar – the current index tells us the ‘right index’ and index of previous item in stack is the ‘left index’. Following is the complete algorithm.

**1)** Create an empty stack.

**2)** Start from first bar, and do following for every bar ‘hist[i]’ where ‘i’ varies from 0 to n-1.
……**a)** If stack is empty or hist[i] is higher than the bar at top of stack, then push ‘i’ to stack.
……**b)** If this bar is smaller than the top of stack, then keep removing the top of stack while top of the stack is greater. Let the removed bar be hist[tp]. Calculate area of rectangle with hist[tp] as smallest bar. For hist[tp], the ‘left index’ is previous (previous to tp) item in stack and ‘right index’ is ‘i’ (current index).

**3)** If the stack is not empty, then one by one remove all bars from stack and do step 2.b for every removed bar.

Following is implementation of the above algorithm.

另外一个细节需要注意的是，弹栈过程中面积的计算。

**h[t] \* (stack.isEmpty() ? i : i - stack.peek() - 1)**

h[t]为当前最小得矩形高度，那么要计算面积则需要找到矩形得左右边界，毫无疑问右边界是i，而左边界由于是栈是递增矩形块得位置，那么栈内得矩形块都是小于h[t]得高度，则右边界是栈顶元素。

![img](https://images0.cnblogs.com/blog/466943/201307/18095649-645e12c5653440f2a9e2ca7b505a3082.png)

那h[t]无疑就是Stack.Peek和t之间那些上流社会的短板啦，而它们的跨越就是i - Stack.Peek - 1。

所以说，这个弹栈的过程也是维持程序不变量的方法啊：**栈内元素一定是要比当前i指向的元素小的。**

----------------------------------------------------------------------------------华丽------------------------------------------------------------------------------------------------------------------------

我只想问算法的作者，他们到底是怎么想出来的，在这么短的时间内。是不是有一些类似的研究或者算法给他们以灵感？

太有画面感了有木有！