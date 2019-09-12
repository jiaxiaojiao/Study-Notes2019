## Java多线程编程

### 目录
- [一些基本概念](#一些基本概念)
- [线程、创建线程](#线程、创建线程)

### 一些基本概念

- 进程 Process
    
    程序运行实例。
	
	进程是程序向操作系统申请资源的基本单元。

- 线程 Thread

	线程是进程中 独立执行的最小单元。

	一个进程可用包含多个线程。同一个进程中的所有线程共享该进程中的资源。

- 任务

	线程要完成的计算被称为任务，特定的线程总是在执行着特定的任务。

	任务代表线程所要完成的工作。

- 多线程

	效率高。

- 多线程编程

	以线程为基本抽象单位的一种编程范式。

### 线程、创建线程

线程 java.lang.Thread

线程的创建：
1.	继承Thread，覆盖run方法并实现线程处理逻辑
2.	实现java.lang.Runnable接口
