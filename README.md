# <center> NEC_Robot <center>
---

1. 机器人基础知识  
    * 多刚体机械臂空间描述及运动学分析： 参考附件[机器人学导论](./机器人学导论.pdf)前4章。
    * 

2. 机器人逆运动学求解
    * 利用Matlab Robotics Toolbox对机器人进行建模并求解
      * 获取[Matlab](https://ww2.mathworks.cn/products/get-matlab.html?s_tid=gn_getml)
      * 安装[Robotics System Toolbox](http://petercorke.com/wordpress/toolboxes/robotics-toolbox)
      * 使用说明参考[Manipulator Algorithm](https://ww2.mathworks.cn/help/robotics/manipulators.html)
      * 我的建模方法：
      > 1. robotics.RigidBodyTree创建机器人身体主体
      > 2. robotics.subTree创建机器人身体分支，可以考虑将身体分为六个subTree: 左右手、左右脚、躯干、头。
      > 3. 创建每个关节相应的robotics.RigidBody和robotics.Joint，再通过addSubTree将每个分支添加到robotics.RigidBodyTree上，完成机器人的初步建模
      > 4. 为进一步完成建模，需要添加参数以约束机器人各构件的运动。Matlab中常采用的方法有：利用DH参数或改进DH参数定义机器人各连杆及关节角的空间关系。这种方法非常简单，如果机器人设计者能提供DH参数，可以非常方便的完成机器人建模并求解。如果没有DH参数，还可以通过在实例化robotics.Joint时，定义Joint Object的jointToParent, childToJoint, setFixedTransform, PositionLimit等属性，约束关节的转动轴、转动方向及转动范围。
      * 逆运动学求解，参考Matlab的[Inverse Kinematics](https://ww2.mathworks.cn/help/robotics/ref/robotics.inversekinematics-system-object.html)以及[Generalized Inverse Kinematics](https://ww2.mathworks.cn/help/robotics/ref/robotics.generalizedinversekinematics-system-object.html)
    * Matlab Robotics System Toolbox工具箱的源码托管于[Matlab Source Code](https://github.com/petercorke/robotics-toolbox-matlab)以及其Python版本托管于[Python Source Code](https://github.com/adityadua24/robopy), 参考源码时需要注意的几个点：
    > 1. 尽管源码开源，但有商业使用限制，参照源码时需要根据相应的License对源码进行Refactor。
    > 2. Python版本的源码中，对空间矢量的描述采用的是相比向量Vector而言更加通用的旋量Screw，如需理解源码，请参考[为什么要使用旋量](https://zhuanlan.zhihu.com/p/33156814)，以及附件[Modern Robotics](./Modern_Robotics.pdf)的第六章。
