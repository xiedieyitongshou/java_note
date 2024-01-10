## Java笔记

### 1.continue、break 和 return 的区别是什么？

1. `continue`：指跳出当前的这一次循环，继续下一次循环。
2. `break`：指跳出整个循环体，继续执行循环下面的语句。

`return` 用于跳出所在方法，结束该方法的运行。return 一般有两种用法：

1. `return;`：直接使用 return 结束方法执行，用于没有返回值函数的方法

2. `return value;`：return 一个特定值，用于有返回值函数的方法

   ```java
      public static void main(String[] args) {
           boolean flag = false;
           for (int i = 0; i <= 3; i++) {
               if (i == 0) {
                   System.out.println("0");
               } else if (i == 1) {
                   System.out.println("1");
                   continue;
               } else if (i == 2) {
                   System.out.println("2");
                   flag = true;
               } else if (i == 3) {
                   System.out.println("3");
                   break;
               } else if (i == 4) {
                   System.out.println("4");
               }
               System.out.println("xixi");
           }
           if (flag) {
               System.out.println("haha");
               return;
           }
           System.out.println("heihei");
       }
   /**for循环中四个if判断是同时走的，，最后走一个输出“xixi”
       第一步就是输出0然后最后一个输出"xix1i"
       第二步i变为1，走第二个if判断，然后continue结束该次循环
       第三步变为2和第一步一样，只不过更改了flag
       第四步变为3输出3结束本次循环
       for循环结束
       然后判断flag输出结果，return结束
   */
   ```

   ### 2.标识符和关键字的区别是什么？

   在我们编写程序的时候，需要大量地为程序、类、变量、方法等取名字，于是就有了 **标识符** 。简单来说， **标识符就是一个名字** 。

   有一些标识符，Java 语言已经赋予了其特殊的含义，只能用于特定的地方，这些特殊的标识符就是 **关键字** 。简单来说，**关键字是被赋予特殊含义的标识符** 。比如，在我们的日常生活中，如果我们想要开一家店，则要给这个店起一个名字，起的这个“名字”就叫标识符。但是我们店的名字不能叫“警察局”，因为“警察局”这个名字已经被赋予了特殊的含义，而“警察局”就是我们日常生活中的关键字。例如static、private等等	

   ### 3.基本数据类型

   Java 中有 8 种基本数据类型，分别为：

   - 6 种数字类型：
     - 4 种整数型：`byte`、`short`、`int`、`long`
     - 2 种浮点型：`float`、`double`
   - 1 种字符类型：`char`
   - 1 种布尔型：`boolean`。

这八种基本类型都有对应的包装类分别为：`Byte`、`Short`、`Integer`、`Long`、`Float`、`Double`、`Character`、`Boolean` 。

### 4.基本类型和包装类型的区别？

- **用途**：除了定义一些常量和局部变量之外，我们在其他地方比如方法参数、对象属性中很少会使用基本类型来定义变量。并且，包装类型可用于泛型，而基本类型不可以。**

- **存储方式**：基本数据类型的局部变量存放在 Java 虚拟机栈中的局部变量表中，基本数据类型的成员变量（未被 `static` 修饰 ）存放在 Java 虚拟机的堆中。包装类型属于对象类型，我们知道几乎所有对象实例都存在于堆中。

- **占用空间**：相比于包装类型（对象类型）， 基本数据类型占用的空间往往非常小。**

- **默认值**：成员变量包装类型不赋值就是 `null` ，而基本类型有默认值且不是 `null`。**

- **比较方式**：对于基本数据类型来说，`==` 比较的是值。对于包装数据类型来说，`==` 比较的是对象的内存地址。所有整型包装类对象之间值的比较，全部使用 `equals()` 方法。**

  equals（）方法与“==”的区别

  **一、java当中的数据类型和“==”的含义：**

  - 基本数据类型（也称原始数据类型） ：byte,short,char,int,long,float,double,boolean。他们之间的比较，应用双等号（==）,比较的是他们的值。
  - 引用数据类型：当他们用（==）进行比较的时候，比较的是他们在内存中的存放地址（确切的说，是**堆内存**地址）。

  注：对于第二种类型，除非是同一个new出来的对象，他们的比较后的结果为true，否则比较后结果为false。因为每new一次，都会重新开辟堆内存空间。

  **二、equals()方法介绍：**JAVA当中所有的类都是继承于Object这个超类的，在Object类中定义了一个equals的方法，equals的源码是这样写的：

  ```java
  public boolean equals(Object obj) {
      return (this == obj);
  ```

对于包装数据类型来说，其每一个都重写过equals（）方法

对于string来说，String类中被复写的equals()方法其实是比较两个字符串的内容。下面我们通过实际代码来看看String类的比较。

```java
public static void main(String args[]) {
    String str1 = "Hello";
    String str2 = new String("Hello");
    String str3 = str2; // 引用传递
    System.out.println(str1 == str2); // false
    System.out.println(str1 == str3); // false
    System.out.println(str2 == str3); // true
    System.out.println(str1.equals(str2)); // true
    System.out.println(str1.equals(str3)); // true
    System.out.println(str2.equals(str3)); // true
}
```

![img](https://pic2.zhimg.com/80/v2-2545b1bf328d6f727d04b4a527828d2d_720w.webp)

### 5.包装类型的缓存机制

Java 基本数据类型的包装类型的大部分都用到了缓存机制来提升性能。

`Byte`,`Short`,`Integer`,`Long` 这 4 种包装类默认创建了数值 **[-128，127]** 的相应类型的缓存数据，`Character` 创建了数值在 **[0,127]** 范围的缓存数据，`Boolean` 直接返回 `True` or `False`。

两种浮点数类型的包装类 `Float`,`Double` 并没有实现缓存机制。

