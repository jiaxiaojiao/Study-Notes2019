# JDK1.8 新特性-函数式接口


## 函数式接口
> “函数式接口”是指仅仅只包含一个抽象方法的接口，每一个该类型的lambda表达式都会被匹配到这个抽象方法

> jdk1.8提供了一个@FunctionalInterface注解来定义函数式接口。

> 函数式接口可以对现有的函数友好地支持 lambda。

JDK 1.8 之前已有的函数式接口:
- java.lang.Runnable
- java.util.concurrent.Callable
- java.security.PrivilegedAction
- java.util.Comparator
- java.io.FileFilter
- java.nio.file.PathMatcher
- java.lang.reflect.InvocationHandler
- java.beans.PropertyChangeListener
- java.awt.event.ActionListener
- javax.swing.event.ChangeListener

JDK 1.8 新增加的函数接口：
- java.util.function