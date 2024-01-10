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

**即如果创建的对象在这个范围内，则创建对象直接调用缓存数据，其在内存中的地址一样**

两种浮点数类型的包装类 `Float`,`Double` 并没有实现缓存机制。

```java
Integer i1 = 33;
Integer i2 = 33;
System.out.println(i1 == i2);// 输出 true

Float i11 = 333f;
Float i22 = 333f;
System.out.println(i11 == i22);// 输出 false

Double i3 = 1.2;
Double i4 = 1.2;
System.out.println(i3 == i4);// 输出 false

Integer i1 = 40;
Integer i2 = new Integer(40);
System.out.println(i1==i2);//输出 false 因为第一个是缓存中的地址，第二个是新创建的对象
```

### 6.自动装箱与拆箱了解吗？原理是什么

- **装箱**：将基本类型用它们对应的引用类型包装起来；

- **拆箱**：将包装类型转换为基本数据类型；

- 装箱其实就是调用了 包装类的`valueOf()`方法，拆箱其实就是调用了 `xxxValue()`方法。

  实例：

  ```java
  Integer i = 10;  //装箱
  int n = i;   //拆箱
  ```

- `Integer i = 10` 等价于 `Integer i = Integer.valueOf(10)`
- `int n = i` 等价于 `int n = i.intValue()`;

### 7.浮点数精度丢失

**原理**：十进制数转化为二进制数时，除不尽导致产生循环，丢弃循环则产生精度丢失

**实例**：

```java
BigDecimal a = new BigDecimal("1.0");
BigDecimal b = new BigDecimal("0.9");
BigDecimal c = new BigDecimal("0.8");

BigDecimal x = a.subtract(b);
BigDecimal y = b.subtract(c);

System.out.println(x); /* 0.1 */
System.out.println(y); /* 0.1 */
System.out.println(Objects.equals(x, y)); /* true */
```

**解决方法**：`BigDecimal` 可以实现对浮点数的运算，不会造成精度丢失。通常情况下，大部分需要浮点数精确运算结果的业务场景（比如涉及到钱的场景）都是通过 `BigDecimal` 来做的。

```java
BigDecimal a = new BigDecimal("1.0");
BigDecimal b = new BigDecimal("0.9");
BigDecimal c = new BigDecimal("0.8");

BigDecimal x = a.subtract(b);//subtract 减去
BigDecimal y = b.subtract(c);

System.out.println(x); /* 0.1 */
System.out.println(y); /* 0.1 */
System.out.println(Objects.equals(x, y)); /* true */
```

### 8.变量

#### 8.1成员变量与局部变量的区别

- **语法形式**：从语法形式上看，成员变量是属于类的，而局部变量是在代码块或方法中定义的变量或是方法的参数；成员变量可以被 `public`,`private`,`static` 等修饰符所修饰，而局部变量不能被访问控制修饰符及 `static` 所修饰；但是，成员变量和局部变量都能被 `final` 所修饰。

- **存储方式**：从变量在内存中的存储方式来看，如果成员变量是使用 `static` 修饰的，那么这个成员变量是属于类的，如果没有使用 `static` 修饰，这个成员变量是属于实例的。而对象存在于堆内存，局部变量则存在于栈内存。

- **生存时间**：从变量在内存中的生存时间上看，成员变量是对象的一部分，它随着对象的创建而存在，而局部变量随着方法的调用而自动生成，随着方法的调用结束而消亡。

- **默认值**：从变量是否有默认值来看，成员变量如果没有被赋初始值，则会自动以类型的默认值而赋值（一种情况例外:被 `final` 修饰的成员变量也必须显式地赋值），而局部变量则不会自动赋值。

  成员变量与class同时存在有默认值，局部变量则是方法中的值，一般没有默认值

  实例：

  ```java
  public class VariableExample {
  
      // 成员变量
      private String name;
      private int age;
  
      // 方法中的局部变量
      public void method() {
          int num1 = 10; // 栈中分配的局部变量
          String str = "Hello, world!"; // 栈中分配的局部变量
          System.out.println(num1);
          System.out.println(str);
      }
  
      // 带参数的方法中的局部变量
      public void method2(int num2) {
          int sum = num2 + 10; // 栈中分配的局部变量
          System.out.println(sum);
      }
  
      // 构造方法中的局部变量
      public VariableExample(String name, int age) {
          this.name = name; // 对成员变量进行赋值
          this.age = age; // 对成员变量进行赋值
          int num3 = 20; // 栈中分配的局部变量
          String str2 = "Hello, " + this.name + "!"; // 栈中分配的局部变量
          System.out.println(num3);
          System.out.println(str2);
      }
  }
  ```

#### 8.2 static关键字

静态变量也就是被 `static` 关键字修饰的变量。它可以被**类的所有实例共享**，无论一个类创建了多少个对象，它们都共享同一份静态变量。也就是说，静态变量只会被分配一次内存，即使创建多个对象，这样可以节省内存。

通常情况下，静态变量会被 `final` 关键字修饰成为常量。

#### 8.3 字符型常量和字符串常量的区别

- **形式** : 字符常量是单引号引起的一个字符，字符串常量是双引号引起的 0 个或若干个字符。

- **含义** : 字符常量相当于一个整型值( ASCII 值),可以参加表达式运算; 字符串常量代表一个地址值(该字符串在内存中存放位置)。

- **占内存大小**：字符常量**只占 2 个字节**; 字符串常量占若干个字节。

  ```Java
  public class StringExample {
      // 字符型常量
      public static final char LETTER_A = 'A';
  
      // 字符串常量
      public static final String GREETING_MESSAGE = "Hello, world!";
      public static void main(String[] args) {
          System.out.println("字符型常量占用的字节数为："+Character.BYTES);//2
          System.out.println("字符串常量占用的字节数为："+GREETING_MESSAGE.getBytes().length);//13
      }
  }
  ```

### 9.方法

#### 9.1方法的返回值

**1、无参数无返回值的方法**

```java
public void f1() {
    //......
}
// 下面这个方法也没有返回值，虽然用到了 return
public void f(int a) {
    if (...) {
        // 表示结束方法的执行,下方的输出语句不会执行
        return;
    }
    System.out.println(a);
}
```

**2、有参数无返回值的方法**

```java
public void f2(Parameter 1, ..., Parameter n) {
    //......
}
```

**3、有返回值无参数的方法**

```java
public int f3() {
    //......
    return x;
}
```

**4、有返回值有参数的方法**

```java
public int f4(int a, int b) {
    return a * b;
}
```

#### 9.2 静态方法为什么不能调用非静态成员?

1. 静态方法是属于类的，在类加载的时候就会分配内存，可以通过类名直接访问。而非静态成员属于实例对象，只有在对象实例化之后才存在，需要通过类的实例对象去访问。

2. 在类的非静态成员不存在的时候静态方法就已经存在了，此时调用在内存中还不存在的非静态成员，属于非法操作。

   实例：

   ```java
   public class Example {
       // 定义一个字符型常量
       public static final char LETTER_A = 'A';
   
       // 定义一个字符串常量
       public static final String GREETING_MESSAGE = "Hello, world!";
   
       public static void main(String[] args) {
           // 输出字符型常量的值
           System.out.println("字符型常量的值为：" + LETTER_A);
   
           // 输出字符串常量的值
           System.out.println("字符串常量的值为：" + GREETING_MESSAGE);
       }
   }
   ```

#### 9.3 静态方法和实例方法有何不同？

**主要体现在调用方式**

首先什么是静态方法，什么是实例方法。其中最主要的区别就在于静态方法前有static进行修饰

在外部调用静态方法时，可以使用 `类名.方法名` 的方式，也可以使用 `对象.方法名` 的方式，而实例方法只有后面这种方式。也就是说，**调用静态方法可以无需创建对象** 。

不过，需要注意的是一般不建议使用 `对象.方法名` 的方式来调用静态方法。这种方式非常容易造成混淆，静态方法不属于类的某个对象而是属于这个类。

因此，一般建议使用 `类名.方法名` 的方式来调用静态方法。

实例

```java
public class Person {
    public void method() {
      //......
    }

    public static void staicMethod(){
      //......
    }
    public static void main(String[] args) {
        Person person = new Person();
        // 调用实例方法 
        person.method();
        // 调用静态方法
        Person.staicMethod()
    }
}
```

#### 9.4 重载和重写有什么区别？

重载就是同样的一个方法能够根据输入数据的不同，做出不同的处理

重写就是当子类继承自父类的相同方法，输入数据一样，但要做出有别于父类的响应时，你就要覆盖父类方法

#### 重载

发生在同一个类中（或者父类和子类之间），方法名必须相同，参数类型不同、个数不同、顺序不同，方法返回值和访问修饰符可以不同。

《Java 核心技术》这本书是这样介绍重载的：

> 如果多个方法(比如 `StringBuilder` 的构造方法)有相同的名字、不同的参数， 便产生了重载。
>
> ```
> StringBuilder sb = new StringBuilder();
> StringBuilder sb2 = new StringBuilder("HelloWorld");
> ```
>
> 
>
> 编译器必须挑选出具体执行哪个方法，它通过用各个方法给出的参数类型与特定方法调用所使用的值类型进行匹配来挑选出相应的方法。 如果编译器找不到匹配的参数， 就会产生编译时错误， 因为根本不存在匹配， 或者没有一个比其他的更好(这个过程被称为重载解析(overloading resolution))。
>
> Java 允许重载任何方法， 而不只是构造器方法。

综上：重载就是同一个类中多个同名方法根据不同的传参来执行不同的逻辑处理。

#### 重写

重写发生在运行期，是子类对父类的允许访问的方法的实现过程进行重新编写。

1. 方法名、参数列表必须相同，子类方法返回值类型应比父类方法返回值类型更小或相等，抛出的异常范围小于等于父类，访问修饰符范围大于等于父类。

2. 如果父类方法访问修饰符为 `private/final/static` 则子类就不能重写该方法，但是被 `static` 修饰的方法能够被再次声明。

3. 构造方法无法被重写  

   构造方法，用于创建对象时执行必要的初始化操作

   构造方法的名称必须**与类名相同**，**无返回值类型**，并且**不能被手动调用**，而是在通过 new 关键字创建对象时自动执行。

   特点：

   1. 构造方法的名称必须与类名相同，且大小写也要一致。

   2. 构造方法没有返回值，包括没有 void 类型。

   3. 如果一个类没有显式地定义构造方法，则 Java 编译器会自动为该类提供一个无参构造方法。如果一个类已经定义了构造方法，则 Java 编译器不会为其再生成默认的无参构造方法。

   4. Java 中构造方法可以重载，即同一个类中可以定义多个不同参数的构造方法，它们的方法名相同，但其参数列表需要不同。

   5. 构造方法也可以拥有访问修饰符，使得其能够被其他类或方法访问。

   ```java
   public class Person {
       private String name;
       private int age;
   
       // 无参构造方法
       public Person() {
           // 执行一些初始化操作
           this.name = "Unknown";
           this.age = 0;
       }
   
       // 带参构造方法
       public Person(String name, int age) {
           // 执行一些初始化操作
           this.name = name;
           this.age = age;
       }
   
       // getter/setter 省略
   
       public static void main(String[] args) {
           // 创建对象时调用无参构造方法
           Person p1 = new Person();
           
           // 创建对象时调用带参构造方法
           Person p2 = new Person("Tom", 18);
       }
   }
   ```
   综上：**重写就是子类对父类方法的重新改造，外部样子不能改变，内部逻辑可以改变。**

   | 区别点     | 重载方法 | 重写方法                                                     |
   | ---------- | -------- | ------------------------------------------------------------ |
   | 发生范围   | 同一个类 | 子类                                                         |
   | 参数列表   | 必须修改 | 一定不能修改                                                 |
   | 返回类型   | 可修改   | 子类方法返回值类型应比父类方法返回值类型更小或相等           |
   | 异常       | 可修改   | 子类方法声明抛出的异常类应比父类方法声明抛出的异常类更小或相等； |
   | 访问修饰符 | 可修改   | 一定不能做更严格的限制（可以降低限制）                       |
   | 发生阶段   | 编译期   | 运行期                                                       |

   **方法的重写要遵循“两同两小一大”**（以下内容摘录自《疯狂 Java 讲义》，[issue#892](https://github.com/Snailclimb/JavaGuide/issues/892) ）：

   - “两同”即方法名相同、形参列表相同；
   - “两小”指的是子类方法返回值类型应比父类方法返回值类型更小或相等，子类方法声明抛出的异常类应比父类方法声明抛出的异常类更小或相等；
   - “一大”指的是子类方法的访问权限应比父类方法的访问权限更大或相等。

   ⭐️ 关于 **重写的返回值类型** 这里需要额外多说明一下，上面的表述不太清晰准确：如果方法的返回类型是 void 和基本数据类型，则返回值重写时不可修改。但是如果方法的返回值是引用类型，重写时是可以返回该引用类型的子类的。