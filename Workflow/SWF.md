# SWF

- 工作流引擎，不如说是分布式计算调度框架。

- 只包括Task和History两部分，甚至是每个Task之间如果要传递一些数据的话，都只能通过第三方存储（比如Message Queue或者Redis）

- 一个Workflow不能太复杂。