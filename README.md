q学习算法用于静态未知环境的移动机器人的路径规划算法，是可行的，但是该方法有很大的缺点，首先数据处理能力不足，需要用表格存储q值，如果当状态很多，得到的q值很多，这就需要很大的内存来存储，占据很大的计算机内存资源，值查询也会很慢，造成效率低下，于是产生了深度强化学习DQN，用神经网络来拟合值函数，状态当作输入，输出为状态值函数，再根据值函数选择动作。
但是DQN也有缺点，更新神经网络参数时，计算TD目标的动作值函数所用的网络参数θ与梯度计算中要逼近的值函数所用的网络参数相同，这样就容易导致数据间存在关联性，从而使得训练不稳定，用来训练神经网络很难收敛；于是有人加入经验回放（记忆库）来打破这种相关性，使神经网络能够稳定收敛。虽然解决了数据相关的问题，但是DQN无法解决过估计的问题。过估计是指估计的值函数比真实的值函数偏大，如果过估计在所有状态都是均匀的，那么根据贪心策略，依然能够找到值函数最大的动作，但是往往过估计在各个状态不是均匀的，因此过估计会影响到策略决策，从而导致获取的不是最优策略。
所以就有人提出DDQN解决过估计的问题，其核心思想是将TD目标的动作选择和TD目标的动作评估分别用不用的值函数来实现，改进max动作选择操作，解决过估计问题，还使用优先经验回放改进经验回放，因为普通经验回放时，利用均匀采样并不是高效利用数据的方式，因为智能体经历过的所有数据对于智能体的学习并非具有同等重要的意义。智能体在某个状态的学习效率可能比其余状态要高，优先回放打破了均匀采样，赋予学习效率高的状态更大的采样权重。

