# Dynamic Programming

* 有些能用动态规划求解但是超时的题目，可以考虑二分法。
* 当看到数据范围极小的时候要考虑用位二进制存储状态，或者考虑暴力求解。



## 背包问题
多重背包，多重背包可以转化为完全背包和01背包。如果某东西的总体积大于包体积，则可以当成是完全背包。否则按物品体积的1，2，4...倍分别进行01背包。这样就相当于构成了所有的可能情况，例如5 ＝ 4 ＋ 1， 7 ＝ 1 ＋ 2 ＋ 4。都可以由这些数字构成。

（下面这种方法仅适用于BOOL型的背包，即weight和value相等的情况）多重背包，学了

学了种很快的新方法，就是每次填f[j]时直接由f[j-weight[i]]推出，前提是num[j - weight[i]] < sum[i]

num每填一行都要清零，num[j]表示当前物品填充j大小的包需要至少使用多少个

但是使用这种方法有一个条件，就是要求f数组只能是bool类型。否则会出错。

对于bool型则不会有性价比的问题，只有体积可达和不可达的问题，在可达前提下只要尽量少的使用当前物品即可，value型则不行，可达不一定少用当前物品，因为多用当前物品可能会获得高价值。

例如，如果当前物品性价比极高，那么对于任意大小的包都应该尽量多的当前物品以追求高价值，用上述方法会使得后面包容量足够大时，会有些位置（j=(sum[i]+1) * weight[i]）因无法满足条件num[j - weight[i]] < sum[i]（即之前已经把当前物品买完），而无法购买当前物品。

## 树形DP
树状dp，一般采用左儿子右兄弟的存储方式，利用记忆化搜索，对树进行从下到上，对子树链进行从右到左的填写。也可以使用存储图的方式存储，然后便利一个节点的所有子节点，在便利过程中不断积累更新父节点的值。

## 概率DP
概率DP求期望：
我们以前学过的求期望的方法是每种结果出现的概率乘以每种结果的值，然后相加。但是通常解决这类问题我们都要对每个中间状态求期望值，最终算出总的期望。这时我们就可以把每个状态的后继状态（子问题）看成是一个结果值，而不是期望值。

如果是算期望通常需要逆向思维E(u)=sigma(pv * E(v)+C)，其中C是状态u和状态v之间的期望差值，pv是u状态转移到v状态的概率。v是u拆分后的子问题。

注意：sigma(pv)=1

在概率dp中有时候我们要求解的f[i][j]可能会同时出现在我们列出的转移方程的两侧，这时候需要解方程，将其统一到方程等号的一边来。

概率DP中求概率通常需要正向思维，由情况i出发到达情况v。那么用如下公式更新所有的情况v，P(v)+=P(i) * P(v|i)。注意：对于一个固定的i，所有到不同的v的概率总和sigma(P(v|i))=1。

动态规划中状态维和值是可以相互转化的。状态维过多，效率低的时候，可以把将其转化为数组值；同理，数组值不唯一无法规划时，可以增加状态维使状态更详细。
