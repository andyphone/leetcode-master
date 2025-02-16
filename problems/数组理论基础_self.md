<p align="center">
  <a href="https://mp.weixin.qq.com/s/RsdcQ9umo09R6cfnwXZlrQ"><img src="https://img.shields.io/badge/PDF下载-代码随想录-blueviolet" alt=""></a>
  <a href="https://mp.weixin.qq.com/s/b66DFkOp8OOxdZC_xLZxfw"><img src="https://img.shields.io/badge/刷题-微信群-green" alt=""></a>
  <a href="https://space.bilibili.com/525438321"><img src="https://img.shields.io/badge/B站-代码随想录-orange" alt=""></a>
  <a href="https://mp.weixin.qq.com/s/QVF6upVMSbgvZy8lHZS3CQ"><img src="https://img.shields.io/badge/知识星球-代码随想录-blue" alt=""></a>
</p>
<p align="center"><strong>欢迎大家<a href="https://mp.weixin.qq.com/s/tqCxrMEU-ajQumL1i8im9A">参与本项目</a>，贡献其他语言版本的代码，拥抱开源，让更多学习算法的小伙伴们收益！</strong></p>



## 数组理论基础

数组是非常基础的数据结构，在面试中，考察数组的题目一般在思维上都不难，主要是考察对代码的掌控能力

也就是说，想法很简单，但实现起来 可能就不是那么回事了。

首先要知道数组在内存中的存储方式，这样才能真正理解数组相关的面试题

**数组是存放在连续内存空间上的相同类型数据的集合。**

数组可以方便的通过下标索引的方式获取到下标下对应的数据。

举一个字符数组的例子，如图所示：

![算法通关数组](https://code-thinking.cdn.bcebos.com/pics/%E7%AE%97%E6%B3%95%E9%80%9A%E5%85%B3%E6%95%B0%E7%BB%84.png)



需要两点注意的是

* **数组下标都是从0开始的。**
* **数组内存空间的地址是连续的**

正是**因为数组的在内存空间的地址是连续的，所以我们在删除或者增添元素的时候，就难免要移动其他元素的地址。**

例如删除下标为3的元素，需要对下标为3的元素后面的所有元素都要做移动操作，如图所示：

![算法通关数组1](https://code-thinking.cdn.bcebos.com/pics/%E7%AE%97%E6%B3%95%E9%80%9A%E5%85%B3%E6%95%B0%E7%BB%841.png)


而且大家如果使用C++的话，要注意vector 和 array的区别，vector的底层实现是array，严格来讲vector是容器，不是数组。

**数组的元素是不能删的，只能覆盖。**

那么二维数组直接上图，大家应该就知道怎么回事了

![算法通关数组2](https://code-thinking.cdn.bcebos.com/pics/%E7%AE%97%E6%B3%95%E9%80%9A%E5%85%B3%E6%95%B0%E7%BB%842.png)


**那么二维数组在内存的空间地址是连续的么？**

不同编程语言的内存管理是不一样的，以C++为例，在C++中二维数组是连续分布的。

我们来做一个实验，C++测试代码如下：

```C++
void test_arr() {
    int array[2][3] = {
		{0, 1, 2},
		{3, 4, 5}
    };
    cout << &array[0][0] << " " << &array[0][1] << " " << &array[0][2] << endl;
    cout << &array[1][0] << " " << &array[1][1] << " " << &array[1][2] << endl;
}

int main() {
    test_arr();
}

```

测试地址为

```
0x7ffee4065820 0x7ffee4065824 0x7ffee4065828
0x7ffee406582c 0x7ffee4065830 0x7ffee4065834
```

注意地址为16进制，可以看出二维数组地址是连续一条线的。

一些录友可能看不懂内存地址，我就简单介绍一下， 0x7ffee4065820 与 0x7ffee4065824 差了一个4，就是4个字节，因为这是一个int型的数组，所以两个相信数组元素地址差4个字节。

0x7ffee4065828 与 0x7ffee406582c 也是差了4个字节，在16进制里8 + 4 = c，c就是12。

如图：

![数组内存](https://img-blog.csdnimg.cn/20210310150641186.png)

**所以可以看出在C++中二维数组在地址空间上是连续的**。

像Java是没有指针的，同时也不对程序员暴漏其元素的地址，寻址操作完全交给虚拟机。

所以看不到每个元素的地址情况，这里我以Java为例，也做一个实验。

```Java
public static void test_arr() {
    int[][] arr = {{1, 2, 3}, {3, 4, 5}, {6, 7, 8}, {9,9,9}};
    System.out.println(arr[0]);
    System.out.println(arr[1]);
    System.out.println(arr[2]);
    System.out.println(arr[3]);
}
```
输出的地址为：

```
[I@7852e922
[I@4e25154f
[I@70dea4e
[I@5c647e05
```

这里的数值也是16进制，这不是真正的地址，而是经过处理过后的数值了，我们也可以看出，二维数组的每一行头结点的地址是没有规则的，更谈不上连续。

所以Java的二维数组可能是如下排列的方式：

![算法通关数组3](https://img-blog.csdnimg.cn/20201214111631844.png)

我们在[数组过于简单，但你该了解这些！](https://mp.weixin.qq.com/s/c2KABb-Qgg66HrGf8z-8Og)分别作了实验

## 数组的经典题目

在面试中，数组是必考的基础数据结构。

其实数据的题目在思想上一般比较简单的，但是如果想高效，并不容易。

我们之前一共讲解了四道经典数组题目，每一道题目都代表一个类型，一种思想。

### 二分法

[704.二分查找](https://mp.weixin.qq.com/s/4X-8VRgnYRGd5LYGZ33m4w)

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length; // 定义target在左闭右开的区间里，即：[left, right)  
        while (left < right) { // 因为left == right的时候，在[left, right)是无效的空间，所以使用 <
            int middle = left + ((right - left) / 2);// 防止溢出 等同于(left + right)/2
            if (nums[middle] > target) {
                right = middle ; // target 在左区间，在[left, middle)中
            } else if (nums[middle] < target) {
                left = middle + 1; // target 在右区间，在[middle + 1, right)中
            } else { // nums[middle] == target
                return middle; // 数组中找到目标值，直接返回下标
            }
        }
        // 未找到目标值
        return -1;
    }
}
//最普遍:左闭右闭
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1; // 定义target在左闭右闭的区间里，[left, right]
        while (left <= right) { // 当left==right，区间[left, right]依然有效，所以用 <=
            int middle = left + ((right - left) >> 1); // 防止溢出 等同于(left + right)/2
            if (nums[middle] > target) {
                right = middle - 1; // target 在左区间，所以[left, middle - 1]
            } else if (nums[middle] < target) {
                left = middle + 1; // target 在右区间，所以[middle + 1, right]
            } else { // nums[middle] == target
                return middle; // 数组中找到目标值，直接返回下标
            }
        }
        // 未找到目标值
        return -1;
    }
}
```


在这道题目中我们讲到了**循环不变量原则**，只有在循环中坚持对区间的定义，才能清楚的把握循环中的各种细节。

**二分法是算法面试中的常考题，建议通过这道题目，锻炼自己手撕二分的能力**。

相关题目：

* 35.搜索插入位置


```java

class Solution {
    public int searchInsert(int[] nums, int target) {
        int left=0,right=nums.length-1;
        int ans = binarySearch1(nums,target);

        // int k = (nums[ans] > target)? 0:1;
        return ans ;
    }
    public int binarySearch1(int[] nums, int target)    {
        int left = 0, right = nums.length - 1, ans = nums.length;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (nums[mid] >= target) {
                right = mid - 1;
                ans = mid;
            } else {
                left = mid + 1;
            }
        }
        return ans;
    }
}

```
* 34.在排序数组中查找元素的第一个和最后一个位置
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int leftIdx = binarySearch1(nums, target);
        int rightIdx = binarySearch2(nums, target) - 1;
        if (leftIdx <= rightIdx && rightIdx < nums.length && nums[leftIdx] == target && nums[rightIdx] == target) {
            return new int[]{leftIdx, rightIdx};
        }
        return new int[]{-1, -1};
    }

    public int binarySearch1(int[] nums, int target)    {
        int left = 0, right = nums.length - 1, ans = nums.length;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (nums[mid] >= target) {
                right = mid - 1;
                ans = mid;
            } else {
                left = mid + 1;
            }
        }
        return ans;
    }
    public int binarySearch2(int[] nums, int target)    {
        int left = 0, right = nums.length - 1, ans = nums.length;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (nums[mid] > target) {
                right = mid - 1;
                ans = mid;
            } else {
                left = mid + 1;
            }
        }
        return ans;
    }
}
```


* 69.x 的平方根
```java

class Solution {
    public int mySqrt(int x) {
        int left = 0, right = x, ans = -1;
        while (left <= right) {
            int mid = left + ((right - left) >> 1);//(right+left)/2;
            if ((long) mid * mid <= x) {
                left = mid + 1;
                ans = mid;
            } else {
                right = mid - 1;
            }
        }
        return ans;
    }
}
```  
* 367.有效的完全平方数
```java

class Solution {
    public boolean isPerfectSquare(int num) {
        int ans = mySqrt(num);
        return ans * ans == num;
    }

    public int mySqrt(int x) {
        int left = 0, right = x, ans = -1;
        while (left <= right) {
            int mid = left + ((right - left) >> 1);//(right+left)/2;
            if ((long) mid * mid <= x) {
                left = mid + 1;
                ans = mid;
            } else {
                right = mid - 1;
            }
        }
        return ans;
    }
}
```

### 双指针法

[27. 移除元素](https://mp.weixin.qq.com/s/RMkulE4NIb6XsSX83ra-Ww)

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int slowIndex = 0;
        for (int fastIndex = 0; fastIndex < nums.length; fastIndex++) {
            if (val != nums[fastIndex]) {
                nums[slowIndex++] = nums[fastIndex]; //移位之后累加作用: 1.计数,2.预订了下一次的移位坐标
            }
        }
        return slowIndex;
    }
}
```

双指针法（快慢指针法）：**通过一个快指针和慢指针在一个for循环下完成两个for循环的工作。**

暴力解法时间复杂度：O(n^2)
双指针时间复杂度：O(n)

这道题目迷惑了不少同学，纠结于数组中的元素为什么不能删除，主要是因为一下两点：

* 数组在内存中是连续的地址空间，不能释放单一元素，如果要释放，就是全释放（程序运行结束，回收内存栈空间）。
* C++中vector和array的区别一定要弄清楚，vector的底层实现是array，所以vector展现出友好的一些都是因为经过包装了。

双指针法（快慢指针法）在数组和链表的操作中是非常常见的，很多考察数组和链表操作的面试题，都使用双指针法。

相关题目：

* 26.删除排序数组中的重复项

```java
//offical
class Solution {
    public int removeDuplicates(int[] nums) {
        int n = nums.length;
        if (n == 0) {
            return 0;
        }
        int fast = 1, slow = 1;
        while (fast < n) {
            if (nums[fast] != nums[fast-1]) {
                nums[slow] = nums[fast]; //每次比较非重复元素时,都会原地复制一遍
                ++slow;
            }
            ++fast;
        }
        return slow;
    }
}
//网友1 offical思路的for版
class Solution {
    public int removeDuplicates(int[] nums) {
        int slow = 0;
        for (int fast = 0; fast < nums.length; fast++ ) {
            if (fast == 0 || nums[fast] != nums[fast-1]) {
                nums[slow++] = nums[fast];//每次比较非重复元素时,都会原地复制一遍
            }
        }
        return slow;
    }
}


//self
class Solution {
    public int removeDuplicates(int[] nums) {
        int slowIndex = 0;
        for (int fastIndex = 1; fastIndex < nums.length; fastIndex++) {
            if (nums[slowIndex] != nums[fastIndex]) {
                nums[++slowIndex] = nums[fastIndex];//每次比较非重复元素时,都会原地复制一遍
            }
        }
        return slowIndex + 1;
    }
}
//self2  根据网友2的思路的优化
class Solution {
    public int removeDuplicates(int[] nums) {
        int slowIndex = 0;
        for (int fastIndex = 1; fastIndex < nums.length; fastIndex++) {
            if (nums[slowIndex] != nums[fastIndex]) {
                if (fastIndex - slowIndex > 1) {//这个判断,避免了每次比较非重复元素时,都会原地复制一遍
                    nums[slowIndex+1] = nums[fastIndex];
                }
                slowIndex++;
            }
        }
        return slowIndex + 1;
    }
}


//网友2 类似self的while版
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int slow = 0;
        int fast = 1;
        while (fast < nums.length) {
            if (nums[slow] != nums[fast]) {
                if (fast - slow > 1) {              //这个判断,避免了每次比较非重复元素时,都会原地复制一遍
                    nums[slow + 1] = nums[fast];
                }
                slow++;
            }
            fast++;
        }
        return slow + 1;
    }
}

```
* 283.移动零

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int slowIndex = 0;
        for (int fastIndex = 0; fastIndex < nums.length; fastIndex++) {
            if (0 != nums[fastIndex]) {
                int tmp = nums[slowIndex];
                nums[slowIndex++] = nums[fastIndex];
                nums[fastIndex] =tmp;
            }
        }
    }
}
```
* 844.比较含退格的字符串

```java
//self  其实用堆栈更直观?
class Solution {
    public boolean backspaceCompare(String s, String t) {
        char[] chars1 = s.toCharArray();
        char[] chars2 = t.toCharArray();
        char[] lastchars1 = getFilterArray(chars1);
        char[] lastchars2 = getFilterArray(chars2);
        if (lastchars1.length != lastchars2.length) {
            return false;
        }
        for (int i = 0; i < lastchars1.length; i++) {
            if (lastchars1[i] != lastchars2[i]) {
                return false;
            }
        }
        return true;
    }

    public char[] getFilterArray(char[] chars) {
        int slowIndex = 0;
        char val = '#';
        for (int fastIndex = 0; fastIndex < chars.length; fastIndex++) {
            if (val != chars[fastIndex]) {
                chars[slowIndex++] = chars[fastIndex]; //移位之后累加作用: 1.计数,2.预订了下一次的移位坐标
            } else {
                slowIndex = slowIndex == 0 ? 0 : slowIndex - 1;
            }
        }
//            return slowIndex;
        char[] ansArray = new char[slowIndex];
        for (int i = 0; i < slowIndex; i++) {   //        if (slowIndex >= 0) System.arraycopy(chars, 0, ansArray, 0, slowIndex);
            ansArray[i] = chars[i];
        }
        return ansArray;
    }
}
//网友 堆栈
class Solution {
    public boolean backspaceCompare(String S, String T) {
        return helper(S).equals(helper(T));
    }

    private String helper(String str) {
        Stack<Character> stack = new Stack<>();
        for (int i = 0; i < str.length(); i++) {
            Character c = str.charAt(i);

            // 如果当前考察字符不是退格符#，则将其入栈
            if (c != '#') {
                stack.push(c);
            } else if (!stack.isEmpty()) {
                // 如果当前考察字符是退格符#且栈不为空
                // 则栈顶元素出栈
                stack.pop();
            }
        }
        return stack.toString();
    }
}
//官方 双指针逆序
class Solution {
    public boolean backspaceCompare(String S, String T) {
        int i = S.length() - 1, j = T.length() - 1;
        int skipS = 0, skipT = 0;

        while (i >= 0 || j >= 0) {
            while (i >= 0) {
                if (S.charAt(i) == '#') {
                    skipS++;
                    i--;
                } else if (skipS > 0) {
                    skipS--;
                    i--;
                } else {
                    break;
                }
            }
            while (j >= 0) {
                if (T.charAt(j) == '#') {
                    skipT++;
                    j--;
                } else if (skipT > 0) {
                    skipT--;
                    j--;
                } else {
                    break;
                }
            }
            if (i >= 0 && j >= 0) {
                if (S.charAt(i) != T.charAt(j)) {
                    return false;
                }
            } else {
                if (i >= 0 || j >= 0) {
                    return false;
                }
            }
            i--;
            j--;
        }
        return true;
    }
}
 
```
* 977.有序数组的平方

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int n = nums.length;
        int[] ans = new int[n];
        for (int i = 0, j = n - 1, pos = n - 1; i <= j;) {
            if (nums[i] * nums[i] > nums[j] * nums[j]) {
                ans[pos] = nums[i] * nums[i];
                ++i;
            } else {
                ans[pos] = nums[j] * nums[j];
                --j;
            }
            --pos;
        }
        return ans;
    }
}
//数组其实是有序的， 只不过负数平方之后可能成为最大数了。
//
//那么数组平方的最大值就在数组的两端，不是最左边就是最右边，不可能是中间。
//
//此时可以考虑双指针法了，i指向起始位置，j指向终止位置。

```

### 滑动窗口

[209.长度最小的子数组](https://mp.weixin.qq.com/s/ewCRwVw0h0v4uJacYO7htQ)

```java
//暴力法 -- 时间复杂度：O(n^2)  空间复杂度：O(1)
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        int n = nums.length;
        if (n == 0) {
            return 0;
        }
        int ans = Integer.MAX_VALUE;
        for (int i = 0; i < n; i++) {
            int sum = 0;
            for (int j = i; j < n; j++) {
                sum += nums[j];
                if (sum >= s) {
                    ans = Math.min(ans, j - i + 1);//j - i + 1:子序列的长度
                    break;
                }
            }
        }
        return ans == Integer.MAX_VALUE ? 0 : ans;
    }
}

//滑动窗口 -- 时间复杂度：O(n) 空间复杂度：O(1)  ---窗口就是 满足其和 ≥ s 的长度最小的 连续 子数组。
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        int n = nums.length;
        int sum = 0; // 滑动窗口数值之和
        int i = 0; // 滑动窗口起始位置
        if (n == 0) {
            return 0;
        }
        int ans = Integer.MAX_VALUE;
        for (int j = 0; j < n; j++) {
            sum += nums[j];
            while (sum >= s) {
                ans = Math.min(ans, j - i + 1);
                sum -= nums[i++]; // 滑窗 之 精髓: 可以像动画演示中的一样, 起始指针移动了,同时从sum中剔除了移动前的该下标的值.
            }
        }
        return ans == Integer.MAX_VALUE ? 0 : ans;
    }
}


//题外话的解法: [前缀和] + [二分查找] 
// 时间复杂度：O(nlogn)， 
// 其中 n 是数组的长度。需要遍历每个下标作为子数组的开始下标，遍历的时间复杂度是 O(n)，
// 对于每个开始下标，需要通过二分查找得到长度最小的子数组，二分查找的时间复杂度是 O(logn)，
// 因此总时间复杂度是 O(nlogn)。

// 空间复杂度：O(n)，其中 n 是数组的长度。额外创建数组 sums 存储前缀和。
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        int n = nums.length;
        if (n == 0) {
            return 0;
        }
        int ans = Integer.MAX_VALUE;
        int[] sums = new int[n + 1];// 生成一个由
        // 为了方便计算，令 size = n + 1 
        // sums[0] = 0 意味着前 0 个元素的前缀和为 0
        // sums[1] = A[0] 前 1 个元素的前缀和为 A[0]
        // 以此类推
        for (int i = 1; i <= n; i++) {
            sums[i] = sums[i - 1] + nums[i - 1];
        }
        for (int i = 1; i <= n; i++) {
            int target = s + sums[i - 1];
            int bound = Arrays.binarySearch(sums, target);//二分查找
            if (bound < 0) {  //<0 是 Arrays.binarySearch对找不到匹配项时的应对机制.
                bound = -bound - 1; // -[-(low + 1)]-1 = low  ,即大于等于某个数[target]的第一个位置.
            }
            /*
             * 通过二分查找得到大于或等于 i 的最小下标 bound，使得sums[bound]−sums[i−1]≥s，并更新子数组的最小长度（此时子数组的长度是 bound−(i−1)。
             */
            if (bound <= n) {
                ans = Math.min(ans, bound - (i - 1));
            }
        }
        return ans == Integer.MAX_VALUE ? 0 : ans;
    }
    //Arrays.binarySearch 的源码如下
    public static int binarySearch(int[] a, int key) {
        return binarySearch0(a, 0, a.length, key);
    }
    private static int binarySearch0(int[] a, int fromIndex, int toIndex,
                                     int key) {
        int low = fromIndex;
        int high = toIndex - 1;

        while (low <= high) {
            int mid = (low + high) >>> 1;
            int midVal = a[mid];

            if (midVal < key)
                low = mid + 1;
            else if (midVal > key)
                high = mid - 1;
            else
                return mid; // key found
        }
        return -(low + 1);  // key not found.  ***功能: 实现查找大于等于某个数[target]的第一个位置.
        // 如果数组中不存在该元素，则会返回 -(插入点 + 1);这里的插入点具体指的是：如果该数组中存在该元素，那个元素在该数组中的下标
    }
}//因为这道题保证了数组中每个元素都为正，所以前缀和一定是递增的，这一点保证了二分的正确性。如果题目没有说明数组中每个元素都为正，这里就不能使用二分来查找这个位置了。



```

本题介绍了数组操作中的另一个重要思想：滑动窗口。

暴力解法时间复杂度：O(n^2)
滑动窗口时间复杂度：O(n)

本题中，主要要理解滑动窗口如何移动 窗口起始位置，达到动态更新窗口大小的，从而得出长度最小的符合条件的长度。

**滑动窗口的精妙之处在于根据当前子序列和大小的情况，不断调节子序列的起始位置。从而将O(n^2)的暴力解法降为O(n)。**

如果没有接触过这一类的方法，很难想到类似的解题思路，滑动窗口方法还是很巧妙的。

相关题目：

* 904.水果成篮

```java
//问题等价于，找到最长的子序列(连续)，最多含有两种“类型”（tree[i] 的值）。
class Solution {
    public int totalFruit(int[] tree) {
        int ans = 0, i = 0;
        Counter count = new Counter();
        for (int j = 0; j < tree.length; ++j) {
            count.add(tree[j], 1);
            while (count.size() >= 3) {  //暨 count.size() > 2
                count.add(tree[i], -1);
                if (count.get(tree[i]) == 0)
                    count.remove(tree[i]);
                i++;
            }

            ans = Math.max(ans, j - i + 1);
        }

        return ans;
    }
}
//可加可减可获取的计数器
class Counter extends HashMap<Integer, Integer> {
    public int get(int k) {
        return containsKey(k) ? super.get(k) : 0;
    }

    public void add(int k, int v) {
        put(k, get(k) + v);
    }
}
```
* 76.最小覆盖子串

```java
class Solution {
    public String minWindow(String s, String t) {
        int i = 0; // 滑动窗口起始位置
        int ans = Integer.MAX_VALUE;
        String returnValue = "";
        Counter sCounter = new Counter();
        Counter tCounter = new Counter();
        char[] samples = t.toCharArray();
        for (char sample : samples) {
            tCounter.count(sample);
        }
        for (int j = 0; j < s.length(); j++) {
            char currentChar = s.charAt(j);
            if (tCounter.containsKey(currentChar)) {  //这个if可有可无,因为下面delete()方法调用的remove并不会因此报错
                sCounter.count(currentChar);
            }
            while (isAllContain(sCounter, tCounter)) {
                if (j - i + 1 < ans) {
                    ans = j - i + 1;//子串长度
                    returnValue = s.substring(i, i + ans);//i + ans 即为 j+1
                    //substring(beginIndex,endIndex)
                    //从beginIndex开始取，到endIndex结束，从0开始数，其中不包括endIndex位置的字符
                    //取得的字符串长度为：
                    // ans = endIndex - beginIndex ,由此可知 endIndex = beginIndex + ans  ;
                }
                sCounter.delete(s.charAt(i++));
            }
        }
        return ans == Integer.MAX_VALUE ? "" : returnValue;
    }
    public boolean isAllContain(Counter sCounter, Counter tCounter) {
        for (Character sample : tCounter.keySet()) {
            Integer count = sCounter.get(sample);
            if (count == null || count < tCounter.get(sample)) {
                return false;
            }
        }
        return sCounter.keySet().size() >= tCounter.keySet().size();
    }
}
class Counter extends HashMap<Character, Integer> {
    public void count(char c) {
        Integer quantity = get(c);
        put(c, quantity == null ? 1 : quantity + 1);
    }

    public void delete(char c) {
        Integer quantity = get(c);
        if (quantity == null) {
            remove(c);
        } else {
            put(c, quantity - 1);
        }
    }
}

    //官方方法之网友优化版
    public String minWindow2(String s, String t) {
        int[] help = new int[128];//char的标准取值范围只有0-127 , 由此可新建一个数组作为统计表
        for (char ch : t.toCharArray()) {
            help[ch]++;   //利用char对应的int值,将t的每一个char出现次数统计到表help
        }
        int left = 0, right = 0, minSize = Integer.MAX_VALUE;
        String res = "";
        int count = t.length();//覆盖需要的总符合次数
        while (right < s.length()) {
            char currentChar = s.charAt(right);
            if (help[currentChar] > 0) {    //若 currentChar在 t 中
                // ---currentChar在t,s同时出现
                //在遍历s时找到了t中出现的字符,且 出现次数并没有超出t出现的次数[次数超出则不再 >0]
                count--;        //计作: 符合了一个
            }
            help[currentChar]--; //同时在help表中,将currentChar的统计次数-1
            System.out.println("help = " + Arrays.toString(help));
            while (count == 0) { //如果移动到了合适的窗口(当s的当前子串已经全部覆盖,即已找到从left下标开始的最小覆盖子串)
                //当 count == 0 时,help表中仅所有匹配字母的计数显示为0, 而其他均为负数
                if (right - left + 1 < minSize) {
                    minSize = right - left + 1;
                    res = s.substring(left, right + 1);//更新结果
                }
                /**
                 * left指针右移工作开始
                 */
                currentChar = s.charAt(left); //取出当前覆盖子串中的最左值
                if (help[currentChar] == 0) { //help表中仅所有匹配字母的计数显示为0, 而其他均为负数
                    // 若该值为 help表中对应的匹配字母, 其计数重新 加回1
                    count++;
                }
                help[currentChar]++;
                left++; //缩小窗口直至count!=0
                /**
                 * left指针右移工作完成
                 */
            }
            right++;
        }
        return res;
    }
```

### 模拟行为

[59.螺旋矩阵II](https://mp.weixin.qq.com/s/Hn6-mlCPvKAdWbiFfQyaaw)

```java
    //根据54 的思路延伸得解如下
    public int[][] generateMatrix(int n) {
        boolean isHorizontal = false;
        boolean isAscend = true;
        int[][] matrix = new int[n][n];
        //规律总结如下:
        //横竖横竖横竖  一定 (即每1轮变一次)
        //升升降降升升  一定 (即每2轮变一次)
        //除第一行外,每2轮会减少输出一个数字
        int fixed_n = n;
        int fixed_size = n * n;
        int k = 0;
        int num = 1;
        int index = -1; //该变量可以看作是将二维数组当成一维数组时的数组下标,其与二维数组下标的关系,
        //必定是 matrix[index / fixed_n][index - (index / fixed_n) * fixed_n]
        for (int i = 0; i < n; i++) {  //将第一行排除在规律外
            index++;
            matrix[index / fixed_n][index - (index / fixed_n) * fixed_n] = num++;
        }
        while (k < fixed_size) {
            if (k % 2 == 0) {
                n--;
            }
            for (int i = 0; i < n; i++) {
                index = isHorizontal ? (isAscend ? index + 1 : index - 1) : (isAscend ? index + fixed_n : index - fixed_n);
                matrix[index / fixed_n][index - (index / fixed_n) * fixed_n] = num++;
            }
            isHorizontal = !isHorizontal;
            if (k % 2 == 0) {
                isAscend = !isAscend;
            }
            k++;
        }
        return matrix;
    }

        //去掉冗餘循環
        public int[][] generateMatrix(int n) {
        boolean isHorizontal = true;
        boolean isAscend = true;
        int[][] matrix = new int[n][n];
        //规律总结如下:
        //横竖横竖横竖  一定 (即每1轮变一次)
        //升升降降升升  一定 (即每2轮变一次)
        //除第一行外,每2轮会减少输出一个数字
        int fixed_n = n;
        int fixed_size = n * n;
        int k = 0;
        int num = 1;
        int index = -1; //该变量可以看作是将二维数组当成一维数组时的数组下标,其与二维数组下标的关系,
        //必定是 matrix[index / fixed_n][index - (index / fixed_n) * fixed_n]

        
        while (n > 0) {//测试时避免死循环用 && (m > 0 || n > 0)
        // System.err.println("=========================================================");

        // System.err.println((isHorizontal ? "水平 " : "垂直 ") + (isAscend ? "升序 " : "降序 ")+ ", n = " + n);

        for (int i = 0; i < n; i++) {
        index = isHorizontal ? (isAscend ? index + 1 : index - 1) : (isAscend ? index + fixed_n : index - fixed_n);
        // System.err.println("index = " + index);
        matrix[index / fixed_n][index - (index / fixed_n) * fixed_n] = num++;
        // for (int[] ints : matrix) {
        //     System.err.println("ints = " + Arrays.toString(ints));
        // }
        }
        if (k % 2 == 0) {
        n--;
        // System.err.println("n--");
        }

        isHorizontal = !isHorizontal;

        if ((k + 1) % 2 == 0) {
        isAscend = !isAscend;
        }
        k++;
        }
        return matrix;
        }
    
```
模拟类的题目在数组中很常见，不涉及到什么算法，就是单纯的模拟，十分考察大家对代码的掌控能力。

在这道题目中，我们再一次介绍到了**循环不变量原则**，其实这也是写程序中的重要原则。

相信大家又遇到过这种情况： 感觉题目的边界调节超多，一波接着一波的判断，找边界，踩了东墙补西墙，好不容易运行通过了，代码写的十分冗余，毫无章法，其实**真正解决题目的代码都是简洁的，或者有原则性的**，大家可以在这道题目中体会到这一点。

相关题目：


* 54.螺旋矩阵
```java
    public List<Integer> spiralOrder(int[][] matrix) {
        boolean isHorizontal = false;
        boolean isAscend = true;
        List<Integer> resultList = new ArrayList<>();
        //规律总结如下:
        //横竖横竖横竖  一定 (即每1轮变一次)
        //升升降降升升  一定 (即每2轮变一次)
        //除第一行外,每2轮会减少输出一个数字
        int m = matrix.length;//m行 : y轴
        int n = matrix[0].length;//n列 : x 轴
        int fixed_n = n;
        int fixed_size = m * n;
        int k = 0;
        int index = -1; //该变量可以看作是将二维数组当成一维数组时的数组下标(例如3*3矩阵其实是一维数组从0数到9),其与二维数组下标的关系,
//必定是 matrix[index / fixed_n][index - (index / fixed_n) * fixed_n]
        for (int i = 0; i < n; i++) {  //将第一行排除在规律外
            index++;
            resultList.add(matrix[index / fixed_n][index - (index / fixed_n) * fixed_n]);
        }
        while (resultList.size() != fixed_size) {//测试时避免死循环用 && (m > 0 || n > 0)
            if (k % 2 == 0) {
                m--;
                n--;
            }
            //System.out.println((isHorizontal ? "水平 " : "垂直 ") + (isAscend ? "升序 " : "降序 ") + "m = " + m + ", n = " + n);
            if (isHorizontal) {
                for (int i = 0; i < n; i++) {
                    index = isAscend ? index + 1 : index - 1;
                    resultList.add(matrix[index / fixed_n][index - (index / fixed_n) * fixed_n]);
                }
            } else {
                for (int i = 0; i < m; i++) {
                    index = isAscend ? index + fixed_n : index - fixed_n;
                    resultList.add(matrix[index / fixed_n][index - (index / fixed_n) * fixed_n]);
                }
            }

            isHorizontal = !isHorizontal;
            if (k % 2 == 0) {
                isAscend = !isAscend;
            }
            k++;
        }
        return resultList;
    }
 
```  


* 剑指Offer 29.顺时针打印矩阵
```java
//和上题基本一样
//由于入参范围需要验证,因而添加:
   if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
       return new int[0];
   }
//且返回值改类型
        int[] resultArray = new int[resultList.size()];
        for (int i = 0; i < resultList.size(); i++) {
            resultArray[i] = resultList.get(i);
        }
        return  resultArray;
```

这里面试中数组相关的理论知识就介绍完了。




-----------------------
* 作者微信：[程序员Carl](https://mp.weixin.qq.com/s/b66DFkOp8OOxdZC_xLZxfw)
* B站视频：[代码随想录](https://space.bilibili.com/525438321)
* 知识星球：[代码随想录](https://mp.weixin.qq.com/s/QVF6upVMSbgvZy8lHZS3CQ)
<div align="center"><img src=../pics/公众号.png width=450 alt=> </img></div>
