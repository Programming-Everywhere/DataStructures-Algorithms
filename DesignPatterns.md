<!-- GFM-TOC -->
* [一、概述](#一概述)
* [二、创建型](#二创建型)
    * [1. 单例（Singleton）](#1-单例singleton)
    * [2. 简单工厂（Simple Factory）](#2-简单工厂simple-factory)
    * [3. 工厂方法（Factory Method）](#3-工厂方法factory-method)
    * [4. 抽象工厂（Abstract Factory）](#4-抽象工厂abstract-factory)
    * [5. 生成器（Builder）](#5-生成器builder)
    * [6. 原型模式（Prototype）](#6-原型模式prototype)
* [三、行为型](#三行为型)
    * [1. 责任链（Chain Of Responsibility）](#1-责任链chain-of-responsibility)
    * [2. 命令（Command）](#2-命令command)
    * [3. 解释器（Interpreter）](#3-解释器interpreter)
    * [4. 迭代器（Iterator）](#4-迭代器iterator)
    * [5. 中介者（Mediator）](#5-中介者mediator)
    * [6. 备忘录（Memento）](#6-备忘录memento)
    * [7. 观察者（Observer）](#7-观察者observer)
    * [8. 状态（State）](#8-状态state)
    * [9. 策略（Strategy）](#9-策略strategy)
    * [10. 模板方法（Template Method）](#10-模板方法template-method)
    * [11. 访问者（Visitor）](#11-访问者visitor)
    * [12. 空对象（Null）](#12-空对象null)
* [四、结构型](#四结构型)
    * [1. 适配器（Adapter）](#1-适配器adapter)
    * [2. 桥接（Bridge）](#2-桥接bridge)
    * [3. 组合（Composite）](#3-组合composite)
    * [4. 装饰（Decorator）](#4-装饰decorator)
    * [5. 外观（Facade）](#5-外观facade)
    * [6. 享元（Flyweight）](#6-享元flyweight)
    * [7. 代理（Proxy）](#7-代理proxy)
* [参考资料](#参考资料)
<!-- GFM-TOC -->

# 一，概述
设计模式（design pattern）是解决问题的方法，学习现有的设计模式可以做到经验复用。

# 二，创建型
## 1. Singleton
### Intent
one lcass has one instance, support htis instance the global asscess point.
### Class Diagram 
使用一个私有构造函数、一个私有静态变量以及一个公有静态函数来实现。

私有构造函数保证了不能通过构造函数来创建对象实例，只能通过公有静态函数返回唯一的私有静态变量。

## 2. Simple Factory 
### Intent 
Create a object without showing the details, but also provide a object creation interface. 
### Class Diagram
![Screen Shot 2020-09-09 at 9 39 45 AM](https://user-images.githubusercontent.com/19642027/92605998-6dcb5800-f280-11ea-9764-1c0f385d452b.png)

1. Simple factory takes Instantiated Operation into a single class. 
2. Simple factory will decide which sub class to do instatition. 
3. Clients won't know the details of the sub class, and when change sub class, the client don't have to change. 
```java
class SimpleFactory {
   public Product createProduct(int type) {
       if(type == 1) return new ConcreateProduct1();
       else if(type == 2) return new ConcreateProduct2();
       return new ConcreateProduct();
   }
}
```
```java
# any clinets need instantiate use SimpleFactory()
public class Client {
   public static void main(String[] args) {
      SimpleFactory simpleFactory = new SimpleFactory();
      Product product = simpleFactory.createProduct(1);
   }
}
```
