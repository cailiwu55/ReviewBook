## 1. abstract class和interface有什么区别？

abstract class抽象类：抽象类中可以有私有变量或者私有方法抽象类不能创建实例，抽象类的子类可以有选择的实现方法，但是可以创建一个抽象类的引用，指向具体的实现子类。一个类只能继承一个超类，

interface接口：接口是公开的，不能有私有变量或者私有方法，接口一定要实现所有方法，接口可以实现[多重继承](http://www.so.com/s?q=%E5%A4%9A%E9%87%8D%E7%BB%A7%E6%89%BF&ie=utf-8&src=wenda_link)，但可以通过继承多个接口实现多重继承，接口还有标识（里面没有任何方法，如[Remote](http://www.so.com/s?q=Remote&ie=utf-8&src=wenda_link)接口）和数据共享（里面的变量全是常量）的作用.。

一般的应用里，最顶级的是接口，然后是抽象类实现接口，最后才到具体类实现。

## 2. 抽象类中的方法是否可以同时是static，是否可以同时是native，是否可以同时是synchronized？

1. native：声明本地方法的关键字，它只有方法声明，没有方法实现，但是它将方法的具体实现交给了本地系统的函数库，没有通过虚拟机，这是java语言与其他语言通信的一种机制。很显然我们不能对一个抽象类中的方法既声明为abstract又声明为native。（但是如果在抽象类中利用本地实现该方法如何？）

2. static：声明静态方法的关键字，首先需要注意的是类其实也是一个对象，抽象类不能产生实例对象，但是类加载机制必然会为一个抽象类产生一个class对象，所以在抽象类中可以定义static方法，因为static方法依赖的是class对象，所以在抽象类中可以定义一个static方法，但是static方法不能被重写，所以我们需要在抽象类中完成静态方法的实现，而且使用AbstractClass.staticMethod\(\)调用。（但这样子有什么意义？）

3. synchronized：声明同步方法的关键字，这个关键字有两种用法，synchronized方法和synchronized块，但是无论synchronized关键字加在方法上还是对象上，它取得的锁都是对象，而不是把一段代码或函数当作锁，而且每个对象只有一个锁（lock）与之相关联，同时实现同步是要很大的系统开销作为代价的，甚至可能造成死锁，所以尽量避免无谓的同步控制。从synchronized的原理中我们可以得出synchronized依赖的是对象，那么抽象类有一个class对象，所以我们也可以在抽象类中定义同步方法，有趣的是，当我们定义了同步方法，只能在子类中重写他，但是还需要在抽象类中具有方法体，如果我们将同步方法同时声明为static的，那么就可以直接利用抽象类调用它。

   [synchronized原理](http://www.cnblogs.com/paddix/p/5367116.html)

   [抽象类中到底可以不可以定义static？博客](http://blog.csdn.net/zq602316498/article/details/39431265)


