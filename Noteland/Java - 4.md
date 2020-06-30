# Java

- [Java](#java)
  - [4.Java 常用技术](#4java-%e5%b8%b8%e7%94%a8%e6%8a%80%e6%9c%af)
    - [4.1 正则表达式](#41-%e6%ad%a3%e5%88%99%e8%a1%a8%e8%be%be%e5%bc%8f)
      - [4.1.1 简介](#411-%e7%ae%80%e4%bb%8b)
      - [4.1.2 捕获组](#412-%e6%8d%95%e8%8e%b7%e7%bb%84)
      - [4.1.3 转义](#413-%e8%bd%ac%e4%b9%89)
      - [4.1.4 `Pattern`类](#414-pattern%e7%b1%bb)
      - [4.1.5 `Matcher`类](#415-matcher%e7%b1%bb)
      - [4.1.6 `PatternSyntaxException`类](#416-patternsyntaxexception%e7%b1%bb)
    - [4.2 泛型](#42-%e6%b3%9b%e5%9e%8b)
      - [4.2.1 简介](#421-%e7%ae%80%e4%bb%8b)
    - [4.3 枚举](#43-%e6%9e%9a%e4%b8%be)
    - [4.4 注释](#44-%e6%b3%a8%e9%87%8a)
    - [4.5 序列化](#45-%e5%ba%8f%e5%88%97%e5%8c%96)
    - [4.6 反射](#46-%e5%8f%8d%e5%b0%84)
    - [4.7 语法糖](#47-%e8%af%ad%e6%b3%95%e7%b3%96)
      - [4.7.1 `Stream API`](#471-stream-api)
      - [4.7.2 `Lambda`表达式](#472-lambda%e8%a1%a8%e8%be%be%e5%bc%8f)
    - [4.8 JDBC](#48-jdbc)

## 4.Java 常用技术
### 4.1 正则表达式
#### 4.1.1 简介
- Java正则表达式在`java.util.regex`包中，主要有三个类：
- `Pattern`
- `Matcher`
- `PatternSyntaxException`
#### 4.1.2 捕获组
- 定义：把多个字符当一个单独单元进行处理的方法
- 创建：括号内的字符分组`(...)`
- 编号：从左至右计算其开括号
<pre>
 以((A)(B(C)))为例，有四个组：
     [1]((A)(B(C)))
     [2](A)
     [3](B(C))
     [4](C)
</pre>
- `group(0)`是整个表达式
#### 4.1.3 转义
- 两个反斜杠才能被解析为其他语言中的转义作用(所有`\`用`\\`表示)
#### 4.1.4 `Pattern`类
- 意义：正则表达式的编译表示
- 构造方法
  - `private`，必须通过静态方法获得对象
- 静态方法
  - `public static Pattern compile(String s[, int flags])`：将正则表达式`s`(根据标志`flags`)编译，返回正则模式
    - `flags`为位掩码(*bit mask*)，每一个二进制位代表一种标志。
  ```java
  private static final int ALL_FLAGS = CASE_INSENSITIVE | MULTILINE | DOTALL | UNICODE_CASE | CANON_EQ | UNIX_LINES |LITERAL | UNICODE_CHARACTER_CLASS | COMMENTS;

  private Pattern(String p, int f) {
     if ((f & ~ALL_FLAGS) != 0) {
         throw new IllegalArgumentException("Unknown flag 0x" + Integer.toHexString(f));
     }
     pattern = p;
     flags = f;
     ...
  }
  ```
  - `public static String quote(String s)`：将字符串`s`转换为字面量(所有符号失去特殊意义)
  - `public Matcher matcher(CharSequence cs)`：根据输入字符序列`cs`匹配，返回匹配实例
#### 4.1.5 `Matcher`类
- 意义：对输入字符串进行解释和匹配操作
- 构造方法
  - `private`，必须通过静态方法获得对象
- 静态方法
  - `public static String quoteReplacement(String s)`：将字符串`s`转换为字面量(消除`\`与`$`的特殊含义)
- 成员方法
  - 索引类
    - `public int start([int group])`：返回在以前的匹配操作期间，给定组所捕获的子序列的初始索引(不填则为0)
    - `public int end([int group])`：返回在以前的匹配操作期间，给定组所捕获的子序列的终止索引(不填则为0)
  - 查找类
    - `public boolean lookingAt()`：是否**字符串前缀(从字符串的第一个字符起)是正则表达式的匹配**
    - `public boolean find([int start])`：从`start`起，是否有下一个匹配正则表达式的子序列(不填则为0)
    - `public boolean matches()`：是否**整个字符串都是正则表达式的匹配**
  - 替换类
    - `public Matcher appendReplacement(StringBuffer sb, String replacement)`：将当前匹配子串替换为`replacement`，并且**将替换后的子串以及其之前到上次匹配子串之后的字符串**添加到`sb`中
    - `public StringBuffer appendTail(StringBuffer sb)`：将最后一次匹配工作后剩余的字符串添加到`sb`中
    - `public String replaceAll(String replacement)`：返回用`replacement`替换所有匹配后的字符串
    - `public String replaceFirst(String replacement)`：返回用`replacement`替换替换第一个匹配后的字符串
    - `public static String quoteReplacement(String s)`：返回字符串`s`的字面替换字符串
  - 捕获组类
    - `public String group([int group])`：返回第`group`个捕获组的字符串(不填则为0，即整个匹配子字符串)
    - `public String group(String name)`：返回根据组名`name`捕获的字符串(捕获组命名方式：`(?<NAME>X) `)
    - `public int groupCount()`：返回捕获组数
#### 4.1.6 `PatternSyntaxException`类
- 意义：正则表达式模式中的语法错误
```java
public static void main(String... args){
    String input = "the fat cat sat on the mat.";
    String regex = "(?<!fat\\s)(.at)";
    StringBuffer sb = new StringBuffer();
    Matcher matcher = Pattern.compile(regex).matcher(input);
    while(matcher.find()) {
        System.out.println(matcher.start());
        System.out.println(matcher.end());
        matcher.appendReplacement(sb, "dog");
        System.out.println(sb.toString());
    }
    matcher.appendTail(sb);
    System.out.println(sb.toString());
 /** 系统输出：
 *    4
 *    7
 *    the dog
 *    12
 *    15
 *    the dog cat dog
 *    23
 *    26
 *    the dog cat dog on the dog
 *    the dog cat dog on the dog.
 */
}
``` 
```java
public static void main(String... args){
    String input = "the fat cat sat on the mat.";
    String regex = "(?<name1>c|f)(?<name2>e|a)t";
    StringBuffer sb = new StringBuffer();
    Matcher matcher = Pattern.compile(regex).matcher(input);
    while(matcher.find()) {
        System.out.println(matcher.groupCount());
        for(int i = 0; i <= matcher.groupCount(); i ++) {
            System.out.println(matcher.group(i));
        }
        System.out.println(matcher.group("name1"));
        System.out.println(matcher.group("name2"));
 }
 /** 系统输出：
 *   2
 *   fat
 *   f
 *   a
 *   f
 *   a
 *   2
 *   cat
 *   c
 *   a
 *   c
 *   a
 *   4
 */
}
``` 
### 4.2 泛型
#### 4.2.1 简介
- 定义：在不创建新的类型的情况下，通过泛型指定的不同类型来控制形参具体限制的类型
### 4.3 枚举
### 4.4 注释
### 4.5 序列化
### 4.6 反射
### 4.7 语法糖
#### 4.7.1 `Stream API`
- 流(*stream*)简介
  - 定义：一种高级集合，用来处理集合中的数据
  - 特点：
    - 只能遍历一次
    - 采用内部迭代
  - 操作种类：
    - 中间操作(*map*)
    - 终端操作(*reduce*)
  - 操作过程：创建流$\rightarrow$中间操作$\rightarrow$终端操作
- 流的创建
- 流的操作
#### 4.7.2 `Lambda`表达式

### 4.8 JDBC