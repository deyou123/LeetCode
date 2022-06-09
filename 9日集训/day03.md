#### [33. 搜索旋转排序数组](https://leetcode.cn/problems/search-in-rotated-sorted-array/)

>整数数组 `nums` 按升序排列，数组中的值 **互不相同** 。
>
>在传递给函数之前，`nums` 在预先未知的某个下标 `k`（`0 <= k < nums.length`）上进行了 **旋转**，使数组变为 `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]`（下标 **从 0 开始** 计数）。例如， `[0,1,2,4,5,6,7]` 在下标 `3` 处经旋转后可能变为 `[4,5,6,7,0,1,2]` 。
>
>给你 **旋转后** 的数组 `nums` 和一个整数 `target` ，如果 `nums` 中存在这个目标值 `target` ，则返回它的下标，否则返回 `-1` 。
>
>**示例 1：**
>
>```
>输入：nums = [4,5,6,7,0,1,2], target = 0
>输出：4
>```
>
>**示例 2：**
>
>```
>输入：nums = [4,5,6,7,0,1,2], target = 3
>输出：-1
>```
>
>**示例 3：**
>
>```
>输入：nums = [1], target = 0
>输出：-1
>```
>
>**提示：**
>
>- `1 <= nums.length <= 5000`
>- `-10^4 <= nums[i] <= 10^4`
>- `nums` 中的每个值都 **独一无二**
>- 题目数据保证 `nums` 在预先未知的某个下标上进行了旋转
>- `-10^4 <= target <= 10^4`
>
>
>
>**进阶：**你可以设计一个时间复杂度为 `O(log n)` 的解决方案吗

##### 题目分析

在数组中找到目标值。数组特色，部分有序。
解题思路
第一种方法，遍历数组找到target 目标值，


第二种方法二分查找法
      1. 注意事项 边界值问题
      2. 二分查找后，总有一遍是有序的，如果目标值在有序这边，进行二分查找即可。

##### 源码

```java
class Solution {
    public int search(int[] nums, int target) {
        int length = nums.length;
        if(length ==0) return -1;
        if(length == 1) return target == nums[0]? 0:-1;

        int l = 0,r = length-1 ;

        while (l<=r){
            int mid = (l +r) /2 ;
            if(target == nums[mid]) return mid;

            if(nums[0] <=nums[mid]){
                if(nums[0]<=target && target<nums[mid]){
                    r = mid -1;

                }else {
                    l = mid +1;
                }
            }else{
                if(nums[mid] < target && target <=nums[r]){
                    l = mid +1;
                }else {
                    r = mid-1;
                }
            }
        }

        return -1;

    }
}
```



#### [81. 搜索旋转排序数组 II](https://leetcode.cn/problems/search-in-rotated-sorted-array-ii/)

已知存在一个按非降序排列的整数数组 `nums` ，数组中的值不必互不相同。

在传递给函数之前，`nums` 在预先未知的某个下标 `k`（`0 <= k < nums.length`）上进行了 **旋转** ，使数组变为 `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]`（下标 **从 0 开始** 计数）。例如， `[0,1,2,4,4,4,5,6,6,7]` 在下标 `5` 处经旋转后可能变为 `[4,5,6,6,7,0,1,2,4,4]` 。

给你 **旋转后** 的数组 `nums` 和一个整数 `target` ，请你编写一个函数来判断给定的目标值是否存在于数组中。如果 `nums` 中存在这个目标值 `target` ，则返回 `true` ，否则返回 `false` 。

你必须尽可能减少整个操作步骤。



**示例 1：**

```
输入：nums = [2,5,6,0,0,1,2], target = 0
输出：true
```

**示例 2：**

```
输入：nums = [2,5,6,0,0,1,2], target = 3
输出：false
```



**提示：**

- `1 <= nums.length <= 5000`
- `-104 <= nums[i] <= 104`
- 题目数据保证 `nums` 在预先未知的某个下标上进行了旋转
- `-104 <= target <= 104`



**进阶：**

- 这是 [搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/description/) 的延伸题目，本题中的 `nums` 可能包含重复元素。
- 这会影响到程序的时间复杂度吗？会有怎样的影响，为什么？



   

```java
class Solution {
    public boolean search(int[] nums, int target) {
        //解题思路：旋转后的数组二分后总有一半是有序的，旋转有序的那部分用二分查找判断；
        //注意：元素可以重复，当左右边界和中间元素相同时，无法判断哪边有序，左右边界向中间移动一位后继续；
        int left = 0;
        int right = nums.length - 1;
        while(left <= right){
            int mid = (left + right)>>1;
            if(nums[mid] == target){
                return true;
            }
            //左右边界和中间元素相同无法区分哪边有序，则移动边界向中间移动
            if(nums[left] == nums[mid] && nums[right] == nums[mid]){
                left++;
                right--;
            }else if(nums[left] <= nums[mid]){
                //左边有序则，左边按照二分法判断边界
                if(nums[left] <= target && target < nums[mid]){
                    right = mid -1;
                }else{
                    left = mid + 1;
                }
            }else{
                //右边有序
                if(nums[mid] < target && target <= nums[right]){
                    left = mid + 1;
                }else{
                    right = mid - 1;
                }
            }
        }

        return false;
    }
}
```



#### [153. 寻找旋转排序数组中的最小值](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/)



已知一个长度为 `n` 的数组，预先按照升序排列，经由 `1` 到 `n` 次 **旋转** 后，得到输入数组。例如，原数组 `nums = [0,1,2,4,5,6,7]` 在变化后可能得到：

- 若旋转 `4` 次，则可以得到 `[4,5,6,7,0,1,2]`
- 若旋转 `7` 次，则可以得到 `[0,1,2,4,5,6,7]`

注意，数组 `[a[0], a[1], a[2], ..., a[n-1]]` **旋转一次** 的结果为数组 `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]` 。

给你一个元素值 **互不相同** 的数组 `nums` ，它原来是一个升序排列的数组，并按上述情形进行了多次旋转。请你找出并返回数组中的 **最小元素** 。

你必须设计一个时间复杂度为 `O(log n)` 的算法解决此问题。



**示例 1：**

```
输入：nums = [3,4,5,1,2]
输出：1
解释：原数组为 [1,2,3,4,5] ，旋转 3 次得到输入数组。
```

**示例 2：**

```
输入：nums = [4,5,6,7,0,1,2]
输出：0
解释：原数组为 [0,1,2,4,5,6,7] ，旋转 4 次得到输入数组。
```

**示例 3：**

```
输入：nums = [11,13,15,17]
输出：11
解释：原数组为 [11,13,15,17] ，旋转 4 次得到输入数组。
```



**提示：**

- `n == nums.length`
- `1 <= n <= 5000`
- `-5000 <= nums[i] <= 5000`
- `nums` 中的所有整数 **互不相同**
- `nums` 原来是一个升序排序的数组，并进行了 `1` 至 `n` 次旋转



>算法分析 输入数组为一个旋转n 次后的数组，不确定n 的大小。 求出旋转数组的最小值。
>
>- 方法一 循环遍历输出。
>- 方法二 二分法循环遍历输出



```java
class Solution {
    public int findMin(int[] nums) {


        int left = 0;
        int right = nums.length -1;

        int mid;
        while (left < right){
             mid = (right + left) >> 1;
            if(nums[mid] < nums[right]){
                right = mid;
            }else {
                left = mid +1;
            }
        }
      return nums[left];
    }
}
```

#### [70. 爬楼梯](https://leetcode.cn/problems/climbing-stairs/)

假设你正在爬楼梯。需要 *n* 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

**注意：**给定 *n* 是一个正整数。

**示例 1：**

```
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶
```

**示例 2：**

```
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
```

Related Topics

记忆化搜索

数学

动态规划

解题思路



方式一
$$
F(n)=
\begin{cases}
f(1)=1,n=1\\
f(2)=2,n=2\\
f(n-1)+f(n-2),n>2
\end{cases}
$$
递归

```java
class Solution {
    public int climbStairs(int n) {
        if(n == 1) return 1;
        if(n == 2) return 2;
        int res = climbStairs( n  -1) +climbStairs( n-2 );
        return res;
    }
}
```

运行时间超时

空间复杂度O(n)

方式二

动态规划

```java
class Solution {
    public int climbStairs(int n) {
       int[] dp = new int[n+1];
       dp[0] = dp[1] = 1;

        for (int i = 2; i <= n ; i++) {
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];

    }
}
```

时间复杂度O(n)

空间复杂度O(1)

方式三数学通向公式

$$
F(n)= \frac{({\frac{1+\sqrt{5}}{2}})^n-({\frac{1-\sqrt{5}}{2}})^n}{\sqrt{5}}
$$



```java
class Solution {
    public int climbStairs(int n) {
        double sqrt5 = Math.sqrt( 5 );
        return (int)((Math.pow( (1+sqrt5) /2, n+1 ) - Math.pow( (1-sqrt5) /2, n+1 ))/sqrt5) ;
    }
}
```

方式四

```java
class Solution {
    public int climbStairs(int n) {
      if(n == 1) return 1;

      int fisrt = 1;
      int second = 2;
        for (int i = 3; i <= n  ; i++) {
            int third = fisrt + second;
            fisrt =second;
            second = third;
        }
        return second;
    }
}
```



还有一种矩阵方式

暂时不写了，知识点掌握不全。回头学习后补上

#### [509. 斐波那契数](https://leetcode.cn/problems/fibonacci-number/)

斐波那契数 （通常用 F(n) 表示）形成的序列称为 斐波那契数列 。该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。也就是：

F(0) = 0，F(1) = 1
F(n) = F(n - 1) + F(n - 2)，其中 n > 1
给定 n ，请计算 F(n) 。

 >示例 1：
 >
 >输入：n = 2
 >输出：1
 >解释：F(2) = F(1) + F(0) = 1 + 0 = 1
 >示例 2：
 >
 >输入：n = 3
 >输出：2
 >解释：F(3) = F(2) + F(1) = 1 + 1 = 2
 >示例 3：
 >
 >输入：n = 4
 >输出：3
 >解释：F(4) = F(3) + F(2) = 2 + 1 = 3
 >
 >
 >提示：
 >
 >0 <= n <= 30
 >



```java
class Solution {
    public int fib(int n) {
        if(n == 0) return 0;
        if(n == 1) return 1;
        return fib(n-1) + fib(n-2);
    }
}
```

其他方法参照上面一题

#### [1137. 第 N 个泰波那契数](https://leetcode.cn/problems/n-th-tribonacci-number/)

泰波那契序列 Tn 定义如下：

T0 = 0, T1 = 1, T2 = 1, 且在 n >= 0 的条件下 Tn+3 = Tn + Tn+1 + Tn+2

给你整数 `n`，请返回第 n 个泰波那契数 Tn 的值。



**示例 1：**

```
输入：n = 4
输出：4
解释：
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4
```

**示例 2：**

```
输入：n = 25
输出：1389537
```



**提示：**

- `0 <= n <= 37`
- 答案保证是一个 32 位整数，即 `answer <= 2^31 - 1`。



```java
class Solution {
    public int tribonacci(int n) {
        if(n == 0) return 0;
        if(n ==1 || n == 2) return 1;

       int [] dp = new int[n +1];
       dp[0] = 0;
       dp[1] = 1;
       dp[2] =1;
        for (int i = 3; i < n+1; i++) {
            dp[i] = dp[i-3] +dp[i-2] + dp[i-1];
        }

        return dp[n];

    }
}
```

解法二 

矩阵相乘

日后再说

#### [2006. 差的绝对值为 K 的数对数目](https://leetcode.cn/problems/count-number-of-pairs-with-absolute-difference-k/)

给你一个整数数组 `nums` 和一个整数 `k` ，请你返回数对 `(i, j)` 的数目，满足 `i < j` 且 `|nums[i] - nums[j]| == k` 。

`|x|` 的值定义为：

- 如果 `x >= 0` ，那么值为 `x` 。
- 如果 `x < 0` ，那么值为 `-x` 。



**示例 1：**

```
输入：nums = [1,2,2,1], k = 1
输出：4
解释：差的绝对值为 1 的数对为：
- [1,2,2,1]
- [1,2,2,1]
- [1,2,2,1]
- [1,2,2,1]
```

**示例 2：**

```
输入：nums = [1,3], k = 3
输出：0
解释：没有任何数对差的绝对值为 3 。
```

**示例 3：**

```
输入：nums = [3,2,1,5,4], k = 2
输出：3
解释：差的绝对值为 2 的数对为：
- [3,2,1,5,4]
- [3,2,1,5,4]
- [3,2,1,5,4]
```



**提示：**

- `1 <= nums.length <= 200`
- `1 <= nums[i] <= 100`
- `1 <= k <= 99`

Related Topics

数组



方法一暴力破解

```java
class Solution {
    public int countKDifference(int[] nums, int k) {
      int ans = 0;
      for (int i = 0; i < nums.length; i++) {
         for (int j = i + 1; j < nums.length ; j++) {
            if(Math.abs((nums[i]-nums[j])) == k){

               ++ans;
            }
         }
      }
      return ans;
    }
}
```

方法二 Hash + 一次遍历

```java
class Solution {
    public int countKDifference(int[] nums, int k) {
		HashMap<Integer,Integer> map = new HashMap<>();
		int res =0;
		for (int i = 0; i < nums.length; i++) {
			res +=map.getOrDefault( nums[i] -k,0 ) + map.getOrDefault( nums[i]+k ,0);
			map.put( nums[i], map.getOrDefault(nums[i],0)+1 );
		}
		return res;
    }
}
```

#### [LCP 01. 猜数字](https://leetcode.cn/problems/guess-numbers/)

小A 和 小B 在玩猜数字。小B 每次从 1, 2, 3 中随机选择一个，小A 每次也从 1, 2, 3 中选择一个猜。他们一共进行三次这个游戏，请返回 小A 猜对了几次？

输入的guess数组为 小A 每次的猜测，answer数组为 小B 每次的选择。guess和answer的长度都等于3。

 

示例 1：

输入：guess = [1,2,3], answer = [1,2,3]
输出：3
解释：小A 每次都猜对了。
示例 2：

输入：guess = [2,2,3], answer = [3,2,1]
输出：1
解释：小A 只猜对了第二次。



题目比较简单

```java
class Solution {
    public int game(int[] guess, int[] answer) {
        int cnt =0;

        for (int i = 0; i < guess.length; i++) {
            if(guess[i] == answer[i]){
                cnt++;
            }

        }
        return cnt;

    }
}
```

#### [LCP 06. 拿硬币](https://leetcode.cn/problems/na-ying-bi/)

桌上有 `n` 堆力扣币，每堆的数量保存在数组 `coins` 中。我们每次可以选择任意一堆，拿走其中的一枚或者两枚，求拿完所有力扣币的最少次数。

**示例 1：**

> 输入：`[4,2,1]`
>
> 输出：`4`
>
> 解释：第一堆力扣币最少需要拿 2 次，第二堆最少需要拿 1 次，第三堆最少需要拿 1 次，总共 4 次即可拿完。

**示例 2：**

> 输入：`[2,3,10]`
>
> 输出：`8`

**限制：**

- `1 <= n <= 4`
- `1 <= coins[i] <= 10`

代码

```java
class Solution {
    public int minCount(int[] coins) {
        int ans =0;
        for (int i = 0; i < coins.length; i++) {
            if((coins[i] %2) ==0){
                ans += coins[i] / 2;
            }else{
                ans += coins[i] /2 +1;
            }
        }
        return ans;
    }
}
```

#### [剑指 Offer II 069. 山峰数组的顶部](https://leetcode.cn/problems/B1IidL/)

符合下列属性的数组 arr 称为 山脉数组 ：

* arr.length >= 3
* 存在 i（0 < i < arr.length - 1）使得：
  * arr[0] < arr[1] < ... arr[i-1] < arr[i]
  * arr[i] > arr[i+1] > ... > arr[arr.length - 1]

给你由整数组成的山脉数组 arr ，返回任何满足 arr[0] < arr[1] < ... arr[i - 1] < arr[i] > arr[i + 1] > ... > arr[arr.length - 1] 的下标 i 。

 

示例 1：

输入：arr = [0,1,0]
输出：1
示例 2：

输入：arr = [0,2,1,0]
输出：1
示例 3：

输入：arr = [0,10,5,2]
输出：1
示例 4：

输入：arr = [3,4,5,1]
输出：2
示例 5：

输入：arr = [24,69,100,99,79,78,67,36,26,19]
输出：2


提示：

3 <= arr.length <= 104
0 <= arr[i] <= 106
题目数据保证 arr 是一个山脉数组


进阶：很容易想到时间复杂度 O(n) 的解决方案，你可以设计一个 O(log(n)) 的解决方案吗？

方法一 循环遍历

```java
class Solution {
    public int peakIndexInMountainArray(int[] arr) {

      int ans = 0;
      int maxVal=arr[0];

      for (int i = 0; i < arr.length; i++) {
         if(arr[i]>maxVal){
            maxVal =arr[i];
            ans = i;
         }
      }
      return ans;

    }
}
```

方法二 二分查找法

```java
class Solution {
    public int peakIndexInMountainArray(int[] arr) {

      int ans = 0;
      int left =0;
      int right = arr.length -1;

      while (left <= right){
         int mid = (left + right) >> 1;
         if(arr[mid] >arr[mid+1]){
            ans = mid;
            right =mid -1;
         }else{
            left = mid +1;
         }

      }
      return ans;

    }
}
```