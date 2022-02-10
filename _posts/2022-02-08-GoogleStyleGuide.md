---
layout:     post                    # 使用的布局（不需要改）
title:      GoogleStyleGuide               # 标题 
subtitle:   谷歌编程风格指南 #副标题
date:       2022-02-08              # 时间
author:     Fu Xiaohang                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - NLP
    - 自然语言处理
---

# 1 Java

- [Google Java Style Guide](https://www.jianshu.com/p/c0e5a4a896be)
- Alibaba Java开发手册

## 1.1 命名

- 类：大驼峰 Book BookList
- 包：全小写+无下划线 com.nju.booklist
- 常量：全大写+下划线 NUMBER EMPTY_ARRAY
- 其他：小驼峰 stop sendMessage

## 1.2 换行/空行

- 大括号与if、else、for、do及while语句一起使用，即使只有一条语句或是空，也应该把大括号写上

- 对于非空块和块状结构，大括号遵循K&R风格即埃及括号([Egyptian brackets](https://link.jianshu.com?t=http://www.codinghorror.com/blog/2012/07/new-programming-jargon.html))：

  - 左大括号前不换行
  - 左大括号后换行
  - 右大括号前换行
  - 右大括号后换行，若如果后面跟着其他内容如else、catch或逗号，那么后面不换行

  ```java
  return () -> {
      while (condition()) {
          method();
      }
  };
  
  return new MyClass() {
      @Override public void method() {
          if (condition()) {
              try {
                  something();
              } catch (ProblemException e) {
                  recover();
              }
          } else if (otherCondition()) {
              somethingElse();
          } else {
              lastThing();
          }
      }
  };
  ```

- 类内的空行

  - 类内的成员之间有一个空行，如属性和方法之间，方法和方法之间
  - 属性和属性之间的空行是可选的
  - 第一个成员前和最后一个成员后的空行是可选的

- 方法内逻辑分组间使用空行

## 1.3 空格

- if/for/while/switch/do/else/catch等保留字与括号之间必须加空格

- 任何`{`前要加空格

- 在`,` `:` `;` `)`后要加空格，

- 二元操作符两边都要加空格，比如赋值(=)，比较(==, <, >, !=, <>, <=, >=, in, not in)，布尔(and, or, not)

- `//`注释左右两边各一个空格

  ```java
  if (flag == 1) { 
  	System.out.println("world"); // 注释
  } else { 
  	method(args1, args2, args3); // 逗号右边有空格 
  }
  ```

- 小括号和字符之前没有空格，主要指函数

  ```java
  System.out.println("world");
  ```

## 1.4 注释

- Javadoc用于从Java源代码生成HTML格式的API文档

- 类、类属性、类方法的注释必须使用Javadoc规范，使用`/**内容*/`格式，不得使用` // xxx `方式

- 类的注释，分为3段

  - 第1段为概要描述，用一句话或者一段话简要描述该类的作用，以英文句号结束
  - 第2段为详细描述，用一段话或者多段话详细描述该类的作用，每段话都以英文句号结束
  - 第3段为文档标记，**必须添加创建者和创建日期**

  ```java
  /** 
   * Graphics is the abstract base class for all graphics contexts 
   * which allow an application to draw onto components realized on 
   * various devices or onto off-screen images.
   *
   * A Graphics object encapsulates the state information needed 
   * for the various rendering operations that Java supports. 
   * Some important points to consider are that drawing a figure that 
   * covers a given rectangle will occupy one extra row of pixels on 
   * the right and bottom edges compared to filling a figure that is 
   * bounded by that same rectangle.
   *
   * @author Sami Shaio 
   * @since 15 April 2021 
   */ 
  public abstract public class Graphics {
  	...
  }
  ```

- 类属性的注释，一般只包含对变量的简短描述

  ```java
  /**
   * 对变量的描述
   */
  private int debug = 0;
  ```

- 类方法的注释，和类一样，3段，第2段是可有可无的，第3段要包括返回值和参数

  ```java
  /** 
   * Draws as much of the specified image as is currently available 
   * with its northwest corner at the specified coordinate (x, y). 
   * This method will return immediately in all cases.
   *
   * If the current output representation is not yet complete then 
   * the method will return false and the indicated object will be notified as the 
   * conversion process progresses. 
   * 
   * @param img  the image to be drawn 
   * @param x    the x-coordinate of the northwest corner 
   *             of the destination rectangle in pixels 
   * @param y    the y-coordinate of the northwest corner 
   *             of the destination rectangle in pixels 
   * @return     true if the image is completely 
   *             loaded and was painted successfully; 
   *             false otherwise.
   */ 
  public boolean drawImage(Image img, int x, int y){
      ...
  }
  ```

- 方法内部单行注释，使用`//`注释，在被注释语句上方另起一行。方法内部多行注释，使用`/* */`注释，注意与代码对齐

  ```java
  if (x.equals(y)) {
      // 注释
  	System.out.println("true");
  }
  ```

## 1.5 行长度

- 每行不超过100个字符

## 1.6 变量声明

- 一次只声明一个变量，不要使用组合声明，如`int a, b;`
- 不要在一个代码块的开头把局部变量一次性都声明了，而是在第一次需要使用它时才声明
- 局部变量在声明时最好就进行初始化，或者声明后尽快进行初始化

## 1.7 编程实践

- @Override能用则用
- 捕获的异常要做出响应，典型的响应方式是打印日志

# 2 Python

- PEP 8，PEP(Python Enhancement Proposals)，Python增强提案，其中PEP 8是Style Guide for Python Code
- [Google Python Style Guide](https://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/contents/)

## 2.1 命名

- 类：大驼峰
- 异常：大驼峰
- 常量：全大写+下划线
- 其他：全小写+下划线 stop send_message

## 2.2 空行

- 顶级定义(类、函数)之间空两行
- 方法定义之间、类定义与第一个方法之间空一行
- 函数或方法中合适的地方可以空一行

## 2.3 空格

- `,` `;` `:`后面要加空格(除了行尾)，前面不要加

  ```python
  print(x, y)
  ```

- 括号内(大、中、小)不要有空格

  ```python
  spam(ham[1], {eggs: 2}, [])
  ```

- 二元操作符两边都要加空格，比如赋值(=)，比较(==, <, >, !=, <>, <=, >=, in, not in)，布尔(and, or, not)

  ```python
  x == 1
  ```

- 当`=`用于指示关键字参数或默认参数值时, 不要在其两侧使用空格

  ```python
  def complex(real, imag=0.0): return magic(r=real, i=imag)
  ```

- 参数列表，索引或切片的左括号前不应加空格

  ```java
  Yes：
  spam(1)
  dict['key'] = list[index]
  ```

  ```java
  No:
  spam (1)
  dict ['key'] = list [index]
  ```

## 2.4 注释

- 使用文档字符串，能够被pydoc提取，使用三重双引号`""" """`

  - 每个文件应该包含一个许可样板，根据项目使用的许可(例如，Apache 2.0,BSD,LGPL,GPL)，选择合适的样板，其开头应是对模块内容和用法的描述

    ```python
    """A one line summary of the module or program, terminated by a period.
    
    Leave one blank line.  The rest of this docstring should contain an
    overall description of the module or program.  Optionally, it may also
    contain a brief description of exported classes and functions and/or usage
    examples.
    
    Typical usage example:
    
    foo = ClassFoo()
    bar = foo.FunctionBar()
    """
    ```

  - 函数和方法要有文档字符串，包含函数做什么，以及输入和输出的详细描述。Args列出每个参数的名字, 并在名字后使用一个冒号和一个空格，分隔对该参数的描述，如果描述太长超过了单行80字符，使用2或者4个空格的悬挂缩进(与文件其他部分保持一致)，描述应该包括所需的类型和含义。Returns描述返回值的类型和语义，如果函数返回None，这一部分可以省略。Raises列出与接口有关的所有异常。

    ```python
    def fetch_smalltable_rows(table_handle, keys, require_all_keys):
        """Fetches rows from a Smalltable.
    
        Retrieves rows pertaining to the given keys from the Table instance
        represented by table_handle.  String keys will be UTF-8 encoded.
    
        Args:
            table_handle: smalltable; An open smalltable.Table instance.
            keys: Sequence; A sequence of strings representing the key of 
            each table row to fetch.  String keys will be UTF-8 encoded.
            require_all_keys: bool; If require_all_keys is True only
            rows with values set for all keys will be returned.
    
        Returns:
            A dict mapping keys to the corresponding table row data
            fetched. Each row is represented as a tuple of strings. For
            example:
    
            {b'Serak': ('Rigel VII', 'Preparer'),
            b'Zim': ('Irk', 'Invader'),
            b'Lrrr': ('Omicron Persei 8', 'Emperor')}
    
            Returned keys are always bytes.  If a key from the keys argument is
            missing from the dictionary, then that row was not found in the
            table (and require_all_keys must have been False).
    
        Raises:
            IOError: An error occurred accessing the smalltable.
        """
        ...
    ```

  - 类应该在其定义下有一个用于描述该类的文档字符串，如果类有公共属性，那么文档中应该有一个Attributes段，并且应该遵守和函数参数相同的格式

    ```python
    class SampleClass(object):
        """Summary of class here.
    
        Longer class information....
        Longer class information....
    
        Attributes:
            likes_spam: Type; A boolean indicating if we like SPAM or not.
            eggs: Type; An integer count of the eggs we have laid.
        """
    
        def __init__(self, likes_spam=False):
            """Inits SampleClass with blah."""
            self.likes_spam = likes_spam
            self.eggs = 0
    
        def public_method(self):
            """Performs operation blah."""
    ```

- 行注释和块注释，使用`#`，最需要写注释的是代码中那些技巧性的部分，对于复杂的操作，应该在其操作开始前写上若干行注释，对于不是一目了然的代码，应在其行尾添加注释。`#`至少离开代码两个空格，后面空一格

  ```python
  # We use a weighted dictionary search to find out where i is in
  # the array.  We extrapolate position based on the largest num
  # in the array and the array size and then do binary search to
  # get the exact number.
  
  if i & (i-1) == 0:  # True if i is 0 or a power of 2.
  ```

## 2.5 行长度

- 每行不超过80个字符，Python会将圆括号, 中括号和花括号中的行隐式的连接起来 , 可以利用这个特点换行

  ```python
  foo_bar(self, width, height, color='black', design=None, x='foo',
               emphasis=None, highlight=0)
  ```

## 2.6 字符串

- 要么都用双引号，要么都用单引号

## 2.7 import

- 每个导入应占一行

  ```python
  Yes: 
  import os
  import sys
  ```

  ```python
  No:  
  import os, sys
  ```

- 导入应该按照从最通用到最不通用的顺序分组(`__future__` `标准库` `第三方库` `本地代码子包`)，每种分组中, 应该根据每个模块的完整包路径按字典序排序

  ```python
  from __future__ import absolute_import
  from __future__ import division
  from __future__ import print_function
  
  import collections
  import queue
  import sys
  
  from absl import app
  from absl import flags
  import bs4
  import cryptography
  import tensorflow as tf
  
  from book.genres import scifi
  from myproject.backend import huxley
  from myproject.backend.hgwells import time_machine
  from myproject.backend.state_machine import main_loop
  from otherproject.ai import body
  from otherproject.ai import mind
  from otherproject.ai import soul
  ```

## 2.8 main

- 

  ```python
  def main():
      ...
  
  if __name__ == '__main__':
      main()
  ```

  

