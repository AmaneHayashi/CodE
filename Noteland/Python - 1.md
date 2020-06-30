# Python

## 1. 基本知识
### 1.1 入门
#### 1.1.1 脚本命令
- `python 文件名.py`：引入解释器执行Python脚本
  - 脚本命令中，`python`也可以写作`python3`
- `python -V`：查看Python版本
  - 注意，`V`是大写
- `python`：进入交互式编程模式`>>>`
  - 可使用`exit()`或`Ctrl+Z`退出交互式编程
- Python 清屏：
    ```python
    import os
    i = os.system("cls")
    ```
#### 1.1.2 语言特点
- **解释型语言**(不用编译，边解释边执行)
- **交互式语言**(在`>>>`后直接执行代码)
- **面向对象语言**(万物皆对象)
- **动态语言**(赋值确定数据类型)
- 易于学习、阅读、维护
- 广泛的标准库
- 互动模式
- 可移植性
- 可扩展性
- 可嵌入式
### 1.2 基本语法
#### 1.2.1 编码方式
- Python3默认采用`UTF-8`编码
- 指定编码方式：`# -*- coding:utf-8 -*-`
#### 1.2.2 标识符
- 第一个字符必须是字母表字母或`_`
- 其它字符可以是字母、数字、下划线
- 大小写敏感
- 可以用中文作变量名
#### 1.2.3 保留字
- 可以通过`keyword.kwlist`(需要导入`keyword`库)输出
- 保留字集合：'False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield'
#### 1.2.4 注释
- 单行注释：以`#`开头
- 多行注释：使用`'''`或`"""`
  ```python
  # -*- coding:utf-8 -*-
  # helloworld.py
  '''
  these are 
  all comments
  '''
  def main():
      print('hello world!')


  if __name__ == '__main__':
      main()

  #end
  ```
- 注释的获取与输出：可以通过`__doc__`成员获取
  ```python
  def a():
    '''这是文档字符串'''
    pass
  print(a.__doc__)
  ```
#### 1.2.5 缩进、空行
- 缩进
  - Python中，不需要使用`{}`
  - 程序缩进必须严格符合标准，否则会报错
- 空行
  - 函数之间或类的方法用空行，类与函数入口之间也用空行分隔
  - 空行不是Python语法的一部分，用于分隔不同含义的代码
#### 1.2.6 多行语句
- 如果语句很长，可以使用反斜杠(`\`)实现多行语句
- 在列表(`[]`)，元组(`()`)，字典(`[]`)中的多行语句不用反斜杠
    ```python
    total = item1 + \
            item2 + \
            item3
    total = ['item1', 'item2',
            'item3']
    ```
#### 1.2.7 分号
- Python代码中不需要分号(`;`)即可以表示语句结尾
- 如果想在同一行使用多条语句，可以用`;`分隔
#### 1.2.8 代码组与子句
- 缩进相同的一组语句构成代码组
    ```python
    if expression : 
        suite
    elif expression : 
        suite
    else :
        suite
    ```
#### 1.2.9 最基本的函数
- `print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)`函数：用于打印输出
  - 参数简介
    - `*objects`为输出的对象，多个对象用逗号`(,)`分开
      ```python
      a = 1
      b = 'python'
      print(a, b)
      # 输出为1 python
      ```
    - `sep`为输出对象的间隔符号，默认是空格`' '`
      ```python
      print(a, b, sep=',')
      # 输出为1,python
      ```
    - `end`为结尾符号，默认是换行符`\n`
      ```python
      print(a, end=',')
      print(b, end='.')
      # 输出为1,python.
      ```
    - `file`为写入的对象，设置后将输出写入到指定文件中
    - `flush`为是否缓存，如果为`True`则强制刷新输出流
      - 应用场景：打开一个文件， 向其写入字符串， 在关闭文件`f.close()`之前，打开文件是看不到写入的字符的。要想在关闭之前实时的看到写入的字符串，应该用`flush=True`. 
  - 命令行使用
    - 使用`print(objext.__doc__)`可以获得文档字符串
      ```python
      print(max.__doc__)
      ```
- `help(object)`函数：用于获得相关帮助信息
  - ``object`为需要获得帮助信息的对象
  - 命令行使用
    - 使用`help()`函数显示`-- More --`时，可以通过按`:q`键退出
#### 1.2.10 导入
- `import 模块名`：导入整个模块(*module*)
    ```python
    import time
    time.sleep(1)
    ```
- `import 模块名 as 别名`：导入整个模块(*module*)并设置别名
    ```python
    import time as t
    t.sleep(1)
    ```
- `from 模块名 import 函数名[, 函数名]`：导入模块的一个(多个)函数
    ```python
    from time import sleep
    sleep(1)
    ```
- `from 模块名 import *`：导入模块的全部函数
    ```python
    from time import *
    sleep(1)
    ```
### 1.3 基本数据类型
#### 1.3.1 变量赋值
- 变量不需要声明，使用前必须赋值
- 使用`=`进行赋值
- 支持多个变量同时赋值，如：`a = b = c = 1`或`a, b, c = 1, 2, 'amane'`
#### 1.3.2 标准数据类型
- 数据类型简介
  - 不可变数据(3个)：`Number`(数字)，`String`(字符串)，`Tuple`(元组)
  - 可变数据(3个)：`List`(列表)，`Dict`(字典)，`Set`(集合)
- 变量类型查询
  - `type(object)`：返回`object`对应的类
    ```python
    a = 1
    print(type(a))
    # 输出：<class 'int'>
    ```
  - `isinstance(object, type_tuple)`：返回`object`对应的类是否在元组`type_tuple`中
    ```python
    a = 1
    print(isinstance(a, int), end = ',')
    print(isinstance(a, (float, bool, complex)))
    # 输出：True,False 
    ```
  - `type()`与`isinstance()`的区别：
    - `type()`不认为继承的子类是一种父类类型，而`isinstance()`认为继承的子类是一种父类类型
        ```python
        class A: pass
        class B(A): pass
        print(isinstance(B(), A), end = ',')
        print(type(B()) == A)
        # 输出：True,False 
        ```
- 变量创建与删除
  - 创建变量：`var[, var2[, var3[..., varN]]] = value[, value2[, value3[..., valueN]]]`
  - 删除变量：`del var1[, var2[, var3[..., varN]]]`
    ```python
    a = 1
    print(a)
    del a
    print(a)
    # 输出：1, 报错(name 'a' is not defined)
    ```
### 1.4 解释器
- 将`bin`路径添加到操作系统的环境变量中，就可以通过 shell终端输入命令来启动Python
- Python编程模式分为交互式编程、脚本式编程
- Python解释器有CPython(官方)，IPython，Jython，PyPy
### 1.5 运算符
> `4 + 5 = 9`，`4`与`5`为操作数，`+`为运算符
#### 1.5.1 算术运算符
- `+`：加法
- `-`：减法
- `*`：乘法
- `/`：除法
- `%`：取模
- `**`：求幂
- `//`：地板除(除法结果下取整)
#### 1.5.2 比较运算符
- `==`：等于
- `!=`：不等于
- `>`：大于
- `<`：小于
- `>=`：大于等于
- `<=`：小于等于
#### 1.5.3 赋值运算符
- `=`：赋值
- `+=`：加赋值
- `-=`：减赋值
- `*=`：乘赋值
- `/=`：除赋值
- `%=`：模赋值
- `**=`：幂赋值
- `//=`：地板除赋值

**Python中没有自增自减运算符！**
#### 1.5.4 位运算符
- `&`：按位与
- `|`：按位或
- `^`：按位异或
- `~`：按位取反
- `<<`：左移位
- `>>`：右移位(带符号)
#### 1.5.5 逻辑运算符
- `and`：与(只要遇到假值就返回那个假值,如果表达式结束依旧没有遇到假值,就返回最后一个值)
- `or`：或(只要遇到真值就返回那个真值,如果表达式结束依旧没有遇到真值,就返回最后一个值)
- `not`：非(对于`not x`，如果`x`为`True`，返回`False`，否则返回`True`)
- 注意事项：
  - Python的逻辑运算符可以不止返回`True`与`False`
  - 只有`0`、`''`、`[]`、`()`、`{}`、`None`，其余任何对象均为真
  ```python
  a = 10 # True
  b = 20 # True
  print(a and b) 
  print(a or b)
  print(not(a and b)
  # 分别输出为20, 10，False
  # 理解：在最后一个中，a and b 结果为20，作为布尔值传入not()时，认为是True
  ```
#### 1.5.6 成员运算符
- `in`(如果在指定的序列中找到值返回`True`，否则返回`False`)
- `not in`(如果在指定的序列中找不到值返回`True`，否则返回`False`)
  ```python
  a = 10
  list = [1, 2, 3, 4, 5]
  print(a in list)
  a = 3
  print(a not in list)
  # 分别输出为False, False
  ```
#### 1.5.7 身份运算符
- `is`(如果两个标识符引用自一个对象返回`True`，否则返回`False`)
- `is not`(如果两个标识符不引用自一个对象返回`True`，否则返回`False`)
- 注意事项：
  - python中，判断是否引用自一个对象，可以通过`id()`函数获得对象内存地址，故`a is b`等价于`id(a) == id(b)`
  - 脚本与交互结果不同
  ```python
  a = 20
  b = 20
  print(a is b)
  a = 200
  b = 200
  print(a is b)
  ```
#### 1.5.8 运算符优先级
|                  运算符                  |       描述        |
| :--------------------------------------: | :---------------: |
|                   `**`                   |       求幂        |
|              `~` `+@` `-@`               |  按位取反,正负号  |
|             `*` `/` `%` `//`             | 乘,除,取模,地板除 |
|                 `+` `-`                  |     加法,减法     |
|                `>>` `<<`                 |    移位运算符     |
|                   `&`                    |      按位与       |
|                 `^` `\|`                 |     位运算符      |
|            `<=` `<` `>` `>=`             |  大于小于运算符   |
|                `==` `!=`                 |    等于运算符     |
| `=` `%=` `/=` `//=` `-=` `+=` `*=` `**=` |    赋值运算符     |
|              `is` `is not`               |    身份运算符     |
|              `in` `not in`               |    成员运算符     |
|             `not` `and` `or`             |    逻辑运算符     |

### 1.6 条件语句与循环结构

### 1.7 基本数据类型



- `Number`
  - 支持`int`，`float`，`bool`，`complex`
  - 数值运算
    - 加法：`+`，`5 + 4 = 9`
    - 减法：`-`，`5 - 4 = 1`
    - 乘法：`*`，`5 * 4 = 20`
    - 除法：`/`，`5 / 4 = 1.25`
    - 地板除：`//`，`5 //4 = 1`
    - 取余：`%`，`5 % 4 = 1`
    - 乘方：`**`，`5 ** 4 = 625`
  - 复数
    - 复数由实部与虚部构成
    - 表示方法：`a + bj`或`complex(a, b)`
  - 其它规则
    - **一个变量可以通过赋值指向不同类型的对象**
      ```python
      a = 1
      a = 'str'
      # 不报错
      ```
    - 在混合计算时，Python会把整型转换成为浮点数
    - 表达次方时，可以借助`E`或`e`表示：`32.3e+18`，`70E-12`
    - 如果整数部分为0，可以缩写为`.小数`：`.2`，`.1+.2j`
- `String`
  - 使用`'`或`"`括起来，并用`\`转义特殊字符
  - Python没有字符类型，一个字符就是长度为1的字符串
  - Python不支持替换字符串中的字符(可以替换引用)
    ```python
    a = 'hello'
    a[0] = 'm' # 报错
    a = 'world' # 通过
    ```
  - 常用功能
    - 输出字面量：在字符串前添加`r`
      ```python
      print('amane\nhayashi', end=' ')
      # 输出为amanehayashi
      print(r'amane\nhayashi')
      # 输出为amane\nhayashi
      ```
    - 字符串连接：使用`+`
      ```python
      a = 'hello'
      print(a + 'world')
      # 输出为helloworld
      ```
    - 字符串重复：使用`*`
      ```python
      a = 'hello'
      print(a * 2)
      # 输出为hellohello
      ```
    - 字符串截取：使用`[start:end]`
      - 默认：截取`[start, end)`范围的字符
      - `end < 0`：截取从`start`到倒数第`end`个字符
      - `[:end]`：截取从开头到`end`
      - `[start:]`：截取从`start`到末尾
      - `[start]`：截取第`[start]`位的字符

> 数据之间的转换也放在各自数据类型介绍
> 
> Python负数的二进制表示没有补码(没有位数限制)