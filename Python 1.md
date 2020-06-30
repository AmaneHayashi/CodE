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
- 多行注释：使用``'''`或`"""`
  ```python
  # -*- coding:utf-8 -*-
  # helloworld.py
  '''
  these are 
  all comments
  '''
  def main:
      print('hello world!')

  if __name__ == '__main__'
      main()

  #end
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
    - 一个变量可以通过赋值指向不同类型的对象
    - 在混合计算时，Python会把整型转换成为浮点数
