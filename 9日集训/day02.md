# 剑指 offer 64

<p>求 <code>1+2+...+n</code> ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入:</strong> n = 3
<strong>输出:&nbsp;</strong>6
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入:</strong> n = 9
<strong>输出:&nbsp;</strong>45
</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>1 &lt;= n&nbsp;&lt;= 10000</code></li>
</ul>
<div><div>Related Topics</div><div><li>位运算</li><li>递归</li><li>脑筋急转弯</li></div></div><br><div><li>👍 382</li><li>👎 0</li></div>

## 解题思路

使用递归

* $$n==1$$时，返回结果为1.
* $$ n > 1$$时 ， 返回结果为 $$ n + sum(n-1)$$

## 源码

```java
class Solution {
    public int sumNums(int n) {
        boolean x = n  > 1 && (n += sumNums( n-1 )) >0;
        return n;
    }
}
```

# 2 的幂

<p>给你一个整数 <code>n</code>，请你判断该整数是否是 2 的幂次方。如果是，返回 <code>true</code> ；否则，返回 <code>false</code> 。</p>

<p>如果存在一个整数 <code>x</code> 使得 <code>n == 2<sup>x</sup></code> ，则认为 <code>n</code> 是 2 的幂次方。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>n = 1
<strong>输出：</strong>true
<strong>解释：</strong>2<sup>0</sup> = 1
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>n = 16
<strong>输出：</strong>true
<strong>解释：</strong>2<sup>4</sup> = 16
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>n = 3
<strong>输出：</strong>false
</pre>

<p><strong>示例 4：</strong></p>

<pre>
<strong>输入：</strong>n = 4
<strong>输出：</strong>true
</pre>

<p><strong>示例 5：</strong></p>

<pre>
<strong>输入：</strong>n = 5
<strong>输出：</strong>false
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>-2<sup>31</sup> <= n <= 2<sup>31</sup> - 1</code></li>
</ul>

<p> </p>

<p><strong>进阶：</strong>你能够不使用循环/递归解决此问题吗？</p>
<div><li>👍 504</li><li>👎 0</li></div>

## 解题思路

* 若 $$n = 2^x $$且 $$x$$ 为自然数（即 $$n$$ 为 $$2$$ 的幂），则一定满足以下条件：
  1. 恒有 $$n\&(n-1)==0$$，这是因为：
     * $$n$$ 二进制最高位为 1，其余所有位为 0；
     * $$n−1$$ 二进制最高位为 0，其余所有位为 1；
  2. 一定满足$$ n > 0$$。
* 因此，通过 $$n > 0$$ 且  $$n\&(n-1)==0$$ 即可判定是否满足$$ n = 2^x$$.

## 源码

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        return n > 0 && (n & (n -1)) == 0;
    }
}
```

# 3 的 幂

<p>给定一个整数，写一个函数来判断它是否是 3&nbsp;的幂次方。如果是，返回 <code>true</code> ；否则，返回 <code>false</code> 。</p>

<p>整数 <code>n</code> 是 3 的幂次方需满足：存在整数 <code>x</code> 使得 <code>n == 3<sup>x</sup></code></p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>n = 27
<strong>输出：</strong>true
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>n = 0
<strong>输出：</strong>false
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>n = 9
<strong>输出：</strong>true
</pre>

<p><strong>示例 4：</strong></p>

<pre>
<strong>输入：</strong>n = 45
<strong>输出：</strong>false
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>-2<sup>31</sup> &lt;= n &lt;= 2<sup>31</sup> - 1</code></li>
</ul>

<p>&nbsp;</p>

<p><strong>进阶：</strong>你能不使用循环或者递归来完成本题吗？</p>
<div><li>👍 255</li><li>👎 0</li></div>



## 方法一

* 我们不断地将 $$n$$ 除以 3，直到 $$n=1$$。如果此过程中 $$n$$ 无法被 3 整除，就说明 $$n$$ 不是 3 的幂。

  本题中的 $n$ 可以为负数或 $0$，可以直接提前判断该情况并返回 $False$，也可以进行试除，因为负数或 0 也无法通过多次除以 3得到 1。

  

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        if(n <= 0) return false;
        while( n %3 == 0){
            n /= 3;
        }
        return n == 1;
    }
}
```

## 方法二

我们还可以使用一种较为取巧的做法。

在题目给定的 32 位有符号整数的范围内，最大的 3 的幂为 $3^{19}$ = 11622614673 
19。我们只需要判断 n 是否是 $3^{19}$  的约数即可。

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        return  n > 0 && (1162261467 % n) == 0;
    }
}
```

# 4 的幂

<p>给定一个整数，写一个函数来判断它是否是 4 的幂次方。如果是，返回 <code>true</code> ；否则，返回 <code>false</code> 。</p>

<p>整数 <code>n</code> 是 4 的幂次方需满足：存在整数 <code>x</code> 使得 <code>n == 4<sup>x</sup></code></p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>n = 16
<strong>输出：</strong>true
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>n = 5
<strong>输出：</strong>false
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>n = 1
<strong>输出：</strong>true
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>-2<sup>31</sup> &lt;= n &lt;= 2<sup>31</sup> - 1</code></li>
</ul>

<p>&nbsp;</p>

<p><strong>进阶：</strong>你能不使用循环或者递归来完成本题吗？</p>
<div><li>👍 301</li><li>👎 0</li></div>

## 方法一 二进制表示中 11 的位置



```java
class Solution {
    public boolean isPowerOfFour(int n) {
        return n > 0 && (n & (n-1)) == 0 && (n & 0xaaaaaaaa) == 0;
    }
}
```



## 方法二 取模性质

![image-20220608134257203](http://typora-dy.oss-cn-beijing.aliyuncs.com/img/image-20220608134257203.png)


```java
class Solution {
    public boolean isPowerOfFour(int n) {
        return n > 0 && (n & (n - 1)) == 0 && (n & 0xaaaaaaaa) == 0;
    }
}
```



![image-20220608134407712](http://typora-dy.oss-cn-beijing.aliyuncs.com/img/image-20220608134407712.png)

```java
class Solution {
    public boolean isPowerOfFour(int n) {
        return n > 0 && (n & (n - 1)) == 0 && n % 3 == 1;
    }
}
```



# n 的第 k 个因子



<p>给你两个正整数&nbsp;<code>n</code> 和&nbsp;<code>k</code>&nbsp;。</p>

<p>如果正整数 <code>i</code> 满足 <code>n % i == 0</code> ，那么我们就说正整数 <code>i</code> 是整数 <code>n</code>&nbsp;的因子。</p>

<p>考虑整数 <code>n</code>&nbsp;的所有因子，将它们 <strong>升序排列</strong>&nbsp;。请你返回第 <code>k</code>&nbsp;个因子。如果 <code>n</code>&nbsp;的因子数少于 <code>k</code>&nbsp;，请你返回 <strong>-1</strong>&nbsp;。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>n = 12, k = 3
<strong>输出：</strong>3
<strong>解释：</strong>因子列表包括 [1, 2, 3, 4, 6, 12]，第 3 个因子是 3 。
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>n = 7, k = 2
<strong>输出：</strong>7
<strong>解释：</strong>因子列表包括 [1, 7] ，第 2 个因子是 7 。
</pre>

<p><strong>示例 3：</strong></p>

<pre><strong>输入：</strong>n = 4, k = 4
<strong>输出：</strong>-1
<strong>解释：</strong>因子列表包括 [1, 2, 4] ，只有 3 个因子，所以我们应该返回 -1 。
</pre>

<p><strong>示例 4：</strong></p>

<pre><strong>输入：</strong>n = 1, k = 1
<strong>输出：</strong>1
<strong>解释：</strong>因子列表包括 [1] ，第 1 个因子为 1 。
</pre>

<p><strong>示例 5：</strong></p>

<pre><strong>输入：</strong>n = 1000, k = 3
<strong>输出：</strong>4
<strong>解释：</strong>因子列表包括 [1, 2, 4, 5, 8, 10, 20, 25, 40, 50, 100, 125, 200, 250, 500, 1000] 。
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= k &lt;= n &lt;= 1000</code></li>
</ul>
<div><div>Related Topics</div><div><li>数学</li></div></div><br><div><li>👍 14</li><li>👎 0</li></div>

## 方法一

解题思路

* 使用循环，遍历计算因子$n \% i == 0$
* 满足条件后，$cnt$  计数并和 $k$ 比较。
* $cnt == k$  返回 因子 $i$ 的值

```java
class Solution {
    public int kthFactor(int n, int k) {
       //i 为因子，cnt 为因子集合的位置。
      int i,cnt = 0;

      for (i = 1; i <= n ; ++i) {
         if(n % i == 0){
            ++cnt;
            if(cnt == k){
               return i;
            }
         }
      }
      return -1;
    }
}
```

## 方法二

* 在上面的基础上，减少时间复杂度到 $\sqrt{n}$,

* 如果 $n$ 是完全平方数，那么满足 $x^2 = n$ 的因子 $x$ 被枚举了两次，需要忽略其中的一次。

```java
class Solution {
    public int kthFactor(int n, int k) {
       int cnt = 0,factor;

      for (factor = 1; factor * factor <= n ; factor++) {
         if( n % factor == 0){
            cnt++;

         }
         if(cnt == k){
            return factor;
         }

      }

      --factor;
      //判断n 是否为完全平方数
      if (factor * factor == n){
         factor --;
      }
      //查询根号n 后的因子，返回用 n / factor 表示
      for (; factor > 0 ; --factor) {
         if( n % factor == 0){
            cnt++;

         }
         if(cnt == k){
            return n /factor;
         }

      }
      return -1;

    }
}
```

# 完全平方数

<p>给定一个 <strong>正整数</strong> <code>num</code> ，编写一个函数，如果 <code>num</code> 是一个完全平方数，则返回 <code>true</code> ，否则返回 <code>false</code> 。</p>

<p><strong>进阶：不要</strong> 使用任何内置的库函数，如  <code>sqrt</code> 。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>num = 16
<strong>输出：</strong>true
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>num = 14
<strong>输出：</strong>false
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= num <= 2^31 - 1</code></li>
</ul>
<div><li>👍 398</li><li>👎 0</li></div>



## 解题思路

* 使用二分法

```java
class Solution {
    public boolean isPerfectSquare(int num) {
        int left = 1, right = num;

        do {
           int mid = (right-left)/2 + left;
           //使用long 保证不超过2^31 - 1。
           long square = (long)mid * mid;
           if(square > num){
               right = mid -1;
           }else if(square < num){
               left = mid + 1;
           }else {
               return true;
           }

        }while ((left <= right));
        return false;
    }
}
```

