6月算法集训第4天

#### [1221. 分割平衡字符串](https://leetcode.cn/problems/split-a-string-in-balanced-strings/)

算法分析

1. 定义出现\'L\' 出现次数减去\'R\' 出现次数为平衡度。
2. 平衡字符串的平衡度自然为零。2个平衡字符串连接必然是平衡字符串。
3. 本题要求分割为最大平衡字符串
4. 所以，一旦发现平衡度为零，就分割平衡字符串。

```java
class Solution {
    public int balancedStringSplit(String s) {
        int i;
        int cnt = 0,ret = 0;

        for ( i = 0; i < s.length(); ++i) {
            cnt += s.charAt( i )=='L'? 1 : -1;
            if(cnt == 0){
                ++ret;
            }

        }
        return ret;
    }
}
```



#### [1217. 玩筹码](https://leetcode.cn/problems/minimum-cost-to-move-chips-to-the-same-position/)

算法分析

1. 假定已经确定移动位置，移动奇数为cost 1。移动偶数位cost 0;
2. 那么，只要确定筹码的出现次数的最少奇数或者偶数就好了。
3. 因为，移动2位成本0，移动1位成本一，所以移动出现次数最少的偶数/奇数即可

```java
class Solution {
    public int minCostToMoveChips(int[] position) {
        int odd = 0,even = 0;
        for (int i = 0; i < position.length; i++) {
            if(position[i] %2 == 0){
                ++even;
            }else {
                ++odd;
            }
        }
        return odd > even ?even:odd;
    }
}
```



#### [1029. 两地调度](https://leetcode.cn/problems/two-city-scheduling/)

算法分析

1. 公司首先将这 2N 个人全都安排飞往 B 市，再选出 N 个人改变它们的行程，让他们飞往 AA 市。如果选择改变一个人的行程，那么公司将会额外付出 price_A - price_B 的费用，这个费用可正可负。
2. 因此最优的方案是，选出 `price_A - price_B` 最小的 N*N* 个人，让他们飞往 `A` 市，其余人飞往 `B` 市。

3. 按照 `price_A - price_B` 从小到大排序；

4. 将前 N 个人飞往 `A` 市，其余人飞往 `B` 市，并计算出总费用。

```java
class Solution {
    public int twoCitySchedCost(int[][] costs) {
        Arrays.sort(costs, (o1, o2) -> o1[0] - o1[1] - (o2[0] - o2[1]) );

        int total = 0;
        int n = costs.length / 2;

        for (int i = 0; i < n; i++) {
            total +=costs[i][0] +costs[i+n][1];
        }
        return total;
    }
}
```

#### [面试题 10.11. 峰与谷](https://leetcode.cn/problems/peaks-and-valleys-lcci/)

算法分析

1. 先对数组排序
2. 使用循环交换第一个和第二个元素，第三个和第四个元素，依次类推。
3. 从而保证了`峰-谷交替`

```java
class Solution {
    public void wiggleSort(int[] nums) {
        Arrays.sort( nums );
        int temp,i;

        for ( i = 0; i < nums.length-1 ; i+=2) {
            temp = nums[i];
            nums[i] = nums[i+1];
            nums[i+1] = temp;
        }
    }
}
```