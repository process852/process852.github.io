# **Towards Accurate Multi-person Pose Estimation in the Wild**
作者提出了多人检测以及2D姿态估计框架，首先利用Faster RCNN检测人体位置框，然后估计每个Bounding Box中人的关节点位置。

## 引言
作者在本文工作中重新回顾了自顶向下的方法，以两阶段的方式实现多人姿态估计。第一阶段，首先预测包含人的Bounding Box的位置和尺度，第二阶段则针对每个检测到的Bounding Box进行关键点定位。除此之外，为了避免重复的关键点检测，提出了一个全新的**基于关键点非极大值算法**。