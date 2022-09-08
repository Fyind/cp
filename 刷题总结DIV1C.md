---
title: 刷题总结DIV1C
date: 2021-10-30 22:10:14
tags:
---
# 知识点

## 枚举

### cnt枚举2个量

在一个数组中,  $cnt[x]$ 代表 $x$ 出现的次数
$$
\sum_x cnt[x] \le n
$$
于是可以枚举所有 $x$ 在枚举所有小于 $cnt[x]$ 的数，总复杂度不超过 $O(n)$

> CF1637E(2100)

### 枚举 $2^k$ 

长度是 $2^k$ 那么直接枚举 $k$ 即可

> CF1626D(2100)



## 二分

同时检查多个参数:

用二进制表示，0表示不符合，1表示符合，放到一个集合里，再枚举集合

> [ zone2021_c ](https://vjudge.net/problem/AtCoder-zone2021_c/origin)

对 $x_i $找下一个不超过$L$ 的点，可以用lowerbound查询

### 倍增dp

> [arc060_c ](https://vjudge.net/problem/AtCoder-arc060_c/origin)



## 整体二分

> CF1601C

## 并查集

对于两者选1的问题，用边建图，然后分析。

> [arc111_b ](https://vjudge.net/problem/AtCoder-arc111_b/origin)

数据结构，小的向大的合成可以降低复杂度

> [abc183_f ](https://vjudge.net/problem/AtCoder-abc183_f/origin)

## 神奇构造

拆分再组合

> [agc055_a ](https://vjudge.net/problem/AtCoder-agc055_a/origin)

构造部分解，然后组合成最终解

循环构造

> [agc056_a ](https://vjudge.net/problem/AtCoder-agc056_a/origin)

#### 三角形数

$1+2+..+k$ 的和

Fermat polygonal number theorem：

任意正整数可以拆分成不超过3个三角形数的和

扩展：

不超过7个三角形数，如果连续按最近的三角形数拆分 (验证正确 <= 1e8) 

> [arc129_c ](https://vjudge.net/problem/AtCoder-arc129_c/origin)







## 数学

### 个数限制

在 

$$
\left \lfloor \frac{m}{1} \right \rfloor+\left \lfloor \frac{m}{2} \right \rfloor+...+\left \lfloor \frac{m}{m} \right \rfloor \le O(mlog(m))
$$

> CF1657D

中，最多有 
$$
2\sqrt{m}
$$

 个不同的数

证明：

考虑 $m/k$

* $k>\sqrt{m}$ ，

  $$
  \frac{m}{k} < \frac{m}{\sqrt{m}} = \sqrt{m}
  $$

  最多不超过 $\sqrt{m}$ 个
* $k \le \sqrt{m}$, 设 $t = \lfloor \frac{m}{k} \rfloor$ , 显然 $t\ge k$

  $$
  \left \lfloor \frac{m}{\lfloor \frac{m}{k} \rfloor} \right \rfloor = k
  $$

  成立

  证明：

  $$
  kt \le m < k(t+1) = kt+k \le kt+t = k(t+1)  \\
  kt \le m < t(k+1) \\
  \left \lfloor \frac{m}{\lfloor \frac{m}{k} \rfloor} \right \rfloor = k
  $$

  一共不超过 $\sqrt{m}$ 个

> CF1603C

### 取模公式

$$
a \bmod b = a-b\cdot \lfloor \frac {a}{b} \rfloor
$$

> CF1553F

### 整除公式

$$
\begin{aligned}
\lfloor \frac{a}{b} \rfloor&=0 , a\in [0,b) \\
\lfloor \frac{a}{b} \rfloor&=1 , a\in [b,2b) \\
... \\
\lfloor \frac{a}{b} \rfloor&=k , a\in [kb,(k+1)\cdot b) \\
\end{aligned}
$$

可以考虑贡献

> CF1553F

平均分配 $A_i$ 到 $k$ 个数上
$$
\sum_{j=1} ^{k} \lfloor \frac{A_i+j-1}{k} \rfloor = A_i
$$

> [agc053_a ](https://vjudge.net/problem/AtCoder-agc053_a/origin)

### 因子个数上界

X的因子个数约为(近似值)
$$
O(X^{\frac{1}{3}})
$$

> [arc124_c ](https://vjudge.net/problem/AtCoder-arc124_c/origin)

### 组合数学

考虑最大的数，然后隔板法

> [arc116_c ](https://vjudge.net/problem/AtCoder-arc116_c/origin)

### 容斥原理

需要用容斥原理的计数dp

> [agc046_b ](https://vjudge.net/problem/AtCoder-agc046_b/origin)



## 卢卡斯定理

https://brilliant.org/wiki/lucas-theorem/#proof-of-the-theorem

> CF1673B(2500)



## 图论

### 完全图

欧拉路径构造

![image-20211101223826968](刷题总结DIV1C/image-20211101223826968.png)

> https://codeforces.com/gym/103329/problem/D

### 最短路

#### 01BFS

0的边权放在队列头，1的边权放在队列尾

> [abc213_e ](https://vjudge.net/problem/AtCoder-abc213_e/origin)

#### Dijkstra

势能法处理负权

> ABC237E



## 博弈论

### 状态转移dp

有2种选择，A会最大化结果，B会最小化结果。 A选择一个值，B减去这个值或加上这个值
$$
max_{x} \left( min(f_1+x,f_2-x) \right)
$$
$f_1,f_2$ 已知, $x \in [0,k]$ . 把 $f_1+x,f_2-x$ 看成2个一次函数，那么最小值就是区下面的部分。再取最大值就是他们的交点
$$
x = \frac{f_2-f_1}{2}
$$
这个时候
$$
y = f_1 + x = f_1+ \frac{f_2-f_1}{2} = \frac{f_1+f_2}{2}
$$
可以证明 $x$ 不会越出 $[0,k]$ 因为 $x(n,m) = \frac{x(n-1,m)+x(n-1,m-1)}{2} \le k$ 所有不用考虑取模问题

> CF1628D1(2100)

轮到A时候最大化A-B的分数，轮到B的时候最小化A-B的分数。然后可以dp这个A-B

> [abc201_d ](https://vjudge.net/problem/AtCoder-abc201_d/origin)



## 动态规划

### 计数dp

找规律发现很多数字相同。把相同的数字分组，然后对组的和进行dp

> ABC232E

### 二维dp

枚举两个端点的复杂度过大，可以考虑从一个点走到另一个点的dp

> ABC210D



考虑一条路径，把空的块作为参数，然后就可以计算dp. 计算的时候，化简，然后把参数乘到dp里面去

> [keyence2021_c ](https://vjudge.net/problem/AtCoder-keyence2021_c/origin)



### 区间dp

考虑贡献，别绕进去

> cf1666j

## 字符串

结论

$a^{inf} < b^{inf} \Leftrightarrow a+b<b+a $

可以用扩展KMP计算



### 回文数

一个长度为 $n$ 回文数由前 $\lceil \frac{n}{2}\rceil $ 个字符决定。因此可以将问题简化为考虑前  $\lceil \frac{n}{2}\rceil $ 个字符

> ABC242E(1200)



### 个数统计

* 已知 $S$ ，且$S,T$ 全是大写字母，统计 $T\le S$ 的字符串个数。

可以用树状图画出统计路线

``` cpp
ll ans = 0;
for (int i = 1;i <= (n+1)/2; ++i) {
    ans = mul(ans, 26);
    ans = add(ans, s[i] - 'A');
}
```



### 数位dp

最优子结构的理解：

> 找出 $\le x$ 的个数

答案就是 $x+1$ , 然后我们用数位dp的思想来考虑这件事。

假设 $x=5674$ 

把 $x$ 存在数组 $A$ 里面，要**倒着存** (不使用0号位)

```
A = {4, 7, 6, 5}
```

设 $dp(pos,limit)$ 为：构造长度为 $pos$ 的数字，且之前是否沿着 $x$ 的边界构造。
$$
\begin{align*}
dp(pos,1) &= dp(pos-1,1) + (A[pos]-1)*dp(pos-1,i-1) \\
dp(pos,0) &= 9*dp(pos-1,0)
\end{align*}
$$
如果沿着边界构造(limit = 1)，那么下一位只能选择不超过 $x$ 的下一位的数也就是 $[0,A[pos]]$

如果limit = 0, 那么下一位以及后面的所有位都可以选 $[0,9]$ 中的数字

性质：limit=1 的状态只有 $len(A)$ 个，如果还有其余状态也要乘上

也就是只有沿着 $x$ 构造才会出现 limit = 1，而且如果 limit = 1，那么之前所有的limit必定为1

所以可以省略limit这个参数，让limit=1的情况不用记忆化

如果只需要构造位数与 $x$ 相同的数字，只需要判断一下在第一次的时候从 $1$ 开始就可以了

``` cpp
int mxnum = limit ? A[k] : 9;    
for (int i = (pos==n);i <= mxnum; ++i) {
   // 代码
} 
```

对于 $x \le 0$ 的情况要特判，不然转换数字会出错

对于 $x$ 的位数很大的情况，要使用字符串进行输入



对于要求最大最小值的问题，那么就要用两个边界来dp

``` cpp
ll tl = l;
int tota = 0;
while (tl) {
    A[++tota] = tl % 10;
    tl /= 10;
}
ll tr = r;
int totb = 0;
while (tr) {
    B[++totb] = tr % 10;
    tr /= 10;
}
int tot = max(tota, totb);

pair<ll,ll> dfs(int pos, int l1, int l2) {
    if (pos == 0 || (l1 == 0 && l2 == 0)) {
        // 边界
    }

    auto &cur = dp[pos][l1][l2];
    if (cur.first != -1) return dp[pos][l1][l2];
    cur = {-1,0};

    int down = l1 ? A[pos] : 0;
    int up = l2 ? B[pos] : 9;
    for (int i = down;i <= up; ++i) {
        // ...
    }

    return cur;
}
```







## 数组排序问题

### 考虑逆序对个数的奇偶性

某操作不影响逆序对个数的奇偶性。多重数字，可以构造出合适的奇偶性。

> ARC136B(1200)





### 多元方程组

设参数，是的方程组有唯一解。然后分析参数的限制。

> ARC135B(1200)



## 解析几何

仿射变换

> [abc189_e ](https://vjudge.net/problem/AtCoder-abc189_e/origin)



# 思维点

### 统计所有子数组的答案和

考虑贡献：有多少个不同的答案，每个答案有多少贡献

> CF1603C



### 用子问题拆解，然后dp

只要定义好状态，可以简化很多代码。

> ABC242D(1200)

# 编码细节

能用vector用vector

``` cpp
void run_case() {
    cin >> n >> m;
    vector<int> A(n+1);
    map<int,int> cnt;
    vector<vector<int>> nodes(n);
    vector<pair<int, int>> bad_pairs;
    for (int i = 1;i <= n; ++i) {
        cin >> A[i];
        cnt[A[i]]++;
    }
    for (auto [x,cntx] : cnt) {
        nodes[cntx].push_back(x);
    }
    for (auto& v : nodes) {
        reverse(v.begin(),v.end());
    }
    
    for (int i = 1;i <= m; ++i) {
        int x, y;
        cin >> x >> y;
        bad_pairs.push_back({x,y});
        bad_pairs.push_back({y,x});
    }
    sort(bad_pairs.begin(), bad_pairs.end());
    for (auto& v : nodes) {
        sort(v.begin(), v.end(), greater<>());
    }
    ll ans = 0;
    for (int cntx = 1; cntx < n; ++cntx) {
        for (auto x : nodes[cntx]) {
            for (int cnty = 1;cnty <= cntx; ++cnty) {
                for (auto y : nodes[cnty]) if (x != y && !binary_search(bad_pairs.begin(), bad_pairs.end(), pair<int, int>{x, y})) {
                    
                    ans = max(ans, 1ll*(cnt[x]+cnty)*(x+y));
                    break;
                    
                }
            }
        }
    }
    cout << ans << '\n';
}

```



