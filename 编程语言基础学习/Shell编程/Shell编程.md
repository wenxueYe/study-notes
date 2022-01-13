# Shell编程

> 整理自[尚硅谷-Shell从入门到实战](https://www.bilibili.com/video/BV1hW41167NW)
>
> - 文章发布在：
>
>     - [GitHub资源地址](https://github.com/wenxueYe/study-notes)
>
>     - [CSDN资源地址](https://blog.csdn.net/weixin_44728780/article/details/122464021)

[TOC]


<hr />

### 前置知识 
 - 为什么要学习Shell？
     - 和运维人员更好的交流，看懂运维编写的Shell程序
     - 编写简单的Shell程序来管理集群、提高开发效率
     
 - Shell是什么？
     - Linux的层级：硬件--Linux内核--Shell(cd、ls……)--外层应用程序
     - shell是一个命令行解释器，它接受应用程序/用户的命令，然后调用操作系统内核操相应的硬件。
     - Shell也是一门编程语言，具有易编写、易调试、灵活性强等特点。
     
 - Shell的未来可能替代
     - Python
     
 - Shell解析器

      - ```shell
          # 查看Shell解析器
          sudo cat /etc/shells
          # 执行结果
          /bin/sh
          /bin/bash
          /bin/rbash
          /bin/dash
          ```

      - 常用的Shell解析器

           - /bin/sh
           - /bin/bash

     - sh和bash解析器二者的关系

          - 检验方式

               ```shell
               cd /bin
               ll | grep bash
               ```

          - 结论

               - sh和bash是软连接的关系，也就是说sh最终调用的也是bash

     - 查看系统默认的Shell解析器

          ```shell
          root@iZm5ealqk5qliuszsl3ez3Z:/bin# echo $SHELL
          #执行结果
          /bin/bash
          ```


<hr />

### HelloWorld

- 注意点
    -   脚本格式
        - 脚本以#！/bin/bash开头(指定Shell解析器)
    
- 入门代码

    - 需求：创建一个Shell脚本，输出"Hello,World!"

        - 创建脚本文件

            ```shell
            touch helloworld.sh
            vim ./helloworld.sh
            ```

        - 代码：脚本文件内容

            ```shell
            #!/bin/bash
            echo "Hello,World!"
            ```

        - 执行脚本

            - 方式1：采用bash或sh+脚本的相对路径或绝对路径，不用赋予脚本以+x权限

                ```shell
                bash helloworld.sh
                # 或
                sh helloworld.sh
                ```

                - 正常打印输出
                - 本质上是bash解析器帮忙执行脚本，所以脚本本身不需要执行权限

            - 方式2

                ```shell
                ./helloworld.sh
                ```

                - 执行结果：-bash: ./helloworld.sh: Permission denied
                - 赋予权限(给+x权限即可)：chmod 777 helloworld.sh
                - 再执行结果为正常打印输出
                - 本质上是脚本自己需要执行，所以需要执行权限

    - 脚本的常用执行方式

        - 采用bash或sh+脚本的相对路径或绝对路径(推荐)
        - 直接执行脚本文件

<hr />

### 多命令处理

- 案例需求

    - 在~/shell/目录下创建一个文本文件multi-command-processing.txt文件，并写入文本：“多命令处理测试文本。”

- 代码：

    ```shell
    #!/bin/bash
    cd ~/shell/
    touch multi-command-processing.txt
    echo "多命令处理测试文本。" >> multi-command-processing.txt
    ```

<hr />

### Shell变量

#### 基本语法

- 定义变量
    - 变量=值
        - 注意：等号两边不能留空白符
- 撤销变量
    - unset 变量
- 输出变量
    - echo $变量
- 声明静态变量
    - readonly 变量
        - 注意：静态变量不能被unset
- 提升变量为全局变量
    - export 变量
- 显示当前Shell中所有变量
    - set

####  变量定义规则

- 变量名称即标识符由字母、数字和下划线组成，不能数字开头，并且建议环境变量全大写
- 变量定义两侧不能带空白符
- 在bash解析过程中，变量默认类型都是字符串类型，因此无法进行直接的数值运算
    - 即定义D=1+1，echo $D的结果仍旧为1+1
- 变量的值如果带空白符，则需要使用双引号或单引号括起来。
- 为使得其他Shell程序能够使用定义的变量，需要将变量的作用域提升至全局变量
    - export 变量

#### 分类

- 系统变量
    - 常用系统变量
        - $HOME
        - $PWD
        - $SHELL
        - $USER
        - etc.
- 自定义变量
    - 包括以上的基本语法和变量定义规则部分

#### 特殊变量

- $n

    - 功能描述

        - n为数字，其中$0表示脚本名称，S1-$9代表第1到第9个参数，10以上的参数需要用大括号来包含，如${10}
            - 近似的可以理解为就如同C语言中的命令行参数，即void main(int args,char \*argv)，但是也有不同点。

    - 实操

        ```shell
        # 需求：输出该脚本文件名称、输出参数1和输入参数2的值
        
        # 创建脚本文件
        touch parameter.sh
        vim parameter.sh
        
        # 代码
        #!/bin/bash
        echo "$S0 $1 $2"
        
        # 执行
        bash ./parameter.sh par1 par2
        
        # 结果
        ./parameter.sh par1 par2
        ```

- $#

    - 功能描述

        - 获取所有输入参数个数，常用于循环

    - 实操

        ```shell
        # 需求：输出该脚本文件名称、输出参数1和输入参数2的值
        
        # 创建脚本文件
        touch parameter.sh
        vim parameter.sh
        
        # 代码
        #!/bin/bash
        echo $#
        
        # 执行
        bash ./parameter.sh par1 par2
        
        # 结果
        2
        ```

- $*

    - 功能描述

        - 这个变量代表命令行中所有的参数，$\*把所有参数看成一个整体

    - 实操

        ```shell
        # 需求：输出该脚本文件名称、输出参数1和输入参数2的值
        
        # 创建脚本文件
        touch parameter.sh
        vim parameter.sh
        
        # 代码
        #!/bin/bash
        echo $*
        
        # 执行
        bash ./parameter.sh par1 par2
        
        # 结果
        par1 par2
        ```

- $@

    - 功能描述

        - 这个变量代表命令行中所有的参数，$\*把每个参数区分对待

    - 实操

        ```shell
        # 需求：输出该脚本文件名称、输出参数1和输入参数2的值
        
        # 创建脚本文件
        touch parameter.sh
        vim parameter.sh
        
        # 代码
        #!/bin/bash
        echo $@
        
        # 执行
        bash ./parameter.sh par1 par2
        
        # 结果
        par1 par2
        ```

        

- $?

    - 功能描述

        - 最后一次执行的命令的返回状态。
            - 如果这个变量的值为0，则表示上一个命令正确执行
            - 如果非0（具体是哪个数，由命令自己来决定），则证明上一个命令执行不正确。

    - 实操

        ```shell
        # 演示命令正确执行
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# bash ./parameter.sh par1 par2
        ./parameter.sh par1 par2
        2
        par1 par2
        par1 par2
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# echo $?
        0
        # 演示命令执行失败
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# lqu
        Command 'lqu' not found, did you mean:
        
          command 'lqa' from deb lqa
        
        Try: apt install <deb name>
        
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# echo $?
        127
        ```

<hr />

### 运算符

- 规则

    - 方式1：$((运算式))	or	$[运算式]

    - 方式2：expr    +, -, \*, /, %

        - <span style="color:red">expr运算符之间要有空白符</span>

        ```shell
         root@iZm5ealqk5qliuszsl3ez3Z:~/shell# expr 1+1
        1+1
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# expr 1+ 1
        expr: syntax error
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# expr 1 +  1
        2
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# expr 1 + 1
        2
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# echo $[1+1]
        2
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# echo $[1+ 1]
        2
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# echo $[1 + 1]
        2
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# echo $((1+1))
        2
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# echo $((1+ 1))
        2
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# echo $((1 + 1))
        2
        ```

- 实操

    ```shell
    # 1+1
    expr 1 + 1
    2
    # (2+3)*4	先计算expr 2 + 3,然后用``符号围起来（也就是中间部分），然后再来一层expr,*记得要\*表示
    expr `expr 2 + 3` \* 4
    20
    # 或者（更好理解）
    s=$[(2+3)*4]
    echo $s
    20
    ```

<hr />

### 条件判断

- 基本语法

    - [ condition ]
        - <span style="color:red">condition前后要有空白符</span>
        - 条件非空即为true，[ test ]返回true，[]返回false

- 常用判断条件

    - 两个整数之间比较

        | 符号 | 描述                     |
        | ---- | ------------------------ |
        | -lt  | (less than)小于        |
        | -le  | (less equal)小于等于    |
        | -eq  | (equal)等于              |
        | -gt  | (greater than)大于      |
        | -ge  | (greater equal)大于等于 |
        | -ne  | (not equal)不等于       |
        | =    | 字符串比较               |

    - 文件权限判断

        | 符号 | 描述                     |
        | ---- | ------------------------ |
        | -r  | (read)有读权限 |
        | -w  | (write)有写权限 |
        | -x  | (execute)有执行权限     |

    - 文件类型判断
        | 符号 | 描述                     |
        | ---- | ------------------------ |
        | -f  | (file)文件存在并且是一个常规文件  |
        | -e  | (existence)文件存在 |
        | -d  | (directory)文件存在并且是一个目录   |

- 多条件判断

    - 短路与 &&
    - 短路或 ||
    
- 实操

    ```shell
    # 判断 2 > 3，用echo $?的方式来判断是否执行成功
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# [ 23 -ge 23 ]
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# echo $?
    0
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# [ 23 -ge 23]
    -bash: [: missing `]'
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# [23 -ge 23]
    [23: command not found
    # 判断helloworld.sh是否有执行权限
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# [ -w helloworld.sh ]
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# echo $?
    0
    # 判断~/shell/目录中文件是否存在
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# [ -e ~/shell/helloworld.sh ]
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# echo $?
    0
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# [ -e ~/shell/test.sh ]
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# echo $?
    1
    # 短路与和短路或
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# [ 23 -gt 3 ] && [ 3 -lt 4  ]
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# echo $?
    0
    ```

<hr />

### 流程控制

- if

    - 基本语法

        ```shell
        if [ 条件判断式 ];then
        	程序
        elif [ 条件判断式 ]
        then
        	程序
        fi
        
        # or
        
        if [ 条件判断式 ]
        	then
        		程序
        elif [ 条件判断式 ]
        then
        	程序
        fi
        ```

    - 注意事项

        1. [ 条件判断式 ]，中括号和条件判断式之间必须有空格

        2. if后要有空格

    - 实操

        ```shell
        # 需求：输入一个数字，如果是1，则输出：输入的测试数字为1；如果是0，则输出：输入的测试数字为0；如果是其他，则什么都不输出
        
        # 准备
        touch if.sh
        vim ./if.sh
        
        # 代码
        #!/bin/bash
        if [ $1 -eq 1 ]
        then
                echo "input key is 1"
        elif [ $1 -eq 2 ]
        then
                echo "input key is 2"
        fi
        
        # 执行和结果
        bash ./if.sh 1
        input key is 1
        bash ./if.sh 2
        input key is 2
        bash ./if.sh 3
        [无输出]
        ```

- case

    - 基本语法

        ```shell
        case $变量名 in
        "值1")
        	如果变量的值为1，则执行程序1
        ;;#等价于break;
        "值2")
        	如果变量的值为2，则执行程序2
        ;;
        *)#等价于default
        	如果变量的值都不是以上的值，则执行此程序
        esac
        ```

    - 注意事项

        1. case行位必须为单词 "in"，每一个模式匹配必须以右括号')'结束
        2. 双分号";;"表示命令序列结束，相当于switch语句中的break
        3. 最后的\*)表示默认模式，相当于switch语句中的default

    - 实操

        ```shell
        # 需求：输入一个数字，如果是1，则输出：输入的测试数字为1；如果是0，则输出：输入的测试数字为0；如果是其他，则输出-1
        
        # 准备
        touch case.sh
        vim ./case.sh
        
        # Code
        #!/bin/bash
        
        case $1 in      
        1)
                echo "input key is 1"
                ;;      
        2)      
                echo "input key is 2"
                ;;
        *)      
                echo "input key is -1"
                ;;
        esac    
        
        # 执行和结果
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# bash ./case.sh 1
        input key is 1
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# bash ./case.sh 2
        input key is 2
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# bash ./case.sh 3
        input key is -1
        ```

- for

    - 基本语法

        ```shell
        for(( 初始值;循环控制条件;变量变化 ))
        	do
        		程序
        	done
        
        # Or
        
        
        for 变量 in 值1 值2 值3...
        	do
        		程序
        	done
        ```

    - 注意事项

    - 实操

        ```shell
        # 需求1（基本语法1）：从1加到100
        
        # 准备
        touch for.sh
        vim ./for.sh
        
        # Code
        #!/bin/bash
        sum=0
        for((i=1;i<=100;i++))
        do
                sum=$[$sum+$i]
        done
        echo $sum
        
        # 执行和结果
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# bash ./for.sh 
        5050
        
        
        # 需求2（基本语法2）：打印所有输入参数
        
        # 准备
        vim for2.sh
        
        # Code
        #!/bin/bash
        for i in $*
        do
                echo "input: $i"
        done
        
        # 执行和结果
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# bash ./for2.sh p1 p2 p3
        input: p1
        input: p2
        input: p3
        
        # ======分割==========
        
        # 需求2的$@表达
        #!/bin/bash
        for i in $@
        do
                echo "input: $i"
        done
        # 这样的话，二者的结果是一致的
        
        # ======分割==========
        
        # 需求2的再修改（给$*和$@加上了引号）
        # Code
        for i in "$*"
        do
                echo "input: $i"
        done
        
        for i in "$@"
        do
        
                        echo "input: $i"
        done 
        # 执行和结果
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# bash ./for2.sh p1 p2 p3
        input: p1 p2 p3
        input: p1
        input: p2
        input: p3
        ```

- while

    - 基本语法

        ```shell
        while [ 条件判断式 ]
        do
        	程序
        done
        ```

    - 注意事项

    - 实操

        ```shell
        # 需求：从1加到100
        
        
        # 准备
        vim ./while.sh
        
        # Code
        #!/bin/bash
        i=1
        sum=0
        while [ $i -le 100 ]
        do
                sum=$[$sum+$i]
                i=$[$i+1]
        done
        echo "$sum"
        
        # 执行和结果
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# bash ./while.sh 
        5050
        ```

        

<hr />

### read读取控制台输入

- 基本用法

    - read \[选项\]\[参数\] 参数
        - 选项
        - -p：指定读取值时的提示符
        - -t：指定读取值时的等待时间（以秒为单位）
    - 参数
        - 变量：指定读取值时的变量名

- 实操

    ```shell
    # 需求：提示在7秒内，读取控制台输入的名称
    
    # 准备
    touch read.sh
    vim ./read.sh
    
    # Code
    #!/bin/bash
    read -t 7 -p "in 7s input your name " NAME
    echo $NAME
    
    # 执行和结果
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# bash ./read.sh 
    in 7s input your name YWX
    YWX
    ```

<hr />

### 函数

#### 系统函数

- basename
    - 基本语法

        - basename [string/pathname] [suffix]

    - 功能描述

        - basename命令会删掉所有的前缀包括最后一个'/'字符，然后将字符串显示出来。

    - 实操

        ```shell
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# basename /home/linux/hello.txt .txt
        hello
        ```

- dirname

    - 基本语法

        - dirname 文件绝对路径

    - 功能描述

        - 从给定的包含绝对路径的文件名中去除文件名（非目录部分），然后返回剩下的路径（目录部分）

    - 实操

        ```shell
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# dirname ./helloworld.sh 
        .
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# pwd
        /root/shell
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# dirname /root/shell/helloworld.sh 
        /root/shell
        ```

#### 自定义函数

- 基本语法

    ```shell
    # []为可选
    [ function ] funname[()]
    {
    	Action;
    	[return int;]
    }
    funname
    ```

- 注意事项

    - 必须在调用函数地方之前，先声明函数，shell脚本是逐行解释运行。不会先进行编译。
    - 函数返回值只能通过$?系统变量获得，可以显示加：return返回；如果不加，将以最后一条命令运行结果，作为返回值。return 后跟数值n(0-255)

- 实操

    ```shell
    # 需求：计算输入两个参数的值
    
    # 准备
    vim ./sum.sh
    
    # Code
    #!/bin/bash
    
    function sum()
    {
            s=0;
            s=$[$1 + $2];
            echo $s
    }
    read -p "input your param1: " P1
    read -p "input your param2: " P2
    sum $P1 $P2
    
    # 执行和结果
    root@iZm5ealqk5qliuszsl3ez3Z:~/shell# bash ./sum.sh 
    input your param1: 2
    input your param2: 4
    6
    ```

<hr />

### Shell工具

#### cut

#### sed

#### awk

#### sort

- 功能描述

    - 将文件进行排序并将排序结果标准输出

- 用法

    - sort [选项] (参数)

        - 参数：指定待排序的文件列表

        | 参数 | 描述                     |
        | ---- | ------------------------ |
        | -n   | 依照数值大小排序         |
        | -t   | 以相反的顺序排序         |
        | -t   | 设置排序时使用的分隔字符 |
        | -k   | 指定需要排序的列         |

    - 实操

        ```shell
        # 数据准备
        touch sort.sh
        vim sort.sh
        zs:23:5.2
        ls:32:3.0
        ww:43:2.2
        zl:56:4.2
        qq:78:1.2
        
        # 按照":"分割后的第三列倒序排序
        root@iZm5ealqk5qliuszsl3ez3Z:~/shell# sort -t : -nrk 3 sort.sh
        zs:23:5.2
        zl:56:4.2
        ls:32:3.0
        ww:43:2.2
        qq:78:1.2
        ```

<hr />

### 企业真实面试题

