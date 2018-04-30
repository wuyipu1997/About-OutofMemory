# 1.	内存泄漏和内存溢出的区别 #
  a)	内存的泄漏指的是分配的对象可达但不可用。

  b)	内存的溢出是指程序运行过程中，无法申请到足够的内存而导致的一种错误。

# 2.	内存泄漏的集中场景 #
a)	长生命周期的对象持有短生命周期对象的引用。

b)	修改hashset对象中参数值，并且参数是参与计算hash的字段。

c)	机器连接数和关闭时间设置。

# 3.	内存溢出的一种场景 #
a)	Java.lang.OutOfMemoryError.

b)	Java.lang.OutOfMemoryError.  在JVM启动的时候就加载了

c)	Java.lang.OutOfMemoryError. 这个类实际上是没法去Agent（代理拦截）的，因为JVM启动时类就已经被加载到内存中了。

1.	堆内存溢出（java.lang.OutOfMemoryError:java.heap space）
在Map中疯狂塞值，也不对map进行清理，会出现内存泄漏，最后内存溢出。

2.	方法区内存溢出（java.lang.OutOfMemoryError:PermGen space ）
将strings定义成静态的,将方法区改小，疯狂创建静态数组，会报错。
但是JDK1.8中不会出现方法区溢出，因为1.8中使用Meta space，使
用的是本地内存，-xx:PermSize=2m 和 -xx:MaxPermSize=2m 参数将无效
因此在使用cglib或者反射生成类时要特别注意，因为方法区中包含class文件

3.	JAVA线程栈的溢出（java.lang.StackOverflowError ）
递归太深或方法调用层级过多（无限递归，没有返回值）

# 4.	如何分析内存溢出 #

a)	对于heap，需要dump 堆。

# 5.	如何避免内存溢出 #

a)	今早释放无用对象的引用。

b)	处理字符串的时候，应避免使用String，推荐使用StringBuffer，每一个String对象都会独占一块内存空间。

c)	尽量少用静态变量，静态变量是存在永久代，而永久代不参与我们的垃圾回收。

d)	避免在for循环中去创建对象。

e)	开启大型文件或者从数据库里面一次读，预估你数据量，并且要设定一个最大值，合理利用空间，给出提示。
