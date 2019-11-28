[toc]

最近在看Java编程思想中发现自己对Java多态的理解并不到位，总结一下对Java多态的理解

首先看以下代码：

**父类Animal**

```java
class Animal {
    int num = 10;
    static int age = 20;

    public void eat() {
        System.out.println("动物吃饭");
    }

    public static void sleep() {
        System.out.println("动物在睡觉");
    }

    public void run() {
        System.out.println("动物在奔跑");
    }
}
```

**子类Cat**

```java
class Cat extends Animal {
    int num = 80;
    static int age = 90;
    String name = "tomCat";

    public void eat() {
        System.out.println("猫吃饭");
    }

    public static void sleep() {
        System.out.println("猫在睡觉");
    }

    public void catchMouse() {
        System.out.println("猫在抓老鼠");
    }
}
```

**测试类Polymorphism**

```java
public class Polymorphism {
    public static void main(String[] args) {
        Animal am = new Cat();
        am.eat();   
        am.sleep(); 
        am.run();   
//        am.catchMouse();
//        System.out.println(am.name);
        System.out.println(am.num);  
        System.out.println(am.age); 
    }
}
```

#### 实现Java多态的前提

- 存在继承关系：Cat类继承了父类Animal类
- 子类要重写父类的方法：Cat类重写了Animal的两个成员方法eat()和sleep()。前者是非静态的，后者是静态的。
- 父类数据类型的引用指向子类对象：Animal am = new Cat()，语句在堆内存中开辟了子类Cat的对象，并把栈内存中的父类引用指向了这个对象

输出结果

```java
猫吃饭
动物在睡觉
动物在奔跑
10
20
```

#### 总结多态成员访问的特点

- 成员变量：编译看父类，运行看父类
- 成员方法：编译看父类，运行看子类。动态绑定
- 静态方法：编译看父类，运行看父类

#### 多态的弊端

> **不能使用子类特有的成员属性和子类特有的成员方法。**

上个例子中如果执行am.catchMouse();System.out.println(am.name);就会报错。

原因及解决：将父类引用指向了子类对象的am强制变回Cat类型。这样am就是Cat类型的引用，指向的就是Cat对象了，自然可以使用Cat类的一切属性和一切成员方法。

```java
Cat cat  = (Cat)am;
cat.eat();   
cat.sleep();  
cat.run(); 
cat.catchMouse();  
```

输出结果

```
猫吃饭
猫在睡觉
动物在奔跑
猫在抓老鼠
```

很明显，执行完强制语句后，cat就指向最开始在堆内存中创建的那个Cat类型的对象了。

#### 向上转型

向上转型就是 Animal am = new Cat() 语句，从小范围转向了大范围，Animal父类数据类型的引用am指向子类Cat对象，类似于从小范围的int转向大范围的double而不会损失精度。

#### 向下转型

向下转型是还原的工作，上例中就是强制转成Cat类型的动作，使用Cat类的一切属性和一切成员方法。

