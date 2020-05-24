### Subtext of today's lecture
#### steps to developing a usable algorithm
- Model the problem
- Find an algorithm to solve it
- Fst enough? Fits in the memory?
- if not, figure out why
- Iterate until satisfied

#### 本书的妙处
- 实验 ： 失败 ： 再实验
- 数学是保证 ， 数据是验证
- **所有的算法都是现有API，再有实现，之后验证，最后数据** 
- 先接口，后实现，强调测试的做法，是在工作中摸爬滚打多年的。

#### 本书的不足
- 没有动态规划！！！


#### Union Find （名词解释 & 单词）
- equivalence 相近的，等价的
- quadratic 二次，平方 ， don't scale with technology
- **Lazy Approach**  : Alternative called "Lazy approach algo design", that we try to avoid doing things until we have to. 
- brute force algorithm , 暴力破解算法是quadratic 的，没有任何的可扩展性。

#### Union ： Quick Find

#### Union ： Quick Union

#### Union ： Quick Union Improvement
1. weighting, 我们在用Tree的时候，一定要避免skinny tall tree. 因为这种情况下会退化成N的时间复杂度。 **保证：link smaller tree to Larger tree** , 最后的结果的是：no item is too far away from the root.
用了Weighting Tree 后，时间复杂度从N减到了近似的logN，这个是非常非常有效的缩减。
其空间的代价仅仅是增加了一个用来计算Size的数组。
**用空间来换时间**
logN 的复杂度是可以Scale的，如果从Million数量级到Billion，时间会从20S到30S

2. 以上的优化已经够好了， Stop？ NO！easy to improve even further!!!
** Path Compression ** 路径压缩
```java
# 只要加一句
while (i !=id[i])
{
    id[i] = id[id[i]];  # <--
    i = id[i];
}
```
**以上的一句话，直接把logN -> log*N** 1 - 0 ， 2 - 1 ， 4 - 2 ， 16 - 3 ， 65536 - 4 ， 2**65535 - 5 ， 无敌！
**这就是Weighted quick-union with path compression的力量!**

- WQUPC (weighted quick union (with pasth compression)) reduces time from 30 years to 6 secs.
- Supercomputer won't help much; good algorithm enables solution
- WQUPC make possible to solve problems that could not otherwise be addressed

#### Union Find Applications
- percolation model, 渗透模型，有很多应用，比如导电与绝缘，水流与隔断
- 蒙特卡洛算法来算 系数p （percolation probability）, 可以算出来 ~ 0.592746
- N * N 的矩阵，可以想象成有虚拟上root和下root的树，