# Game Theory

## NP问题
NP问题，必胜态N（next player wins）,必败态P(previous player wins)

如果某状态的直接后继中有必败态那么它一定是必胜态，否则为必败态。

## SG函数
设函数g(x)。我们先把所有的最终局面（最终局面均为必败P局面）g(x)赋值为0。然后所有其他局面g(x)等于其直接后继状态中没有出现过的最小自然数。这样一来所有是g(x)＝0的状态就是必败态，其他为必胜态。

根据定理：有这样一个游戏，是多个游戏共同进行，每个游戏都执行到底时才算整个游戏结束，每次一个选手可以把一个游戏进行一步。对于这样的游戏它的某状态的g(x)值，为每个子游戏的现在所处的状态的g(x)值抑或起来的结果。
