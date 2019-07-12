## fish-redux学习系列1
  
#### 主要特点 -- 分治和组合
fish-redux中提倡分治和组合；分治是值分而治之如：view层和数据层的拆分，reducer和effect和action的出现；组合是指最后state,view,effect,reducer,dependencies,middleware的组合。组合和分治的好处是页面结构细分，数据层,view层的分离，利用后续维护扩展和协同开发；

#### 主要思想 -- 基于redux做数据管理
fish-redux是基于redux做的数据管理。大致就是和redux一样，区别在reducer的合并上，fish-redux直接做掉了。将数据统一维护在store中，如需修改提高修改的门槛，dispatch相应的action到reducer中做state的修改。

#### 主要架构图
![fish-redux架构](/assets/fish-redux1.jpg)

#### 各部分详细描述
![fish-redux各部分描述](/assets/fish-redux2.jpg)


#### 创新之举 -- Adapter
做局部显示，抽象了adapter来做性能的优化，类似于listview的场景，一个list，对应着一个list-adapter，里面做item组件和数据的拼装，实现在上层做模型抽象。Adapter有三种实现。

- DynamicFlowAdapter
- StaticFlowAdapter
- CustomAdapter




  	