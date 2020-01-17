---
description: 'https://zhuanlan.zhihu.com/p/60168527'
---

# React 生命周期

### 最初\(16.3版本\)

![](../.gitbook/assets/image%20%285%29.png)

![](../.gitbook/assets/image%20%287%29.png)

* 基础   
  * 构造函数    
  * render
*  流程    
  * 初始化
  * 加载（will\did）    
  * 更新（should\will\did）        
    * state变化触发的更新
    * 由props变化触发的更新
  * 卸载（will）
* 理解补充：   

  *  需要理解几个流程的具体发生过程
  * 理解适合执行setState的钩子（加载前后、更新后、接props）
  * 强制更新  forceUpdate\(\)

### 版本16.4之后    

![](../.gitbook/assets/image%20%283%29.png)

* 移除了加载will\接受props\更新will    
* 增加了    ​    
  * getDerivedStateFromProps  字面意思是从props获得新的state，创建和更新都会触发钩子
  * ​​getSnapshotBeforeUpdate   更新前（能读到更新前的props\state快照）    \#16.8 

### React Hooks​

另起一篇专门总结    ​  
  
  
  
  
  
  
  
  
  
  


