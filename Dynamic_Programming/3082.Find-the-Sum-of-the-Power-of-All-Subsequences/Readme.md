### 3082.Find-the-Sum-of-the-Power-of-All-Subsequences

“子序列的子序列”思考起来比较费劲，但是如果只是求“和为k的子序列的个数”，这个看上去就是典型的DP。然后我们再思考一下，本题其实就是求每个“和为k的子序列”有多少个超序列（super sequence）。

举个列子，假设总元素个数是n。如果有一个子序列q的长度是m，它的和是k，那么nums里就有`(n-m)^2`个序列包含q，这些序列的都有这么一个子序列q满足条件，所以q本质上给最终答案贡献了`(n-m)^2`。

所以我们只需要求出所有不同长度的、和为k的子序列个数。这个只不过在前述DP的基础上，再增加一个变量/下标记录已经选取元素的个数。即令dp[i][s][j]表示在前i个元素里、选取j个元素、和为s的子序列有多少个。显然它的转移方程就取决于第i个元素是否选取：
```cpp
dp[i][s][j] += dp[i-1][s][j];  // no select nums[i]
dp[i][s][j] += dp[i-1][s-nums[i]][j-1], if (s>=nums[i] && j>=1);  // select nums[i]
```
最终考察完整个nums之后，我们遍历子序列的长度j，就可以知道存在有dp[n][k][j]个符合要求的子序列，并且其长度是j。那么它的超序列就有`(n-j)^2`个。
