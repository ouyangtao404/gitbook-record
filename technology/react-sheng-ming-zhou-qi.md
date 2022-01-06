---
description: https://zhuanlan.zhihu.com/p/60168527
---

# React 生命周期

### 最初(16.3版本)

![](<../.gitbook/assets/image (5).png>)

![](<../.gitbook/assets/image (12).png>)

* 基础  &#x20;
  * 构造函数   &#x20;
  * render
* &#x20;流程   &#x20;
  * 初始化
  * 加载（will\did）   &#x20;
  * 更新（should\will\did）       &#x20;
    * state变化触发的更新
    * 由props变化触发的更新
  * 卸载（will）
*   理解补充：  &#x20;

    * &#x20;需要理解几个流程的具体发生过程
    * 理解适合执行setState的钩子（加载前后、更新后、接props）
    * 强制更新  forceUpdate()



### 版本16.4之后   &#x20;

![](<../.gitbook/assets/image (3).png>)

* 移除了加载will\接受props\更新will   &#x20;
* 增加了    ​   &#x20;
  * getDerivedStateFromProps  字面意思是从props获得新的state，创建和更新都会触发钩子
  * ​​getSnapshotBeforeUpdate   更新前（能读到更新前的props\state快照）    #16.8&#x20;

### React Hooks​

另起一篇专门总结    ​\
\
\
\
\
\
\
\
\
\
\
