# Java
### 2.面向对象
#### (1)入门
1. 面向对象的三个特征：**封装性、继承性、多态性**
2. 类：创建Java对象的模板
   - **类名与源文件名统一，一个源文件中只能有一个`public`类**
   - 一个类中可以有**局部变量、实例变量与类变量**
   - 一个类要有构造方法(**若不显式定义，Java编译器会自动提供无参构造方法**)
     - 构造方法不能直接调用，必须通过`new`关键字来自动调用，创建类的实例
   - 根据类可以创建对象，需要**声明、实例化、初始化**

      <font color='orange'><注：以实例化一个学生对象为例：
      ```java
      Student stu = new Student("小明", "男", 15);
      ```
      - 声明：`Student`，说明了对象的引用类型为`Student`
      - 实例化：`new Student()`，分配内存空间，引起构造方法的调用，为对象返回一个`Student`引用
      - 初始化：`("小明", "男", 15)`，通过`Student`的有参构造函数对类的实例变量进行初始化>

      </font>
   - 可以根据创建的对象访问实例变量，调用成员方法
    ```java
    public class MyClass {
        private int label;

        public int squareLabel() {
            return label * label;
        }

        public static void main(String[] args){
            //初始化一个类[声明，实例化，初始化]
            MyClass myclass = new MyClass();
            //访问实例变量
            myclass.label = 2;
            //调用成员方法
            System.out.println(myclass.squareLabel());
            //输出：4
        }
    }
    ```
3. 方法：包含于类或对象中，是**解决一类问题的步骤的有序组合**
   - 方法的优点：
     - 使程序变得更简短而清晰
     - 有利于程序维护
     - 可以提高程序开发的效率
     - 提高了代码的重用性
   - 方法的写法：
      ```java
      修饰符 返回值类型 方法名(参数类型 参数名) [抛出异常]{
          ...
          方法体
          ...
          return 返回值;
      }
      ```
      - 修饰符：定义该方法的访问类型(**告诉编译器如何调用该方法**)
      - 返回值类型：定义返回值的数据类型(**没有返回值，类型为`void`**)
      - 方法名：方法的实际名称
      - 参数：**占位符(形参)。当方法被调用时，传递值给参数。这个值被称为实参。参数是可选的，方法可以不包含任何参数**
      - 方法体：具体的功能代码块
      - 抛出异常：可选部分。方法执行时可能会有异常，可以在方法方法头通过`throws`关键字抛出异常(**消极处理方式，异常将由上层调用处理**)，关键字后面写抛出的异常类
      - 返回值：方法处理结束后需要返回给调用者的值
      ```java
      public int maxSquare(int a, int b) {
        int result;
        if(a > b){
          result = a * a;
        }
        else{
          result = b * b;
        }
        return result;
      }
      ```
      在上面的例子中，`public`为修饰符，`int`为返回值类型，`maxSquare`为方法名，`int`为参数类型，`a, b`为参数名，中间代码为方法体，`result`为返回值。
   - 方法的调用：当程序调用一个方法时，程序的控制权交给了被调用的方法。当**被调用方法的返回语句执行或者到达方法体闭括号时**，交还控制权给程序。
     - `main`方法被JVM调用，其`args`参数(命令行参数)可以通过命令行传入<font color='red'>(**详见Java第一部分(基本知识)第1节(入门)第1点(脚本命令)**)</font>
     - 方法有返回值时，可以将方法调用的结果当做一个值
     - 方法无返回值时，可以将方法调用看作一条语句
      ```java
      //方法有返回值
      int i = Math.max(20, 30);
      //方法无返回值
      System.out.println("hello world!");
      ```
      ```java
      //[1]
      public static int add(int a, int b){
          return a + b;
      }
      
      //[2] - [1]的重载
      public static Integer addInt(Integer a, Integer b){
          return add(a, b);
      }

      //[1],[2]不能将方法写作return plus(a, b)或return plusInt(a, b);

      //[3]
      public int plus(int a, int b){
          return plusInt(a, b);
      }

      //[4] - [3]的重载
      public Integer plusInt(Integer a, Integer b){
          return plus(a, b);
      }
      //[3],[4]可以将方法写作return add(a, b)或return addInt(a, b);
      ```
    <font color='green' style='font-weight:bold'>

    - 方法的值传递与引用传递
      - 基本数据类型是值传递，对形参的修改不会影响实参
      - 引用类型(对象+数组)是引用传递，形参和实参指向同一个内存地址(同一个对象)，所以对对象属性(数组元素)的修改会影响到实参。但是直接对对象修改时，相当于将形参指向另一个内存地址，则不会影响到实参
      - `String`以及基本数据类型的包装类可以理解为传值，对形参的修改不会影响实参
    
    </font>

      ```java
      public static void main(String[] args){
          int a = 10, b = 20;
          Integer i = 20, j = 20;
          int[] arr = {1, 2, 3, 4, 5};
          String s = "helloworld";
          swap(a, b);
          System.out.println("a: " + a + ", b: " + b);
          //输出：a:10, b:20(值传递不影响实参)
          swap(i, j);
          System.out.println("i: " + i + ", j: " + j);
          //输出：i:10, j:20(包装类也是值传递不影响实参)
          subStr(s);
          System.out.println("s: " + s);
          //输出：s: helloworld(String也是值传递不影响实参)
          nullStr(s);
          System.out.println("s: " + s);
          //输出：s: helloworld(同理)
          editFirst(arr);
          System.out.println("arr:" + Arrays.toString(arr));
          //输出：arr: [2, 2, 3, 4, 5](数组是引用传递，修改元素影响实参)
          changeArr(arr);
          System.out.println("arr:" + Arrays.toString(arr));
          //输出：arr: [2, 2, 3, 4, 5](数组是引用传递，但将形参指向另一个内存地址，对实参无影响)
      }

      //该方法实现两个整数的交换
      public static void swap(int a, int b){
          a = a + b;
          b = a - b;
          a = a - b;
          System.out.println("a: " + a + ", b: " + b);
          //输出:a:20, b:10(实现交换)
      }

      //该方法实现两个整数的交换
      public static void swap(Integer i, Integer j){
          i = i + j;
          j = i - j;
          i = i - j;
          System.out.println("i: " + i + ", j: " + j);
          //输出:i:20, j:10(实现交换)
      }

      //该方法实现在字符串后连接新字符串"123"
      public static void concatStr(String s){
          s = s.concat("123");
      }

      //该方法实现将字符串置为null
      public static void nullStr(String s){
          s = null;
      }

      //该方法实现将数组第一个元素置为1
      public static void editFirst(int[] arr){
          arr[0] = 2;
      }

      //该方法实现替换数组
      public static void changeArr(int[] arr){
          arr = new int[]{1, 2, 3};
      }
      ```
    - 方法的可变参数
      - 写法：`type... params`
      - **一个方法只能有一个可变参数，必须是最后一个参数**
      - **可变参数与数组在编译后是相同的**，不能作为方法的重载
      - 可变参数方法的优先级低于固定参数方法
      ```java
      public static void func(String... params){
          System.out.println(1);
      }

      //该方法会报错，与可变参数重复
      public static void func(String[] params){}

      public static void func(String param1, String param2){
          System.out.println(0);
      }

      public static void main(String... args){
          func("str");
          //此时输出为1(可变参数)
          func("str", "str");
          //此时输出为0(固定参数>可变参数)
          func("str", "str"， "str");
          //此时输出为1(可变参数)
      }
      ```
    - 静态方法与非静态方法
      - 静态方法：属于类的方法，使用`static`修饰
        - 可以调用静态方法、静态变量，不能直接调用非静态方法、非静态变量(可以通过实例化对象后调用)
        - 访问方式：`类名.方法名`(推荐)或`对象名.方法名`
      - 非静态方法：属于对象(实例)的方法
        - 可以调用非静态方法、非静态变量、静态方法、静态变量
        - 访问方式：`对象名.方法名`
        ```java
        public class Test {
            //静态变量
            public static String str = "hello";
            //非静态变量
            String s = "world!";
        }

        //静态方法
        public static void main(String[] args){
            System.out.println(str);//编译通过[A1]
            System.out.println(s);//编译不通过[A2]
            System.out.println(Test.str);//编译通过[A3]
            System.out.println(Test.s);//编译不通过[A4]
            Test test = new Test();
            System.out.println(test.str);//编译通过[A5]
            System.out.println(test.s);//编译通过[A6]
        }

        //非静态方法
        public void print(){
            System.out.println(str);//编译通过[B1]
            System.out.println(s);//编译通过[B2]
            System.out.println(Test.str);//编译通过[B3]
            System.out.println(Test.s);//编译不通过[B4]
            Test test = new Test();
            System.out.println(test.str);//编译通过[B5]
            System.out.println(test.s);//编译通过[B6]
        }
        /* 结果分析：
        A1,B1；静态变量能直接被静态、非静态方法访问
        A2,B2：非静态变量不能被静态方法访问，能被非静态方法访问
        A3,B3：静态变量可以通过'类名.变量名'访问
        A4,B4：非静态变量不能通过'类名.变量名'访问
        A5.B5：非静态变量可以通过'对象名.变量名'访问
        A6,B6：静态变量可以通过'对象名.变量名'访问
        */
        ```
    - 构造方法
      - 构造方法和它所在类的名字相同
      - 构造方法没有返回值
      - 构造方法可以重载(定义多种构造方法)
      - 不能直接调用，必须通过`new`关键字来自动调用，创建类的实例
      - Java提供一个**默认的无参构造方法，其修饰符和类的修饰符相同，将所有类变量初始化为默认值**。一旦自定义构造方法，则默认方法失效(**自定义有参构造，则默认无参构造失效**)
      - 构造方法的参数名与实例变量名相同时，可以用`this`指代实例变量
      ```java
      class MyClass {
        int i;
      
        // 无参构造方法
        MyClass(){}

        // 有参构造方法
        MyClass(int i ) {
          this.i = i;
        }
      }
      ```
    - 析构方法(**已过时**)
      - 方法名：`finalize()`
      - 修饰符：`protected`(确保不会被类以外代码调用)
      - 在对象被垃圾收集器析构之前调用，用来清除回收对象(相当于手动回收)
      - 过时原因：可能导致性能问题、死锁、挂起、资源泄漏。
      ```java
        public static void main(String... args) {
          Brokens b = new Brokens(1);
          System.out.println(b.toString());
          b = null;
          System.gc();//执行本语句时调用finalize()
        }
        
        //finalize()方法的写法
        @Override
        protected void finalize() throws Throwable {
          super.finalize();
          System.out.println("finalized");
        }
      ```
4. Java 变量类型
    - 变量的声明：`type identifier [= value][, type identifier [= value] ...];`

    <font color='green' style='font-weight:bold'>

    - Java 变量类型有**类变量、实例变量、局部变量**
      - 类变量(静态变量)
        - 声明关键字：`static`
        - 声明地点：类中，方法、构造方法、语句块之外
        - 修饰符：一般使用`public`
        - 访问方式：可通过`类名.变量名`访问
        - 默认值：有
        - 初始化：声明时初始化、静态语句块初始化、构造方法初始化、静态方法初始化
        - 修改值：部分允许(对于`final`修饰的类变量，不允许)
        - 存储：方法区
        - 生命周期：在第一次被访问时创建，在程序结束时销毁
        - 数量：类只拥有类变量的一份拷贝，与创建对象数无关(所有对象共享)
        - 其它特点：一般被声明为常量(`static final`)
      - 实例变量
        - 声明关键字：无
        - 声明地点：类中，方法、构造方法、语句块之外
        - 修饰符：一般使用`private`
        - 访问方式：可通过`getter`方法(通用)或`对象名.变量名`访问(若变量为`private`，则此方法只适用于当前类内的方法调用)
        - 默认值：有
        - 初始化：`setter`方法初始化、构造方法初始化
        - 修改值：允许
        - 存储：堆内存
        - 生命周期：在对象创建的时候创建，在对象被销毁的时候销毁
        - 数量：每个对象拥有实例变量的一份拷贝
        - 其它特点：实例变量在整个类内部是可访问的，而不管实例变量声明在类的哪个位置(但为了阅读方便一般写在头部)
      - 局部变量
        - 声明关键字：无
        - 声明地点：方法、构造方法、语句块中
        - 修饰符：不可使用
        - 访问方式：只有对应的方法、构造方法、语句块中可以访问
        - 默认值：无，必须初始化才能使用
        - 初始化：新建时必须初始化
        - 修改值：允许
        - 存储：栈内存
        - 生命周期：在方法、构造方法、语句块被执行的时候创建，执行完成后被销毁(循环初始化部分声明的变量的生命周期为整个循环，循环体内声明的变量声明周期是从它声明到循环体结束)
        - 数量：每个方法、构造方法、语句块可以创建自己的局部变量

      </font>

     ```java
      public class MyClass {
          // 类变量(常量)[一般public static final]
          public static final int PI; //可在此初始化
          //类变量[一般public static]
          public static int visits; //可在此初始化
          //实例变量[一般private]
          private int level; //可在此初始化(意义不大)

          //静态代码块
          static {
              //可以在此处初始化，但与上面的初始化只能有一个(final关键字的变量不可重复赋值)
              PI = 3;
              //没有final关键字的类变量可以在此处初始化，可以多次赋值
              visits ++;
              //静态方法不能调用非静态变量
          //    level = 1; //(编译错误！)
          }

          public MyClass() {
              //final类变量不可在构造代码块初始化！
          //    PI = 3; //(编译错误！)
              //没有final关键字的类变量可以在此处初始化
              visits ++;
              //实例变量可以在构造代码块初始化，但没有太大意义
              level = 1;
          }

          public MyClass(int level){
              visits ++;
              //实例变量在构造代码块中最常用的初始化方式
              this.level = level;
          }

          public static void main(String[] args){
              //myclass1.level与myclass1.getLevel()等价
              MyClass myclass1 = new MyClass(1);
              System.out.println("myclass1相关参数：" + "常量:" + PI + "类变量：" + visits + "实例变量：" + myclass1.level);
              MyClass myclass2 = new MyClass(1);
              System.out.println("myclass2相关参数：" + "常量:" + PI + "类变量：" + visits + "实例变量：" + myclass2.getLevel());
              /**理论输出为：
              * myclass1相关参数：常量:3类变量：2实例变量：1
              * myclass2相关参数：常量:3类变量：3实例变量：1
              */
              //改变静态变量与实例变量的值，观察变化
              myclass1.setBiggerSquare(3);
              myclass2.setLevel(3);
              System.out.println("myclass1相关参数：" + "常量:" + PI + "类变量：" + visits + "实例变量：" + myclass1.getLevel());
              System.out.println("myclass2相关参数：" + "常量:" + PI + "类变量：" + visits + "实例变量：" + myclass2.level);
              /**理论输出为：
              * myclass1相关参数：常量:3类变量：9实例变量：1
              * myclass2相关参数：常量:3类变量：9实例变量：3
              */
          }

          //这是一个非静态方法
          public void setBiggerSquare(int root){
              //局部变量必须在声明时初始化
              int square = root * root;
              visits = Math.max(visits, square);
              //执行完毕,square的生命结束
          }

          //通过一系列getter与setter方法提供外部对实例变量访问的途径
          public void setLevel(int level){
              this.level = level;
          }

          public int getLevel(){
              return this.level;
          }

          //实例变量可以声明在类的任何位置，且不受影响
          private int grades;
      }
     ```
5. Java 修饰符：用来定义类、方法或者变量，通常放在语句的最前端。
   - 访问控制修饰符：设置访问权限，保护对类、变量、方法和构造方法的访问
     - `default`(即不写修饰符)：同一包内的类可见，可用于类、接口、变量、方法
     - `private`：同一类内可见，可用于变量、方法、部分类(**可用于内部类，不可用于其它类**)
     - `public`：所有类可见，可用于类、接口、变量、方法
     - `protected`：同一包内的类和子类可见，可用于变量、方法、部分类(**可用于内部类，不可用于其它类**)
     - 访问可见性比较：`public`>`protected`>`default`>`private`
     - 访问修饰符的继承规则：**不能降低访问可见性**
      <table style="text-align:center;margin:auto;">
      <tr>
          <th rowspan="2">父类修饰符</th>
          <th colspan="4">子类修饰符</th>
      </tr>
      <tr>
          <td><code>public</code></td>
          <td><code>protected</code></td>
          <td><code>default</code></td>
          <td><code>private</code></td>
      </tr>
      <tr>
          <td><code>public</code></td>
          <td>√</td>
          <td>×</td>
          <td>×</td>
          <td>×</td>
      </tr>
      <tr>
          <td><code>protected</code></td>
          <td>√</td>
          <td>√</td>
          <td>×</td>
          <td>×</td>
      </tr>
      <tr>
          <td><code>default</code></td>
          <td>√</td>
          <td>√</td>
          <td>√</td>
          <td>×</td>
      </tr>
      <tr>
          <td><code>private</code></td>
          <td>√</td>
          <td>√</td>
          <td>√</td>
          <td>√</td>
      </tr>
      </table>
      
   - 非访问修饰符
     - `static`：静态修饰符，修饰方法、变量
       - 静态变量：声明独立于对象的静态变量。**无论一个类实例化多少对象，它的静态变量只有一份拷贝**。访问方式：`className.variableName`<font color='red'>(**详见Java第二部分(面向对象)第1节(入门)第4点(Java 变量类型)**)</font>
       - 静态方法：声明独立于对象的静态方法。**静态方法不能直接使用类的非静态变量**。访问方式：`className.methodName`<font color='red'>(**详见Java第二部分(面向对象)第1节(入门)第3点(方法)**)</font>
     - `final`：最终修饰符，修饰类、方法、变量、对象
       - 常量：`final`修饰的变量**不能被重新赋值**，必须显式指定初始值，**通常和`static`修饰符一起使用创建常量**
       - 最终方法：可以被子类继承，但是**不能被子类重写**
       - 最终类：**不能被继承**(如`java.lang.String`类)
       - 对象：`final`修饰的对象**内存地址不能改变，但是可以修改其属性**
      ```java
        //最终类
      public final class Test {
            //常量
            public static final float PI = 3.14159;
            //最终方法
            public final float getPI(){
                return PI;
            }
      }
      ```
      ```java
      //final变量的三种赋值方式
      public class Test {
          public final int j = 1;//方法一
          public final int k;

          public Test() {
              k = 3;//方法二
          }

          public Test() {
              this();//方法二变体(无参构造器赋值)
          }

          public final int i;

          //构造代码块
          {
              i = 2;//方法三
          }
      }
      ```
      ```java
      //final static变量的三种赋值方式
      public class Test {
          public final static int PI = 3;//方法一
          public final static double E;

          //静态代码块
          static {
              E = 2.71828;//方法二
          }
      }
      ```
      ```java
      public class Person {
          private String name;
          public Person(){};
          public Person(String name){
              this.name = name;
          }
          //省略getter与setter方法
          public static void main(String[] args){
              final Person person = new Person("小王");
              person.setName("小明");//编译通过
              person = null;//编译错误
          }
      }
      ```
     - `abstract`：抽象修饰符，修饰类、方法<font color='red'>(**详见Java第二部分(面向对象)第6节(接口与抽象类)第3点(抽象类)**</font>
       - 抽象类：**不能实例化对象，用于将来子类进行扩充**
       - 抽象方法：没有功能代码块的方法，其**实现由子类提供**
     - `synchronized`：同步修饰符，修饰方法<font color='red'>(**Java 并发详见**)</font>
       - 被同步修饰符修饰的方法，同一时间只能被一个线程访问
     - `transient`：暂态修饰符，修饰变量<font color='red'>(**Java 序列化详见**)</font>
       - 被该修饰符修饰的变量，**当对象被序列化时时，变量值不会被持久化；当对象被反序列化时，变量值变为默认值**
     - `volatile`：共享修饰符，修饰变量<font color='red'>(**Java 并发详见**)</font>
       - 被该修饰符修饰的成员变量在**每次被线程访问时，都强制从共享内存中重新读取该成员变量的值。当成员变量发生变化时，会强制线程将变化值回写到共享内存。在任何时刻，两个不同的线程总是看到该成员变量的同一个值**
       - `volatile`不能用在`final`前面：`final`禁止修改，而`volatile`支持更新，两者相互矛盾
       - `volatile`对象引用可能是`null`
     - `native`：本地修饰符，修饰方法
       - 本地方法不由Java语言实现
       - 本地方法可以返回的类型不受限制
       - 本地方法在定义时不需要功能代码块(其实现由外部代码完成)
     - `strictfp`：精确浮点修饰符，修饰类、方法
       - 使用该修饰符时，所声明的范围内Java的编译器以及运行环境会完全依照浮点规范IEEE-754来执行。
       - 使得浮点运算更加精确， 且不会因不同的硬件平台导致执行的结果不一致
   - 修饰符与可修饰内容一览表

        修饰符          | 类    | 接口 |内部类 | 方法   | 变量  |对象
        :---:          |:---:  |:---: |:---:  |:---:  |:---: |:---:
        `public`       | √     | √    | √     |√      |√     |×
        `protected`    | ×     | ×    | √     |√      |√     |× 
        `private`      | ×     | ×    | √     |√      |√     |×
        `static`       | ×     | ×    | √     |√      |√     |×
        `final`        | √     | ×    | √     |√      |√     |√
        `abstract`     | √     | √    | √     |√      |×     |×  
        `synchronized` | ×     | ×    | ×     |√      |×     |× 
        `transient`    | ×     | ×    | ×     |×      |√     |×
        `volatile`     | ×     | ×    | ×     |×      |√     |× 
        `native`       | ×     | ×    | ×     |√      |×     |×  
        `strictfp`     | √     | √    | √     |√      |×     |× 

#### (2)封装
1. 定义：将抽象性函式接口的实现细节部份包装、隐藏，必须通过严格的接口控制才能访问该类的代码和数据
2. 功能：只需修改代码实现，而不用管代码调用
3. 优点：
   - 良好的封装能够减少耦合
   - 类内部的结构可以自由修改
   - 可以对成员变量进行更精确的控制
   - 隐藏信息，实现细节
4. 实现举例：将类的实例变量属性设置为`private`，并提供对外的公共方法访问(`getter`与`setter`方法)
   ```java
   public class Test {

       private int flag;

       public void setFlag(int flag){
           this.flag = flag;
       }

       public int getFlag(){
           return flag;
       }
   }
   ```
#### (3)继承
1. 定义：子类继承父类的特征和行为，使得子类对象(实例)具有父类的实例域和方法，或子类从父类继承方法，使得子类具有父类相同的行为。
2. 驱动力：代码重复臃肿、维护性低→将代码中相同的部分提取出来组成一个父类→继承→提高代码维护性、简洁度、复用性
   - 代码维护性：后期需要修改时需要修改的代码数
3. 特点：
   - 子类拥有父类**非`private`的属性、方法**
   - 子类可以对父类进行扩展
   - 子类可以用自己的方式实现父类的方法
   - Java 支持单继承(父子)、多重继承(父子孙)，不支持多继承(两个爸爸)(可以通过`implements`实现多个接口)
   - 如果不写继承，则所有的类默认继承于`java.lang.Object`(祖先)
4. 矛盾点：继承提高了代码的耦合性，降低了代码的独立性
5. 关键字：`extends`(继承类)，`implements`(实现接口)
   - `extends`：只能继承一个类
   - `implements`：可以继承多个接口(接口间用逗号分隔)<font color='red'>(**详见Java第二部分(面向对象)第6节(接口与抽象类)第4点(接口)**</font>
6. 引用：`super`(引用父类)，`this`(引用自身)
   - `super`：实现对父类成员的访问
     - 调用父类构造方法：`super`语句必须是子类构造方法的第一条语句(默认调用)
        ```java
        super();//调用无参构造
        super(参数列表);//调用有参构造
        ```
        ```java
        public class Father {
            public Father(){};
        }

        public class Child {
            public Child(){
                super();//也可不写，默认调用super()
                System.out.println("child constructs");
            }

            public Child(int i){
                System.out.println("child constructs");
                super();//编译错误，super语句必须是第一条语句
            }
        }
        ```
     - 调用父类方法或变量：
        ```java
        /* 未重写时可直接访问 */
        方法名(参数列表);
        变量名;
        /* 重写后需要super */
        super.方法名(参数列表);
        super.变量名;
        ```
   - `this`：实现对自身成员的访问
     - 调用子类构造方法：`this`语句必须是子类构造方法的第一条语句(常用于子类构造方法重载的情形)
        ```java
        this();//调用无参构造
        this(参数列表);//调用有参构造
        ```
        ```java
        public class Father {
            public Father(){};
        }

        public class Child {

            private int i;

            public Child(){
                this(0);//重载调用
            };

            public Child(int i){
                this.i = i;
            }

            public Child(){
                super();
                this(0);//编译错误，this必须是第一条语句
            }
        }
        ```
      - 调用当前对象方法或变量
        ```java
        this.变量名;
        this.方法名;
        //类变量推荐使用类名.变量名访问
        ```
    - 注意：**不能在静态方法中使用`super`与`this`**
7. 构造方法的继承：
   - 构造方法不能被重写
   - 子类构造方法时先调用父类构造方法(**多重继承则从祖先类开始**)
   - 子类不继承父类的构造方法，不能在子类中使用父类构造方法名来调用父类构造方法
   - 一旦子类显式调用父类构造方法，则不再默认调用父类无参构造
   - 构造方法的调用分析：
     - 父类有无参构造方法：子类默认调用父类的无参构造方法
     - 父类无无参构造方法：子类必须显式调用其有参构造方法，否则编译错误
     - 父类同时有无参、有参构造方法：可以自行选择调用何种构造方法

```java
public class Father {
    public Father(int s){};
}

public class Child extends Father {
    public Child(){
        //编译错误，父类只有有参构造，必须显式调用
    }

    public Child(){
        super(0);//编译成功
    }

    public Child(int s){
    super(s);//编译成功
    }
}
```
```java
public class Father {
    public Father(){};
    public Father(int s){};
}

public class Child extends Father {
    public Child(){
        super(0);//调用了有参构造
    }

    public Child(int s){
    //调用了无参构造
    }
}
```
8. 静态成员的继承：
   - 静态成员不能被继承，只能被访问(当且仅当子类没有与父类指定的静态成员同名的成员时，否则无法访问)
   - 静态成员**不存在被子类重写的情况，也就不构成多态**
```java
public class Father {
    public static void f(){
        System.out.println("father f");
    };
}

public class Child extends Father {

    public static void f(){
        System.out.println("child f");
    };

    public static void main(String[] args){
        Father f = new Child();
        f.f();
        Child c = new Child();
        c.f();
    }
    /* 如果Child类没有写f()方法，输出为：
        father f
        father f
    *  Child类写了f()方法后，输出为：
        father f
        child f
    */
}
```
9.  父类成员修饰符与子类继承、旁类访问的关系：
    <font color='green' style='font-weight:bold'>
     - 修饰符与旁类、子类对父类实例成员访问权限的关系：
       - `default`：父类与同包类[A]可以访问父类静态成员，不同包类[B]均不能访问(A、B互相无法访问)
       - `private`：父类[A]可以访问父类静态成员，其它类(子类、旁类)[B]均不能访问(A、B互相无法访问)
       - `public`：任何类均能互相访问
       - `protected`：如下表所示

        继承  | 同包 | 访问从父类继承的成员 | 访问子类继承的成员 | 访问父类实例的成员 | 访问兄弟类实例的成员 
        :---:     |:---: |:---: |:---: |:---: |:---:
        是        | 是 |√    |√     |√   |√ 
        是        | 否 |√    |√     |×   |×
        否        | 是 |——   |——    |√   |√
        否        | 否 |——   |——    |×   |×
        (注意：无论子类是否能访问父类的方法，其均继承了该方法，只是无法访问而已)
     - 修饰符与旁类、子类对父类静态成员访问权限的关系：
       - `default`：父类与同包类[A]可以访问父类静态成员，不同包类[B]均不能访问(A、B互相无法访问)
       - `private`：父类[A]可以访问父类静态成员，其它类(子类、旁类)[B]均不能访问(A、B互相无法访问)
       - `public`：任何类均能互相访问
       - `protected`：父类、同包类、子类[A]可以访问父类静态成员，不同包旁类[B]不能访问(A、B互相无法访问)

</font>

  ```java
  //例1
  package pkg0;
  public class Father {
      protected void f(){};
      public static void main(String[] args){
          new Father().f(); //编译通过
          new Child0().f(); //编译通过
          new Child01().f(); //编译通过
          new Child1().f(); //编译通过
          new Child11().f(); //编译通过
          new Child2().f(); //编译通过
      }
  }

  public class Child0 extends Father {
      public static void main(String[] args){
          new Father().f(); //编译通过
          new Child0().f(); //编译通过
          new Child01().f(); //编译通过
          new Child1().f(); //编译通过
          new Child11().f(); //编译通过
          new Child2().f(); //编译通过
      }
  }

  public class Child01 extends Father {
      public static void main(String[] args){
          new Father().f(); //编译通过
          new Child0().f(); //编译通过
          new Child01().f(); //编译通过
          new Child1().f(); //编译通过
          new Child11().f(); //编译通过
          new Child2().f(); //编译通过
      }
  }

  public class Test0 {
      public static void main(String[] args){
          new Father().f(); //编译通过
          new Child0().f(); //编译通过
          new Child01().f(); //编译通过
          new Child1().f(); //编译通过
          new Child11().f(); //编译通过
          new Child2().f(); //编译通过
      }
  }

  package pkg1;
  public class Child1 extends Father {
      public static void main(String[] args) {
          new Father().f(); //编译不通过
          new Child0().f(); //编译不通过
          new Child01().f(); //编译不通过
          new Child1().f(); //编译通过
          new Child11().f(); //编译不通过
          new Child2().f(); //编译不通过
      }
  }

  public class Child11 extends Father {
      public static void main(String[] args) {
          new Father().f(); //编译不通过
          new Child0().f(); //编译不通过
          new Child01().f(); //编译不通过
          new Child1().f(); //编译不通过
          new Child11().f(); //编译通过
          new Child2().f(); //编译不通过
      }
  }

  public class Test1 {
      public static void main(String[] args) {
          new Father().f(); //编译不通过
          new Child0().f(); //编译不通过
          new Child01().f(); //编译不通过
          new Child1().f(); //编译不通过
          new Child11().f(); //编译不通过
          new Child2().f(); //编译不通过
      }
  }

  package pkg2;
  public class Child2 extends Father {
      public static void main(String[] args) {
          new Father().f(); //编译不通过
          new Child0().f(); //编译不通过
          new Child01().f(); //编译不通过
          new Child1().f(); //编译不通过
          new Child11().f(); //编译不通过
          new Child2().f(); //编译通过
      }
  }

  /* 关系梳理：
    探讨方法；f()
    根源：Father类，pkg0包
    继承关系：Father -> Child0, Child01, Child1, Child11, Child2
    位置关系：Fahter, Child0, Child01, Test0在一个包，Child1, Child11在一个包，Child2在一个包
  */
  /* 结果分析：
    Father编译全通过：
      [1]自身能通过：Father自身具有f()方法
      [2]子对象能通过：父类可以访问子类继承过去的f()方法
    Child0, Child01编译全通过：
      [1]自身能通过：Father的直接子类可以访问f()方法
      [2]父对象能通过：父子同包时，子类实例可以访问基类实例的f()方法
      [3]兄弟对象能通过：父子同包时，子类实例可以访问任意另一子类的f()方法
    Child1, Child11, Child2编译只有自身通过：
      [1]自身能通过：Father的直接子类可以访问f()方法
      [2]父对象不通过：父子不同包时，子类实例不能访问基类实例的f()方法
      [3]兄弟对象不能通过：父子同包时，子类实例不能访问任意另一子类的f()方法
    Test0编译全通过：
      [1]Test1和父类同包，可以访问父类实例、子类实例的f()方法，但自身没有f()方法
    Test1编译全不能通过：
      [1]Test1既不和父类同包，又不是继承关系
  */
  ```
  ```java
  //例2
  package pkg0;
  public class Father {
      protected void f(){};
      public static void main(String[] args){
          new Father().clone(); //编译通过
          new Child0().clone(); //编译通过
          new Child01().clone(); //编译通过
          new Child1().clone(); //编译通过
          new Child11().clone(); //编译通过
          new Child2().clone(); //编译通过
      }
  }

  public class Child0 extends Father {
      public static void main(String[] args){
          new Father().clone(); //编译不通过
          new Child0().clone(); //编译通过
          new Child01().clone(); //编译不通过
          new Child1().clone(); //编译不通过
          new Child11().clone(); //编译不通过
          new Child2().clone(); //编译不通过
      }
  }
          new Child2().clone(); //编译不通过  
      }
  }

  public class Test0 {
      public static void main(String[] args){
          new Father().clone(); //编译不通过
          new Child0().clone(); //编译不通过
          new Child01().clone(); //编译不通过
          new Child1().clone(); //编译不通过
          new Child11().clone(); //编译不通过
          new Child2().clone(); //编译不通过
      }
  }

  package pkg1;
  public class Child1 extends Father {
      public static void main(String[] args) {
          new Father().clone(); //编译不通过
          new Child0().clone(); //编译不通过
          new Child01().clone(); //编译不通过
          new Child1().clone(); //编译通过
          new Child11().clone(); //编译不通过
          new Child2().clone(); //编译不通过
      }
  }

  public class Child11 extends Father {
      public static void main(String[] args) {
          new Father().clone(); //编译不通过
          new Child0().clone(); //编译不通过
          new Child01().clone(); //编译不通过
          new Child1().clone(); //编译不通过
          new Child11().clone(); //编译通过
          new Child2().clone(); //编译不通过
      }
  }

  public class Test1 {
      public static void main(String[] args) {
          new Father().clone(); //编译不通过
          new Child0().clone(); //编译不通过
          new Child01().clone(); //编译不通过
          new Child1().clone(); //编译不通过
          new Child11().clone(); //编译不通过
          new Child2().clone(); //编译不通过
      }
  }

  package pkg2;
  public class Child2 extends Father {
      public static void main(String[] args) {
          new Father().clone(); //编译不通过
          new Child0().clone(); //编译不通过
          new Child01().clone(); //编译不通过
          new Child1().clone(); //编译不通过
          new Child11().clone(); //编译不通过
          new Child2().clone(); //编译通过
      }
  }
  /* 关系梳理：
    探讨方法；clone()
    根源：java.lang.Object类，java.lang包
    继承关系：Object -> Father -> Child0, Child01, Child1, Child11, Child2
    位置关系：Object在一个包，Fahter, Child0, Child01, Test0在一个包，Child1, Child11在一个包，Child2在一个包
  */
  ```
#### (4)重写与重载
1. 重写(*Override*)：**子类对父类允许访问的方法的实现过程进行重新编写(只改变功能代码块)**
   - 本质；方法名与参数相同，代码不同
   - 规则：
     - 前提：继承
     - 可重写内容：**(实例)变量与方法**
     - 参数列表：必须不变
     - 返回类型：必须不变
     - 访问权限：不能比父类中被重写的方法的访问权限更低
     - 异常权限：不能抛出新的检查异常或者比被重写方法申明更加宽泛的异常
     - 不能被重写的方法：`final`方法、`static`方法(**子类可以重新声明，但是与父类独立，不构成多态特性**)<font color='red'>(**详见Java第二部分(面向对象)第3节(继承)第8点(静态成员的继承)**</font>、构造方法、不可视的方法<font color='red'>(**详见Java第二部分(面向对象)第3节(继承)第9点(父类成员修饰符与子类继承、旁类访问的关系)**</font>
     - 父类调用：调用父类中被重写的方法，必须使用关键字`super`
2. 重载(*Overload*)：一个类里面，方法名字相同，而参数不同，返回类型可以相同也可以不同。
   - 本质：方法名相同，参数不同
   - 规则：
     - 前提：同一个类(及其子类，可以认为是广义重载)
     - 可重写内容：**重名的方法**
     - 参数列表：**必须改变(改变方式：参数顺序、参数类型、参数数目等)**
     - 返回类型：可以改变
     - 访问权限：可以改变
     - 异常权限：可以抛出新的检查异常或者比被重写方法申明更加宽泛的异常
     - 不能以返回值类型作为重载函数的区分标准
     - 常用于构造器的重载
```java
/* 改变参数顺序构成重载 */
public String test(int a, String s){
    return s;
}   

public String test(String s, int a){
    System.out.println("test4");
    return s;
}   
```
#### (5)多态
1. 定义：同一个事件发生在不同的对象上会产生不同的结果
2. 语法：
   - 类的多态：`父类 变量名 = new 子类();`
   - 抽象类的多态：`抽象类 变量名 = new 抽象类子类();`
   - 接口的多态：`接口 变量名 = new 接口实现类();`
3. 必要条件：**继承、重写、向上转型**
4. 优点：
   - 消除类型之间的耦合关系
   - 替换性
   - 扩展性
   - 接口性
   - 灵活性
   - 简化性
5. 实现方式：
   - 重写
   - 接口
   - 抽象类
6. 动态绑定与静态绑定
   - 绑定：调用一个方法时，究竟应该调用哪个方法
   - 动态绑定(多态)：在程序运行过程中根据变量当时实际所指的对象的类型动态决定调用的方法
   - 静态绑定(静态方法)：在程序编译过程中确定了这个方法是哪个类中的方法
7. 向上转型：父类引用指向子类对象 **(父类的引用，子类的方法)**
   - [A]**向上转型时，子类单独定义的方法会丢失**
   - [B]**父类对象不能转换为子类引用**
```java
/* 向上转型的理解例子 */
public class Animal {
    public void eat(){
        System.out.print("动物在吃东西");
    }
}

public class Bird extends Animal {
    public void eat(){//重写
        System.out.print("鸟在吃谷子");
    }
    public void drink(){//子类单独定义的方法
        System.out.print("鸟在喝水");
    }
}

public class Cat extends Animal {
    public void eat(){//重写
        System.out.print("猫在吃鱼");
    }
}

public class Main {
    public static void main(String... args){
    //    Bird bird = new Animal();//编译错误[B]
        Animal animal = new Bird();//向上转型
        animal.eat();
    //    animal.drink();//编译错误[A]
        animal = new Cat();//向上转型
        animal.eat();
        /* 输出：鸟在吃谷子猫在吃鱼*/
    }
}
```
```java
/* 向上转型的应用例子(封装+继承+多态) */
public class Educator {

    /* 教育者ID */
    private String id;
    /* 教育者起始工作年 */
    private int startYear;

    /*省略getter与setter方法*/

    /* 实现教育者在学校数据库里的注册 */
    public int register(){
        /*访问学校数据库，并完成注册功能。需要ID, startYear等字段。具体代码略*/
    }
}

public class Teacher extends Educator {...}

public class Student extends Educator {...}

public class Main {
    public static void main(String... args){
        Educator educator = new Student();
        educator.register();
        //通过在父类实现注册方法，子类通过向上转型即可调用，否则需要在教师类与学生类分别写注册方法
    }
}
```
8. 向下转型：父类引用转换为子类引用 **(子类引用对应于子类对象，否则会出错)**
   - [A]向下转型的前提是向上转型了(不能将父对象转型为子对象)
   - [B]向下转型只能转型为本类对象(不能讲子对象转型为兄弟对象)
   - [C]可以借助`instanceof`关键字进行安全转型
   
   [**注意，向下转型编译期不会报错，但是执行时会出现异常`ClassCastException`，因此均建议安全转型**]
```java
/* 向下转型的理解例子(借用先前向上转型理解的类) */
public class Main {
    public static void main(String... args){
        /*向下转型[C]*/
        Animal animal = new Bird();
        if(animal instanceof Bird){
            Bird bird = (Bird)animal;
        }
        else{
            Cat cat = (Cat)animal;
        }
        /*反例子*/
        Animal animal2 = new Animal();
        Bird bird = (Bird)animal2;//执行错误[A]
        Animal animal3 = new Bird();
        Cat cat = (Cat)animal3;//执行错误[B]
    }
}
```
9. **<font color='pink'>(*Hard*)</font>** 继承链的方法调用：
   - 优先级(从高到低)：`this.show(O)`→`super.show(O)`→`this.show((super)O)`→`super.show((super)O)`
   - 原则(向上转型)：
     - 引用类型决定能调用哪些方法
     - 对象(实例)类型决定`this`与`super`
```java
class A {
    public String show(D obj) {
        return ("A and D");
    }
 
    public String show(A obj) {
        return ("A and A");
    }
 
}
 
class B extends A{
    public String show(B obj){
        return ("B and B");
    }
 
    public String show(A obj){
        return ("B and A");
    }
}

class C extends B{
	 
}
 
class D extends B{
 
}

public class Test {
    public static void main(String... args){
        A a1 = new A();
        A a2 = new B();
        B b = new B();
        C c = new C();
        D d = new D();
 
        System.out.println("1--" + a1.show(b));
        System.out.println("2--" + a1.show(c));
        System.out.println("3--" + a1.show(d));
        System.out.println("4--" + a2.show(b));
        System.out.println("5--" + a2.show(c));
        System.out.println("6--" + a2.show(d));
        System.out.println("7--" + b.show(b));
        System.out.println("8--" + b.show(c));
        System.out.println("9--" + b.show(d));
    }
}
/* 分析：
继承关系：C,D→B→A
引用与实例：
    a1为A的引用，A的实例，可以调用show(D)与show(A)
    a2为A的引用，B的实例，可以调用show(D)与show(A)
    b为B的引用，B的实例，可以调用show(B)与show(A)以及继承于A的方法
解答：
  [1]A.show(B)→(无super)→A.show(A)，故输出为：A and A
  [2]A.show(C)→(无super)→A.show(B)↑A.show(A)，故输出为：A and A
  [3]A.show(D)，故输出为：A and D
  [4]B.show(B)→A.show(B)→B.show(A)，故输出为：B and A
  [5]B.show(C)→A.show(C)→B.show(B)↑B.show(A)，故输出为：B and A
  [6]B.show(D)→A.show(D)，故输出为：A and D
  [7]B.show(B)，故输出为：B and B
  [8]B.show(C)→A.show(C)→B.show(B)，故输出为：B and B
  [9]B.show(D)→A.show(D)，故输出为：A and D
答疑：
 - Q:为什么[4]中找到了B.show(B)却跳过？
 - A:因为a2是A的引用，只能执行A的方法，而A的方法没有show(B)。
 - Q:为什么[9]中B没有show(D)却输出？
 - A:因为B是A的子类，继承了show(D)方法。
*/
```
#### (6)接口与抽象类
1. 抽象方法：没有功能代码块的方法，其**实现由子类提供**
   - 抽象方法不能被`final`与`static`修饰
     - `final`：`abstract`需要被子类继承覆盖，否则毫无意义，而 `final` 是禁止继承的，两者相互排斥
     - `static`：`static`是类级别的，与对象实例无关，而 `abstract`需要被继承，与对象实例有关，两者相互排斥
   - 构造方法不能是抽象方法(因为构造方法不能被继承)
2. 虚函数、纯虚函数
   - 虚函数：Java没有虚函数的概念，普通方法就相当于C++的虚函数，**动态绑定是Java的默认行为**。如果Java中不希望某个函数具有虚函数特性，可以加上`final`关键字变成非虚函数
   - 纯虚函数：即抽象方法
3. 抽象类：**不能实例化对象的类**
     - 符号定义：`[访问修饰符] abstract class`
     - 特点：
       - 支持的访问修饰符：`default`，`protected`，`public`
       - 抽象类不能实例化对象，用于将来子类进行扩充
       - 一个类不能同时被`final`与`abstract`修饰
       - 抽象类不一定有抽象方法(可能全是非抽象方法)，有抽象方法一定是抽象类
       - **抽象方法的继承依然需要遵守修饰符继承规则**
       - 任何继承抽象类的子类**必须实现所有父类的抽象方法，除非子类也是抽象类**
        ```java
        //抽象类
        public abstract class Animal {
            //实例变量
            private int longevity;
            public Animal(int longevity){
                this.longevity = longevity;
            };

            abstract void move();
        }

        public class Cat extends Animal {
            public Cat(){
                super(10);//调用父类有参构造方法
            }

            //遵守修饰符继承规则,default可以继承为default,protected,public[如果使用private修饰符会编译错误]
            @Override 
            protected void move(){
                System.out.println("猫在爬");
            }
        }
        ```
   - 抽象类与类的区别：
     - 抽象类不能实例化对象
     - 抽象类可以有抽象方法
     - 一个类继承自抽象类，(除非是抽象子类，否则)必须实现所有抽象方法
4. 接口：抽象方法的集合
   - 符号定义：`[访问修饰符] interface`
   - 特点：
     - 支持的访问修饰符：`default`，`protected`，`abstract`
     - 接口中的成员都是公有的
     - 接口中的方法是抽象的(隐式指定为`public abstract`)
     - 接口中的变量是常量(隐式指定为`public static final`)(因此必须赋初值)
     - *JDK1.8*以后，可以在接口显式指定`static`或`default`，实现静态方法或默认方法的方法体(子类无需重写)
     - 一个接口**可以继承多个接口**
     - 接口不能被实例化
   - 接口的实现：
     - 语法：`implements 接口名[, 其它接口名, ...]`
     - 一个类可以同时实现多个接口
     - 类在实现接口的方法时，需遵守重写方法的所有规则
     - 除非类是抽象类，否则需要实现接口的所有(无方法体的)方法
     - 若实现的接口继承自父接口，还需要实现所有父接口的方法
   - 标记接口：没有包含任何方法的接口
     - 作用：建立一个公共的父接口，使对象拥有某个或某些特权
     - 是否使用标机接口可以用`instanceof`进行类型查询
    ```java
    /*标记接口(事件监听接口)*/
    package java.util;
    public interface EventListener {

    }
    ```
   - 接口与类的区别：
     - 接口不能实例化对象
     - 接口没有构造方法、静态代码块。构造代码块
     - **(已过时)** 接口所有的方法必须是抽象方法
     - 接口不能包含成员变量
     - 接口支持多继承
5. 接口与抽象类的区别：
   - 抽象类中可以有各种类型成员变量，接口只能有`public static final`常量
   - 抽象类可以有静态代码块、构造代码块、构造方法，接口没有
   - 一个类只能继承一个抽象类，但可以实现多个接口
   - **(已过时)** 接口不能静态方法，而抽象类可以有
6. 设计模式探讨：**抽象类是对一种事物的抽象，即对类抽象，而接口是对行为的抽象。抽象类是对整个类整体进行抽象，包括属性、行为，但是接口却是对类局部(行为)进行抽象。抽象类是“是不是”，接口是“有没有”。**
     - 例1：飞机和鸟是不同类的事物，但是它们都有一个共性，就是都会飞。那么在设计的时候，可以将飞机设计为一个类`Airplane`，将鸟设计为一个类`Bird`，但是不能将`飞行`这个特性也设计为类，因此它只是一个行为特性，并不是对一类事物的抽象描述。此时可以**将`飞行`设计为一个接口`Fly`，包含方法`fly()`，然后`Airplane`和`Bird`分别根据自己的需要实现`Fly`这个接口**。
     - 例2：门都有`open()`和`close()`两个动作，此时我们可以定义通过抽象类和接口来定义这个抽象概念：
        ```java
        abstract class Door {
            void open();
            void close();
        }

        interface Door {
            void open();
            void close();
        }
        ```
        但是现在如果我们需要门具有报警的功能，那么该如何实现?下面提供两种思路：
        - 将这三个功能都放在抽象类里面，但是这样一来所有继承于这个抽象类的子类都具备了报警功能，但是有的门并不一定具备报警功能；
        - 将这三个功能都放在接口里面，需要用到报警功能的类就需要实现这个接口中的`open()`和`close()`。但这个类可能根本就不具备`open()`和`close()`这两个功能，比如火灾报警器。

        从这里可以看出，**`Door`的`open()`、`close()`和`alarm()`根本就属于两个不同范畴内的行为，`open()`和`close()`属于门本身固有的行为特性，而`alarm()`属于延伸的附加行为**。因此最好的解决办法是单独**将报警设计为一个接口，包含`alarm()`行为，`Door`设计为单独的一个抽象类，包含`open`和`close`两种行为。再设计一个报警门继承`Door`类和实现`Alarm`接口**。
        ```java
        abstract class Door {
            void open();
            void close();
        }

        interface Alarm {
            void alarm();
        }
        ```
![面向对象编程图例](https://www.runoob.com/wp-content/uploads/2013/12/oopxxx.png)

#### (8)包
1. 包
   - 定义：打包一组相互联系的类型(类、接口、枚举和注释)，为这些类型提供访问保护和命名空间管理的功能
   - 作用：(**相当于C++中的命名空间**)
     - 把功能相似或相关的类或接口组织在同一个包中
     - 避免命名冲突
     - 限定了访问权限
   - 语法：`package pkg1[.pkg2[.pkg3...]]`
   - 保存路径：`pkg1[/pkg2/pkg3/...]/类名.java`
     - 完整类名：`pkg1[.pkg2.pkg3....].类名`
     - 完整文件名：`pkg1[\pkg2\pkg3\...]\类名.java`
   - 缺省包(*default package*)：如果创建类/接口/枚举/注释时不声明包，则会将其放入缺省包中
   - 创建包：
     - 包名建议小写
     - 包声明要在源文件开头
     - 每个源文件只能有一个包声明
   - 导入包(中的类)：
     - 语法：
       - 导入包中一个类：`import package pkg1[.pkg2[.pkg3...]].类名`
       - 导入包中所有类：`import package pkg1[.pkg2[.pkg3...]].*`
     - 导入声明要在包声明之后，类声明之前
     - 每个源文件可以有多个导入
   - 命令行中带包的类的编译与执行方式：
     - (回顾)编译一个类：`javac A.java`
     - (回顾)执行一个类：`java A`
     - 编译一个包的所有类：`javac -d . *.java`
     - 执行主函数：`java 包名.主类名`
2. 源文件声明规则
   - 一个源文件中只能有一个`public`类
     - 原因：Java程序是从一个`public`类的`main`函数开始执行，只有一个`public`类是为了给类装载器提供方便
   - 一个源文件可以有多个非`public`类
   - 源文件的名称应该和`public`类的类名保持一致
   - 在同一源文件中，不能给不同的类不同的包声明
   - 先声明包，再导入包，最后声明类
#### (9)代码块的执行顺序
1. 执行顺序：父类静态成员初始化→父类静态代码块→子类静态成员初始化→子类静态代码块→父类实例变量初始化→父类构造块→父类构造函数→子类实例变量初始化→子类构造块→子类构造函数
2. 若静态成员及静态代码块已加载，则再次实例化该类时不需重复加载
```java
public class Father {
    private int father = Main.getValue(Father.class);
    public static int fat = Main.getStatic(Father.class);
    static {
        System.out.println("父类静态块执行");
    }

    {
        System.out.println("父类构造块执行");
    }

    public Father(){
        System.out.println("父类构造函数执行");
    }
}

public class Child extends Father {
    private int child = Main.getValue(Child.class);
    public static int chi = Main.getStatic(Child.class); 
    static {
        System.out.println("子类静态块执行");
    }

    {
        System.out.println("子类构造块执行");
    }

    public Child(){
        System.out.println("子类构造函数执行");
    }
}

public class Main {
    public static void main(String... args){
        Child child = new Child();
        /*顺次输出[A]*/
        Father fachild = new Child();
        /*顺次输出[B]*/
        Father father = new Father();
        /*顺次输出[C]*/
    }

    public static int getValue(Class<?> clazz) {
    	System.out.println(clazz.getName() + "初始化实例变量执行");
    	return 1;
    }

    public static int getStatic(Class<?> clazz) {
    	System.out.println(clazz.getName() + "初始化静态变量执行");
    	return 1;
    }

    /* 输出结果：
        [A]
            Father初始化静态变量执行
            父类静态块执行
            Child初始化静态变量执行
            子类静态块执行
            Father初始化实例变量执行
            父类构造块执行
            父类构造函数执行
            Child初始化实例变量执行
            子类构造块执行
            子类构造函数执行
        [B]
            Father初始化实例变量执行
            父类构造块执行
            父类构造函数执行
            Child初始化实例变量执行
            子类构造块执行
            子类构造函数执行
        [C]
            Father初始化实例变量执行
            父类构造块执行
            父类构造函数执行
    */
}
```
