# House Robber
---
## 题意

**https://leetcode.com/problems/house-robber/description/**

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

**Example 1:**</p>

Input: [1,2,3,1]</p>
Output: 4</p>
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
             
**Example 2:**</p>

Input: [2,7,9,3,1]</p>
Output: 12 </p>
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
             
             
中文意思： 你是一个盗贼，你需要抢劫一个街道上的屋子，每个屋子有一定数量的钱，但是你不能一晚上连续抢两家相邻的，这会触发报警器，在不触发报警的同时，求得一晚上最大的抢劫的钱的数量，并返回。


### 思路
定义nums[]存放的是每个房子的钱数。
逆向的思考，抢的可能性有两种，最后一家已经被抢，考虑的应该上一家抢的是nums[nums.length - 2] ,如果没有抢，那么上一家应该是 nums[nums.length - 1]


### 解法1 ：
暴力破解：全局搜索，时间复杂度过高

```java
    public static int solve(int idx, int[] nums){
        if (idx < 0)
            return 0;
        return Math.max(solve(idx - 1 ,nums),solve(idx - 2 ,nums) + nums[idx]);
    }
    public static int rob(int[] nums) {
       return solve(nums.length - 1 , nums);
}

```

### 解法2 ：
```java
 public static  int []result;
   public static int sovle(int xid, int[] nums) {
        if (xid < 0) {
            return 0;
        }
        // 计算是否算过
        if (result[xid] >= 0) {
            return result[xid];
        }
        result[xid] = Math.max(sovle(xid - 2, nums) + nums[xid], sovle(xid - 1, nums));
        return result[xid];
    }
  public static int rob(int[] nums) {

        result = new int[nums.length];
        for (int i = 0; i < result.length; i++) {
            result[i] = -1;
        }

        return sovle(nums.length - 1, nums);
    }
```    

---
#小兵相前冲
---

### 题意
 N*M的棋盘，小兵要从左下角走到右上角，只能向上或者向右，问多少种走法。
 
### 思路
 * 两种走法 ：反过来思考
 * 2 * 3 的棋盘的走法 是通过 2 * 2 的棋盘的状态和 1 * 3 的棋盘共同推出的
 * 向右走 f（n）
 
### 解法
```java

    // 士兵一次性走一步
    public int f(int n, int m) {

        if (n == 0 || m == 0) {
            return 0;
        }
        // 条状的棋盘
        if (n == 1 || m == 1) {
            return 1;
        }
        return f(n - 1, m) + f(n, m - 1);
    }

    // 小兵在一个方向走一步或者两步， 走k 步呢？ ==》下楼梯问题
    public int f1(int n, int m) {

        if (n == 0 || m == 0) {
            return 0;
        }
        // 条状的棋盘
        if (n == 1 || m == 1) {
            return 1;
        }
        return f1(n - 1, m) + f(n, m - 1) + f1(n - 2, m) + f(n, m - 2);
    }

    // 某些格子小兵是禁止走，不需要改变代码，加0 就够了
    public int f2(int n, int m) {

        if (n == 0 || m == 0) {
            return 0;
        }
        // 条状的棋盘
        if (n == 1 || m == 1) {
            return 1;
        }
        return f2(n - 1, m) + f2(n, m - 1);
    }

    /**
     * 组合
     * 若表示在 n 个物品中选取 m 个物品，则如存在下述公式：C(n,m)=C(n,n-m)=C(n-1,m-1)+C(n-1,m)。
     * 从n个不同元素中，任取m(m≤n)个元素并成一组，叫做从n个不同元素中取出m个元素的一个组合；从n个不同元素中取出m(m≤n)个元素的所有组合的个数，叫做从n个不同元素中取出m个元素的组合数。
     *
     * @param n
     * @param r
     */
    int nCr(int n, int r) {
        if (n < r) {
            return 0;
        }
        if (r == 0) {
            System.out.println("==");
            return 0;
        }

        return nCr(n - 1, r - 1) + nCr(n - 1, r);
    }
```
 
# 下楼梯问题 Climbing Stairs

### 题意

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

**Example 1:**

Input: 2</br>
Output: 2</br>
Explanation: There are two ways to climb to the top.</br>
1. 1 step + 1 step</br>
2. 2 steps</br>

**Example 2:**

Input: 3 </br>
Output: 3</br>
Explanation: There are three ways to climb to the top.</br>
1. 1 step + 1 step + 1 step</br>
2. 1 step + 2 steps</br>
3. 2 steps + 1 step</br>

中文：你正在爬楼梯，需要n步骤才可以到达，每一次，你可以爬一步，或者两步，需要多少方式爬到顶

### 题解
```java
public static void main(String[] args) {
        System.out.println(jumpFloor(3));
    }
    /**
     * 递归
     * @param n
     * @return
     */
    public int climbStairs(int n) {

        if (n == 0) {
            return 0;
        }
        if (n == 1) {
            return 1;
        }
        if (n == 2) {
            return 2;
        }
        return climbStairs(n-1) + climbStairs(n-2);
    }

    // 一只青蛙一次可以跳上 1 级台阶，也可以跳上 2 级。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。
    public static int jumpFloor(int n) {

        if (n == 1) {
            return n;
        }
        if (n == 2)
            return n;
        int[] dp = new int[n+1];

        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i < n+1; i++) {
            dp[i] = dp[i - 2] + dp[i - 1];
        }
        return dp[n];
    }
```

# 01背包问题

### 题意

一个旅行者有一个最多能装m公斤的背包，现在有n中物品，每件的重量分别是W1、W2、……、Wn，每件物品的价值分别为C1、C2、……、Cn， 需要将物品放入背包中，要怎么样放才能保证背包中物品的总价值最大？





# CoinChange

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

**Example 1:**

Input: coins = [1, 2, 5], amount = 11
Output: 3 
Explanation: 11 = 5 + 5 + 1
**Example 2:**

Input: coins = [2], amount = 3
Output: -1


# 最长公共子序列
# Edit Distance
# 旅行商问题
---
##题意
一个商人要不重复的访问N个城市，允许从任意城市出发，在任意城市结束。现已知任意两个城市之间的道路长度

求城市的访问序列，使得商人走过的路程最短

如 ： N =4 ，访问 序列 3，4，1，2
NP问题，最优解