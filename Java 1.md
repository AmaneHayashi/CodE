# Java

 * [1 基本知识](#1-基本知识)
   	* [1.1 入门](#11-入门)
     	* [1.1.1 脚本命令](#111-脚本命令)
     	* [1.1.2 主函数格式](#112-主函数格式)
     	* [1.1.3 语言特性](#113-语言特性)
     	* [1.1.4 SDK、JDK、JDE](#114-SDK、JDK、JRE)
   	* [1.2 基本语法](#12-基本语法)
  		* [1.2.1 对象与类](#121-对象与类)
  		* [1.2.2 方法与函数](#122-方法与函数)
  		* [1.2.3 基本规则](#123-基本规则)
  		* [1.2.4 标识符命名规则](#124-标识符命名规则)
  		* [1.2.5 标识符命名规范](#125-标识符命名规范)
  		* [1.2.6 注释](#126-注释)
  		* [1.2.7 注释规范](#127-注释规范)
  	* [1.3 关键字](#13-关键字)
  		* [1.3.1 访问控制](#131-访问控制)
  		* [1.3.2 类、方法与变量修饰符](#132-类、方法与变量修饰符)
  		* [1.3.3 程序控制](#133-程序控制)
  		* [1.3.4 错误处理](#134-错误处理)
  		* [1.3.5 包](#135-包)
  		* [1.3.6 基本类型](#136-基本类型)
  		* [1.3.7 变量引用](#137-变量引用)
  		* [1.3.8 保留关键字](#138-保留关键字)
  	* [1.4 基本数据类型](#14-基本数据类型)
    	* [1.4.1 变量存储与内存](#141-变量存储与内存)
    	* [1.4.2 原码、反码与补码](#142-原码、反码与补码)
    	* [1.4.3 数据类型](#143-数据类型)
  	* [1.5 运算符](#15-运算符)
    	* [1.5.1 算术运算符](#151-算术运算符)
    	* [1.5.2 关系运算符](#152-关系运算符)
    	* [1.5.3 位运算符](#153-位运算符)
    	* [1.5.4 逻辑运算符](#154-逻辑运算符)
    	* [1.5.5 赋值运算符](#155-赋值运算符)
    	* [1.5.6 其它](#156-其它)
    	* [1.5.7 运算符优先级与结合性](#157-运算符优先级与结合性)
  	* [1.6 常用转义字符](#16-常用转义字符)
  	* [1.7 循环结构与条件语句](#17-循环结构与条件语句)
  		* [1.7.1 与C语言的区别](#171-与C语言的区别)
  		* [1.7.2 循环结构](#172-循环结构)
  		* [1.7.3 条件语句](#173-条件语句)

## 1. 基本知识
### 1.1 入门
#### 1.1.1 脚本命令
- `javac FILENAME.java`：将java源文件编译为class字节码文件(生成`.class`文件)；
   - `FILENAME`为java源文件的文件名
- `java FILENAME param...`：执行java源文件；
   - `FILENAME`为java源文件的文件名
   - `param`为传入的参数(即`public static void main(String[] args)`中的`args`)，用空格隔开，可以用双引号标记
```java
public class Test {
  public static void main(String args[]){ 
    for(int i=0; i<args.length; i++){
      System.out.println("args[" + i + "]:" + args[i]);
    }
  }
}
```
```cmd
$ javac Test.java 
$ java Test hello world my java !
args[0]: hello
args[1]: word
args[2]: my
args[3]: java
args[4]: !
```
#### 1.1.2 主函数格式：
```java
public static void main(String[] args){
    System.out.println("hello world!");
}
```
#### 1.1.3 语言特性
- **面向对象**(类、接口、继承)
- **分布式**(支持分布式应用开发)
- **强类型**(变量都必须先定义后使用)
- 健壮(强类型机制、异常处理、垃圾的自动收集)
- 安全(语言安全特性，类安全防范机制)
- 体系结构中立(编译为字节码格式)
- **可移植/兼容性好[平台无关性]**(体系结构中立性)
- 高性能(JIT编译器，运行速度接近C++)
- **多线程**(并行执行)
- **兼具解释性与编译性**(*解释型语言：先翻译成中间代码，再由解释器对中间代码进行解释运行；编译型语言：将源代码编译生成机器指令，再由机器运行机器指令。*  Java的解释性：先将源代码(`.java`)编译生成字节码(`.class`)，再通过 JVM(java 虚拟机)运行生成机器指令；Java的编译性：JIT(*Just in time*)机制能够将部分已经解释翻译的常用机器指令保存。下次不需要解释，直接运行)
- **准动态语言**(*静态语言：数据类型的检查在运行前(如编译期)完成；动态语言：数据类型的检查在运行时完成，即第一次赋值给变量时在内部记录数据类型* Java的静态性：强类型机制；Java的动态性：反射机制)
#### 1.1.4 SDK、JDK、JRE
- SDK(*Software Development Kit*)：软件开发工具包，在Java中特别用于描述1998年~2006年之间的JDK
- JDK(*Java Development Kit*)：java的开发工具包，编写Java程序的程序员使用的软件 **[用于编写]** 
- JRE(*Java Runtime Environment*)：java程序的运行环境，运行Java程序的用户使用的软件 **[用于运行]** 

### 1.2 基本语法
#### 1.2.1 对象与类
- 对象(*Object*)：对象是类的一个实例
- 类(*Class*)：类是一个模板，它描述一类对象的行为和状态
#### 1.2.2 方法与函数
- 方法(*Method*)：面向对象
- 函数(*Function*)：面向过程
   
  > **在Java中，只有方法；<br>在C中，只有函数；<br>在C++中，在类里叫方法，在类外叫函数**
#### 1.2.3 基本规则
- Java大小写敏感
- Java程序入口：`public static void main(String[] args) `
- Java标识符：标识变量名、类名、类中的方法名、文件名等
- Java修饰符：修饰类中方法和属性
- Java关键字与保留字：不能用于常量、变量、和任何标识符的名称
- Java注释：注释中的字符(以及空白行)将被Java编译器忽略。
#### 1.2.4 标识符命名规则
- 以字母(`A.Z` 或者 `a.z`)、美元符(`$`)、下划线(`_`)开始
- 首字符后可以是字母(`A.Z` 或者 `a.z`)、美元符(`$`)、下划线(`_`)或数字的任何字符组合
- 关键字不能用作标识符
- 大小写敏感
#### 1.2.5 标识符命名规范
- **所有命名能通过名字看出其代表的意义，不要用拼音命名**
- 项目名：全部小写：`dorest`
- 包名：全部小写(可通过`.`分配子文件夹)：`com.amane.tools`
- 源文件名：与类名一致：`MyClass.java`
- 类/接口名：(大驼峰法)每个单词的首字母大写：`MyClass`
- 方法名：(小驼峰法)第二个单词起首字母大写：`suchMethod`
- 变量名：(小驼峰法)第二个单词起首字母大写：`hashMap`
- 数组名：`[]`紧贴数组类型之后： `int[] keys`
- 常量名：全部大写，单词之间用`_`隔开：`COMMON_KEY`
#### 1.2.6 注释
- 单行注释：`// ... //`
- 多行注释：
     - `/* ... */`：用于普通的注释
     - `/** ... */`：写入`javadoc`，鼠标放在注释的方法上面会显示注释的内容，在换行时每行开始有一个`*`<font color='red'>(**详见Java第四部分(基本技术)第4节(注释)**)</font>
```java
/**
  * this is a 
  * example of
  * multi.line comment
  */
public static void main(String[] args){
    // this is a example of single.line comment
    System.out.println("hello world!");
}
```
#### 1.2.7 注释规范
- 类注释：每个类前添加说明性注释
    ```java
    /**
    * Copyright (C), <起始年>.<终止年>, <公司名>
    * FileName: <文件名>
    * <类的详细说明>
    *
    * @author  <作者名>
    * @Date    <日期>
    * @version <版本号>
    */
    ```
- 属性注释：类的属性前添加说明性注释
    ```java
    /** 属性意义 */

    ```
- 方法注释：类的方法前添加说明性注释
    ```java
    /**
    * 类方法的使用说明
    *
    * @param <参数名> <参数使用说明>
    * @return <返回结果的说明>
    * @throws <异常类型/错误代码> <方法中抛出异常的说明>
    */
    ```
- 构造方法注释：类的构造方法前添加说明性注释
    ```java
    /**
    * 构造方法的使用说明
    *
    * @param <参数名> <参数使用说明>
    * @throws <异常类型/错误代码> <方法中抛出异常的说明>
    */
    ```
- 内部注释：用于方法中对一些难懂的代码进行注释
    ```java
    // 注释
    ```
    举例：
    ```java
    /**
    * Copyright (C), 2019.2021, BUPT
    * FileName: Person.java
    * 人物类
    *
    * @author  amanehayashi
    * @Date    22:00 21/10/2019
    * @version 1.00
    */
    public Person {

        /**人物ID */
        private String id;

        /**人物名字 */
        private String name;

        /**人物描述 */
        private String desc;
        
        //省略getter与setter方法

        /**
        * 人物类的无参构造
        */
        public Person () {

        }

        /**
        * 人物类的全参构造
        *
        * @param id 人物ID
        * @param name 人物姓名
        * @param desc 人物描述
        */
        public Person (String id, String name, String desc){
            this.id = id;
            this.name = name;
            this.desc = desc;
        }

        /**
        * map转换为Person类
        *
        * @param map 用于转换的映射表
        * @throws NullPointerException . 映射中没有键值对时抛出
        */
        public String mapToPerson(Map<String, String> map) throws NullPointerException {
            Person person = new Person();
            person.setId(map.get("id"));
            person.setName(map.get("name"));
            person.setDesc(map.get("desc"));
            return person;
        }
    }
    ```

### 1.3 关键字：
#### 1.3.1 访问控制
- `private`：私有的
- `protected`：受保护的
- `public`：公共的
#### 1.3.2 类、方法与变量修饰符
- `abstract`：抽象类
- `class`：类
- `extends`：继承
- `final`：最终(不可变)
- `implements`：实现
- `interface`：接口
- `native`：原生方法
- `new`：新建
- `static`：静态
- `strictfp`：严格
- `synchronized`：同步
- `transient`：短暂
- `volatile`：易失
#### 1.3.3 程序控制
- `break`：跳出循环
- `case`：条件
- `default`：默认
- `do`：运行
- `else`：否则
- `for`：循环
- `if`：如果
- `instanceof`：是...的实例
- `return`：返回
- `switch`：选择
- `while`：循环
#### 1.3.4 错误处理
- `assert`：断言
- `catch`：捕获
- `finally`：执行
- `throw`：抛出
- `try`：尝试
#### 1.3.5 包
- `import`：引入
- `package`：包
#### 1.3.6 基本类型
- `boolean`
- `byte`
- `char`
- `double`
- `float`
- `int`
- `long`
- `short`
#### 1.3.7 变量引用
- `super`：超类
- `this`：本类
- `void`：无返回值
#### 1.3.8 保留关键字
- `goto`：**不能使用**
- `const`：**不能使用**
- `null`：空

### 1.4 基本数据类型
#### 1.4.1 变量存储与内存
- 创建变量时，需要在内存中申请空间
- Java将内存划分为方法区、堆内存、栈内存
    - 方法区：存储已被Java虚拟机加载(类被编译后)的内容，即类信息、运行时常量池等 **[编译产生]**
      - 类信息：类名、父类名、修饰符、直接接口有序列表、类常量池等
        - 类常量池(*Class Constant Pool*)：存放编译器生成的各种字面量(包括**文本字符串/基本类型的值/`final`常量**)和符号引用(包括**类和结构的完全限定名、字段名称和描述符、方法名称和描述符**)
          - 静态变量：基本数据类型的静态变量将值存储在方法区
          - 静态引用：若未用`new`，则引用存储在方法区，指定默认值为`null`；若用`new`分配了对象，则引用存储在方法区，本身在堆内存，堆地址在方法区
          - 方法：(类编译生成的字节码中的)静态方法、普通方法(对应的字节码)加载到方法区，但**方法区中没有实例变量**
      - 运行时常量池(*Runtime Constant Pool*)：类常量池被加载到内存之后的版本，它的**字面量可以动态的添加,符号引用可以被解析为直接引用**(以字符串为例，运行时常量池通过查询全局字符串池，保证全局字符串池里的引用值与运行时常量池中的引用值一致)

      <font color='orange'>
      注：

        - 常量池包括**类常量池(属于类信息的一部分，在方法区)、运行时常量池(在方法区)、(全局)字符串常量池(JDK6.0以前在方法区，JDK7.0起在堆内存中)**
        - 每个类文件都有一个类常量池，一个运行时常量池
        - 类常量池也称为静态常量池，运行时常量池称为动态常量池

      </font>

    - 堆内存：存放所有new出来的对象 **[动态申请]**，由垃圾回收器回收
      - 特点：**跟随JVM**，JVM只有一个堆区，它被所有线程共享
      - 存储：<font color='orange'>[对非局部变量，其内容与引用都在堆中]</font>
        - 关键字`new`产生的所有对象
        - 实例变量(非`static`修饰的成员变量)
        - 数组
      - 优点：可以动态地分配内存大小，生存期也不必事先告诉编译器
      - 缺点：速度慢
    - 栈内存：存放局部变量，对象引用 **[静态调用]**，自动回收
      - 特点：**跟随线程**，每个线程包含一个栈区，栈中数据其它栈不能访问。栈中的数据都是以栈帧的格式存在。
        - 栈帧(*Stack Frame*)：内存区块。每个方法执行时，都会创建一个栈帧，用于**存储局部变量表、操作数栈、动态链接、方法出口信息**等，每一个方法从调用直至执行完毕的过程，就对应着一个栈帧在虚拟机中入栈到出栈的过程。<font color='orange'>[线程与栈一对一，方法与栈帧一对一，线程与方法(栈与栈帧)一对多]</font>
      - 存储：
        - 局部变量包括`final`的局部变量
        - 八种基本数据类型的局部变量在栈中存储对应的值
        - **局部对象的引用所指对象在堆中的地址在存储在了栈中**(如果对象的引用没有指向具体的对象，对象的引用则是`null`)
      - 优点：速度快，仅次于寄存器
      - 缺点：栈是跟随线程的，栈中的数据大小与生存期必须是确定的

  举例：
  ```java
  public class  PersonDemo
  {
      public static void main(String[] args) 
      {   //局部变量p和形参args都在main方法的栈帧中
          //new Person()对象在堆中分配空间
          Person p = new Person();
          //sum在栈中，new int[10]在堆中分配空间
          int[] sum = new int[10];
      }
  }

  class Person
  {   //实例变量name和age在堆(Heap)中分配空间
      private String name;
      private int age;
      //类变量(引用类型)name1和"cn"都在方法区
      private static String name1 = "cn";
      //类变量(引用类型)name2在方法区
      //new String("cn")对象在堆(Heap)中分配空间
      private static String name2 = new String("cn");
      //num在堆中，new int[10]也在堆中
      private int[] num = new int[10];


      Person(String name,int age)
      {   
          //this及形参name、age在构造方法被调用时
          //会在构造方法的栈帧中开辟空间
          this.name = name;
          this.age = age;
      }

      //setName()方法在方法区中
      public void setName(String name)
      {
          this.name = name;
      }

      //speak()方法在方法区中
      public void speak()
      {
          System.out.println(this.name+"..."+this.age);
      }

      //showCountry()方法在方法区中
      public static void  showCountry()
      {
          System.out.println("country="+country);
      }
  }
  ```
#### 1.4.2 原码、反码与补码(以8位为例)
- 原码：在数值前直接加一符号位的表示法(0正1负)
     - 最大正数：`0111 1111`(`127`)
     - 最小负数：`1111 1111`(`.127`)
- 反码：在原码基础上，**正数与原码相同，负数非符号位与原码相反**
     - 最大正数：`0111 1111`(`127`)
     - 最小负数：`1000 0000`(`.127`)
- 补码：在原码基础上，**正数与原码相同，负数为加高位与正数值相减**
     - 最大正数：`0111 1111`(`127`)
     - 次小负数：`1000 0001`(`.127`，**相当于`1 0000 0000 . 0111 1111`**)
     - 最小负数：`1000 0000`(`.128`)
#### 1.4.3 数据类型
- 内置数据类型
     - `byte`
       - 8位，有负号，二进制补码表示的整数
       - 最小值`.128`$(.2^7)$，最大值`127`$(2^7.1)$
       - 默认值`0`
       - 包装类为`java.lang.Byte`
       - 示例：`byte a = 10`
     - `short`
       - 16位，有符号，二进制补码表示的整数
       - 最小值`.32,768`$(.2^{15})$，最大值`32,767`$(2^{15}.1)$
       - 默认值`0`
       - 包装类为`java.lang.Short`
       - 示例：`short a = 1000`
     - `int`
       - 32位，有符号，二进制补码表示的整数
       - **是整数的默认类型**
       - 最小值$.2^{31}$，最大值$2^{31}.1$
       - 默认值`0`
       - 包装类为`java.lang.Integer`
       - 示例：`int a = 100000007`
     - `long`(<font color='red'>**注意数字后的字符`L`！**</font>)
       - 64位，有符号，二进制补码表示的整数
       - 最小值$.2^{63}$，最大值$2^{63}.1$
       - 默认值`0L`
       - 包装类为`java.lang.Long`
       - 示例：`long a = 1000L`
     - `float`(<font color='red'>**注意数字后的字符`f`！**</font>)
       - 单精度，32位，符合IEEE 754标准的浮点数
       - 最小正值$2^{.149}$，最大正值$(2.2^{.23})\times 2^{127}$[负值的值与正值相同]
       - 默认值`0.0f`
       - 包装类为`java.lang.Float`
       - 示例：`float f = 234.5f`

        <font color='orange'><注：根据IEEE 754标准，`float`分为三部分：
        - 符号位($S$，`1bit`，0为正1为负)
        - 指数位($E$，`7bit`，正规形式指数范围$.126\sim 127$，全0全1时为非正规形式)
        - 尾数位($M$，`23bit`，形式为$1.M$[正规形式]或$0.M$[非正规形式])

        正规形式下的值为$(−1)^S\times (2^{E−127})\times(1.M)$></font>
     - `double`
       - 双精度，64位，符合IEEE 754标准的浮点数
       - **是浮点数的默认类型**
       - 最小正值$2^{.1074}$，最大正值$(2.2^{.52})\times 2^{1023}$[负值的值与正值相同]
       - 默认值`0.0d`
       - 包装类为`java.lang.Double`
       - 示例：`double d = 234.5`

        <font color='orange'><注：根据IEEE 754标准，`double`分为三部分：
        - 符号位($S$，`1bit`，0为正1为负)
        - 指数位($E$，`11bit`，正规形式指数范围$.1022\sim 1023$，全0全1时为非正规形式)
        - 尾数位($M$，`52bit`，形式为$1.M$[正规形式]或$0.M$[非正规形式])
        
        正规形式下的值为$(−1)^S\times (2^{E−1023})\times(1.M)$></font>
     - `boolean`
       - 表示一位信息(真假)
       - 只有两个取值(`true`,`false`)
       - 默认值`false`
       - 包装类为`java.lang.Boolean`
       - 示例：`boolean b = true`
     - `char`
       - 表示一个16位`Unicode`字符
       - 最小值`\u0000`(即`0`)，最大值`\ufff`(即`65,535`)
       - 默认值`\u0000`
       - 包装类为`java.lang.Character`
       - 示例：`char c = 'A'`(**单引号！**)
     - `void`
       - 表示没有返回值
       - 包装类为`java.lang.Void`
       - **可以认为是一种基本数据类型**，但无法直接操作

- 引用数据类型
     - 引用类型指向一个对象，指向对象的变量是引用变量(类似于指针)
     - 对象、数组、接口均为引用数据类型
     - 默认值均为`null`

   <font color='orange'><注：内置数据类型在声明变量时，同时分配了引用空间与数据空间；引用类型，只分配了引用空间，数据空间没有分配(此时值为`null`)></font>
   
- 常量(**与变量对应**)
     - 不可被修改，**通常大写表示**
     - 使用`final`关键字修饰常量
- 字面量(**表示值**)
     - 数值字面量：前缀`0`表示8进制，`0x`表示16进制，如：
        ```java
        int a = 0144; //相当于int a = 104;
        int b = 0x14; //相当于int b = 20;
        ```
     - 字符字面量：两个**单引号**之间的字符序列(可包含`Unicode`字符)
     - 字符串字面量：两个**双引号**之间的字符序列(可包含`Unicode`字符)

   <font color='orange'><注：常量、字面量、变量的区分：
   ```java
   const int PI = 3;
   String str = "Hello World!";
   ```
   其中，`str`为变量，`3`与`"Hello World"`为字面量(`"Hello World"`也可称为字符串常量)，`PI`为常量></font>
- 类型转换
     - 转换原则
       - 优先级(自低到高)：`(byte,short,char) —> int —> long —> float —> double `
       - 不能对`boolean`类型进行类型转换
       - 不能把对象类型转换成不相关类的对象
       - 容量大(高优先级)的类型转换为容量小(低优先级)的类型时，必须使用强制类型转换
     - 强制转换
       - 大范围到小范围的强制转换可能导致溢出或损失精度，此时将按补码处理
       ```java
       int i = 256;// i = 1 0000 0000
       byte b = (byte)i;// 此时b = 0(0000 0000)
       ```
       - 浮点数到整数的强制转换是**直接舍弃小数部分**
       ```java
       int a = (int)23.7; // 此时a = 23
       int b = (int).45.67f;// 此时b = .45
       ```
       - 如果比`int`类型小的类型做运算，java在编译的时候就会将它们**统一强转成`int`类型**。如果比`int`类型大的类型做运算，就会自动转换成它们中最大类型那个
       ```java
       short a = 1;
       short b = 1;
       // 则a + b为int类型
       ```
     - 自动转换
       - 对于数字，转换前的数据类型的位数要低于转换后的数据类型
       - `char`与`int`可以自动转换

### 1.5 运算符
#### 1.5.1 算术运算符
- 加法(`+`)
- 减法(`.`)
- 乘法(`*`)
- 除法(`/`)
- 取余(`%`)
- 自增(`++`)
- 自减(`..`)<br>
   <font color='orange'>
   <注：自加与自减运算符分前缀与后缀，若为前缀(加/减号在前)，则先自加/自减再进行表达式运算，否则相反：
   ```java
   int a = 1, b = 1;
   int x = a ++;// x = 1, a = 2
   int y = ++b;// y = 2, b = 2
   a = a++;// a = 2
   b = ++b;// b = 3
   ```
   </font>
#### 1.5.2 关系运算符
- 相等(`==`)<font color='red'>[注意有两个等号！]</font>
- 不等(`!=`)
- 大于(`>`)
- 小于(`<`)
- 大于等于(`>=`)
- 小于等于 (`<=`)
#### 1.5.3 位运算符 **[对数字进行运算]**
- 与(`&`)
- 或(`|`)
- 非(`~`)
- 异或(`^`)
- 左移位(`<<`)
- (带符号)右移位(`>>`)
- (无符号)右移位(`>>>`)<br>
   <font color='orange'>
   <注：`>>`与`>>>`的差别主要体现在负数上：
   ```java
   //.1的补码是1111 1111 1111 1111 1111 1111 1111 1111
   int x = .1 >> 1;// x = .1(最高位是1)
   int y = .1 >>> 1;// y = 2^31.1(最高位是0)
   ```
   可以使用位运算符判断数字的奇偶性：
   ```java
   //右移位再左移位，将末位置0
   boolean isOdd = a >> 1 << 1 != a;
   //与1做或运算，将末位置1
   boolean isOdd = a | 1 == a;
   ```
   位运算符**不是惰性运算符**。
   </font>
#### 1.5.4 逻辑运算符 **[对布尔量进行运算]**
- 逻辑与(`&&`)
- 逻辑或(`||`)
- 逻辑非(`!`)<br>
   <font color='orange'>
   <注：逻辑运算符**是惰性运算符(短路特性)**。对于`&&`，只要第一个为`false`，则不进行后面条件计算直接返回`false`；对于`||`，只要第一个为`true`，则不进行后面条件计算直接返回`true`：
   ```java
   int a = 0;
   boolean b = (a <= 1) || (1 / a == 0);//前面为true，直接返回，不报错
   boolean b = (a == 1) && (a ++ == 0);//前面为false，直接返回，a仍然为0
   ```
   </font>
#### 1.5.5 赋值运算符
- 简单赋值(`=`)
- 加赋值(`+=`)
- 减赋值(`.=`)
- 乘赋值(`*=`)
- 除赋值(`/=`)
- 模赋值(`%=`)
- 左移位赋值(`<<=`)
- 右移位赋值(`>>=s`)
- 按位与赋值(`&=`)
- 按位异或赋值(`^=`)
- 按位或赋值(`|=`)<br>
   <font color='orange'>
   <注：对于任何(非简单)赋值运算符`W=`，`a W= b`与`a = a W b` **不完全等价**，前者不会改变`a`的数据类型，后者必须要求`a`与`b`数据类型相同：
   ```java
   short s = 3;
   s = s + 3;//报错(编译器认为3是int类型，不同类型不能计算)
   s += 3;//编译通过(此时默认3位short类型)
   ```
   </font>
#### 1.5.6 其它
- 三元运算符(`[var v =] [expression] ? [ifTrue] : [ifFalse]`)

   <font color='orange'><注：三元运算符必须有返回值，**不能是表达式**：
   ```java
   boolean b = false;
   int a;
   a = b ? 1 : .1;//正确
   b ? a = 1 : a = .1;//错误
   ```
   </font>

- 类型检查运算符(`[anObject] instanceof [aType]`)

   <font color='orange'><注：`instanceof`左侧必须是对象，右侧必须是类型(类或接口名)：
   ```java
   int a = 1;
   Integer i = 1;
   boolean b1 = a instanceof int;// 编译错误，int不是类或接口名
   boolean b2 = i instanceof Integer;// true
   boolean b3 = a instanceof Object;// 编译错误，a不是对象
   boolean b4 = i instanceof Object;// true
   ```
   判断一个实例引用的类型时:
- 使用的是实际类型 **(`new`的类型)**，而不是**声明的类型**
. 子类是父类的类型，但父类不是子类的类型
   ```java
   class School {}
   public class University extends School {
      public static void main(String[] args){
        University u1 = new University();
        University u2 = new School();//不成立(子类不能用父类实例化)
        School s1 = new School();
        School s2 = new University();//实际上是University
        boolean b1 = u1 instanceof School;//true
        boolean b2 = s1 instanceof University;//false
        boolean b3 = s2 instanceof School;//true
        boolean b4 = s2 instanceof University;//true
      }
   }
   ```
   </font>

#### 1.5.7 运算符优先级与结合性

类别	    |操作符	                      |结合性
:---:     |:---:                        |:---:
后缀    	|`()`, `[]`, `.`(点操作符)     |左到右
一元	    |`++`, `..`, `!`, `~`	        |**右到左**
乘除 	    |`*`, `/`, `％`	              |左到右
加减 	    |`+`, `.`	                    |左到右
移位 	    |`>>`, `>>>`, `<<`	          |左到右
比较 	    |`>`, `>=`, `<`, `<=` 	      |左到右
相等 	    |`==`, `!=`	                  |左到右
按位与	  |`&`	                        |左到右
按位异或	|`^`	                        |左到右
按位或	  |`|`	                        |左到右
逻辑与	  |`&&`	                        |左到右
逻辑或	  |`||`	                        |左到右
三元	    |`?`	                        |**右到左**
赋值	    |`=`, `+=`, `.=`, `*=`, `/=`, `％=`, `>>=`, `<<=`, `&=`, `^=`, `|=`	|**右到左**
逗号	    |`,`                          |左到右

  <font color='orange'><注：结合顺序导致的计算结果不同示例：

  ```java
  int a = 2;
  System.out.println(..a/2+(++a*2));//此时结果为4
  System.out.println(++a*2+..a/2);//此时结果为7
  ```
  右结合性(右到左)理解：对于`a = b + c + d`，由于`=`为右结合，故先计算右边部分，由于`+`为左结合，故先计算`b + c`(假设结果为`e`)，再计算`e + d`(假设结果为`f`)，最后将结果`f`赋值给`a`。

  三元运算符**虽然具有右结合性，但是运算时自左向右运算**：
  ```java
  int a = 2;
  int b = (a == 2) ? 1 : (++a == 3) ? 3 : 2;// a = 2, b = 1
  int c = (++a == 2) ? 1 : (++a == 3) ? 3 : 2;//a = 4, c = 2
  ```
  </font>

### 1.6 常用转义字符
符号        | 字符含义
:---:       |:---:
`\n`        | 换行
`\r`	    | 回车
`\f`	    | 换页符
`\b`	    | 退格
`\0`	    | 空字符 
`\s`	    | 字符串
`\t`	    |  制表符
`\"`	    | 双引号
`\'`	    | 单引号
`\\`	    | 反斜杠
`\ddd`	    | 八进制字符
`\uxxxx`	| 16进制`Unicode`字符

### 1.7 循环结构与条件语句
#### 1.7.1 与C语言的区别
- **java中不能用1与0代替`true`与`false`**
#### 1.7.2 循环结构
- `while`循环：至少执行0次，当表达式为`false`时跳出循环。
   ```java
   while(布尔表达式){
     //循环体
   }
   ```
- `do...while`循环：**至少执行1次**，当表达式为`false`时跳出循环。
   ```java
   do{
     //循环体
   } while(布尔表达式);
   ```
- `for`循环：执行次数在执行前已决定，当表达式为`false`时跳出循环。
   ```java
   for(初始值;布尔表达式;更新形式){
     //循环体
   }
   ```
- 无限循环的三种形式
   ```java
   方法一：while(true){...}
   方法二：do{...}while(true);
   方法三：for(;;){...}
   ```
- 嵌套循环(多见于`for`嵌套)：在`for`循环中再嵌套`for`循环，可用于遍历多维数组等
   ```java
   for(int i = 0; i < 10; i ++){
     for(int j = 0; j < 10; j ++){
       System.out.println(10 * i + j);
     }
   }
   //执行结果：顺次输出0~99的所有整数
   ```
. `break`：用于**跳出当前循环**
   ```java
   for(int i = 0; i < 10; i ++){
     for(int j = 0; j < 10; j ++){
       if(j == 8){
         break;
       }
       System.out.println(10 * i + j);
     }
   }
   //执行结果：顺次输出0~99中所有个位数小于8的整数
   ```
   <font color='orange'><注：若想一次性跳出所有循环，可以通过标号实现：
   ```java
   label:
   for(int i = 0; i < 10; i ++){
     for(int j = 0; j < 10; j ++){
       if(j == 8){
         break label;
       }
       System.out.println(10 * i + j);
     }
   }
   //执行结果：顺次输出0~7的所有整数
   ```
   </font>

- `continue`：用于**跳过当前次循环(进入下一次)**
   ```java
   for(int i = 0; i < 10; i ++){
     for(int j = 0; j < 10; j ++){
       if(j == 8){
         continue;
       }
       System.out.println(10 * i + j);
     }
   }
   //执行结果：顺次输出0~99中所有个位数不等于8的整数
   ```
- 增强循环：用于对数组或集合进行循环。
   ```java
   int[] a = {10, 20, 30, 40, 50};
   for(int i : a){
     System.put.println(i);
     i ++;
   }
   //执行结果：顺次输出数组元素，但数组元素值不变
   ```
     <font color='orange'><注：
     **与普通循环相比，增强循环更加简洁，适合于只要元素输出的情景。增强循环得不到下标(索引)，且无法对元素进行操作。**
   ```java
   //反编译结果
    int[] a = { 10, 20, 30, 40, 50 }; byte b; int j, arrayOfInt[];
    for (j = (arrayOfInt = a).length, b = 0; b < j; ) { 
      int i = arrayOfInt[b];
      System.out.println(i);
      i++;
      b++; 
    }
   ```
    **对于数组，增强循环依然是使用索引遍历(但是是对临时数组的索引)；对于集合，增强循环采用的是迭代器遍历。**</font>
   
   循环还可以通过<font color='red'>**迭代器遍历(详见)**、`forEach`**语句(详见)**</font>实现。
#### 1.7.3 条件语句
- `if...else if...else`：每组条件语句**只有最先为真的执行，执行优先级与出现顺序相同**。可以出现的组合有：`if`、`if`+`else`，`if`+`else if`+`else`。**可以出现嵌套选择语句**。
    ```java
    if(布尔表达式){
      //代码段
    }
    else if(布尔表达式){
      //代码段
    }
    else{
      //代码段
      if(布尔表达式){
          //代码段
      }
      else {
          //代码段
      }
    }
    ```
- `switch...case...deafult`：判断**一个变量与一系列值中某个值是否相等**，每个值称为一个分支。
    - `switch`语句中的变量类型可以是：`byte`、`short`、`int`、`char`、`String`(从JSE1.7起支持)
    - `case`语句的值的数据类型必须与变量的数据类型相同，且必须为字符串常量或字面量
    - `switch`语句可以包含一个`default`分支，在没有`case`语句的值和变量值相等的时候执行，**`default`分支不需要`break`语句**
    - 当变量的值与`case`语句的值不相等时，**直接跳入下一个`case`，无论当前`case`有没有`break`都不会执行**
    - 当变量的值与`case`语句的值相等时，`case`语句之后的语句开始执行，**直到第一个`break`语句出现(这个`break`不一定是这个语句的`case`，每个`case`不必须要求有一个`break`)时停止**
    ```java
    switch(变量){
      case 可选值：
          //执行语句
      case 可选值：
          //执行语句
      -..
      default:
          //执行语句
    }
    ```
    ```java
    int i = 1
    switch(i){
      case 0：
          System.out.print(0);
      case 1：
          System.out.print(1);
      case 2:
          System.out.print(2);
          //break;
      default:
          System.out.print("default");
    }
    //若注释break，输出为：12default
    //若不注释break，输出为：12
    ```
