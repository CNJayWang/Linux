# Linux Shell
## Shell简介
 	Sell又叫壳，操作系统底层有个kernel它是用来把操作系统的上层应用需求转化成底层需求。比如说底层系统磁盘的读写，网络的连接，进程的调度，内存的管理，各种硬件的驱动等。但是出于安全考虑我们是无法对kernel直接操作的，这时候就需要一个shell(壳)，把用户的信息解释传递给kernel。

### 两种不同的shell
	1.CLI Comand Line Interface 
		命运行形式的shell通过指令传递信息，也是我们要介绍的Linux Shell
	2.GUI Graphical User Interface
		图形化的shell，也是当今主流的形式，通过点击拖拽等操作，简单方便。

### Linux Shell
	对于linux来说，GUI只是上层的辅助，大多数能还是要通过CLI。GUI能完成的CLI基本完成，而CLI能完成的GUI未必能完成。所以要用好Linux系统必须要用好CLI。

### 几种Cli Shell
#### bash
	bash是Linux默认的标准shell,它由Brian Fox 和Chet Ramey共同完成，是BourneAgain Shell的缩写，内部命令一共有40个。
#### ash
	ash shell 是由kenneth Almquist编写的,含有24个命令，占有的Linux的内部资源很少，所以用起来很方便。
#### csh
	csh 是由William Joy为代表的共计47位作者编成，共52个命令。
#### ksh
	ksh 是Korn shell的缩写，由Eric Gisin编写，一共有42条命令。
#### sh
	sh 由Steve Bourne开发，是Bourne Shell的缩写，是Unix标准默认的shell

## Shell与编程语言
	大体上，可以将编程语言分为两类：编译型语言和解释型语言
### 编译型语言
	编译型语言是先将源代码转换成目标代码，也就是编译。运行程序时，直接运行目标代码，目标代码很接近计算机底层语言。这里应该是汇编代码，所以执行效率很高。这就是编译语言的优点，但是编写一个简单的程序需要大量代码。
    这些语言有C/C++、Java、Pascal、Ada、Fortan。
### 解释型语言
	解释型语言也叫脚本语言。这类程序时运行执行时，解释器读取源代码，并将其转化成目标代码，再由计算机运行。由于么次执行都需要编译成目标代码，所以效率下降。
    使用脚本语言的好处是，他们更比编译型语言跟高层，更接近自然语言，所以编写更加简单。往往很复杂的C程序用脚本花费很少的时间和代码就能完成，唯一的不足就是运行效率，但现在但计算机的性能越来越快，基本上可以和编译型的程序相媲美了。
	这些语言有Python、Perl、Lua、Ruby、Shell
    所以说Linux Shell 是解释型语言，我们可以用Shell编写一些程序，像其他解释型语言编程一样。
### Shell 用在何处
	Shell通过了POSIX的标准化的，所以基本上写一次就可以用在很多系统上。
#### Shell 脚本的三大优点
* 简单性：Shell是一个解释型语言，是一个高级语言，可以通过简洁的语言表达操作
* 可移植性：符合POSIX的标准，所以可以做到无须修改就能在很多地方运行
* 简单的开发：短时间就可以开发功能强大的脚本程序

#### 不适合用shell完成的功能
1. 数学计算类的操作，如浮点、算术、这类数学计算更适合c/c++这类编译型的语言，因为它能更好的运用计算机的底层资源。
2. 跨平台、复杂的应用
3. 直接和计算机底层交互的操作，因为Shell是基于kernel的。
4. 需要图形化的操作也不适合。
5. 需要I/O或socket网络编程的

## Shell 编程

### Hello World
```
#!/bin/bash
echo "Hello World !"
```
这就是一个shell脚本
`!#`是一个约定的标记，它告诉系统运行这个脚本需要用什么的解释器。`echo`是向窗口输出文本。

#### 两种运行shell的方法
##### 可执行程序的方式
代码保存，扩展名和C代码一样。不影响代码大执行，但最好用能表意的扩展名，增强可读性么，毕竟程序不是给只给你一个看么，约定俗成，都用`.sh`扩展名。

执行时应到脚本的目录运行`./xxx.sh`，因为解释器需要在PATH中寻找这个文件，`./`是在当前PATH中找。

这种方式运行就是在第一行已经定义好了解释器，单文件文件路径一定别弄错了。

#####把脚本文件直接作为解释器的参数
这种方式是直接运行解释器，并脚本文件作为参数。如：
```
/bin/bash xxx.sh
/bin/sh xxx.sh
/bin/ash xxx.sh
```
这样运行脚本就是不需要在脚本第一行定义运行的解释器了。


###变量

####定义变量

有C、Java编程基础的应该会容易定义Shell中的变量，Shell的变量名也遵循相似的规则
* 首字符必须为（a-z,A-Z）
* 中间不能有空格，可以使用下划线
* 不能使用标点符号
* 是能适应系统的保留关键字

变量定义举例：
```
username="Jay"
email="jay.wang.liu@gmail.com"
```
#### 变量的使用
使用一个变量只需要在变量多前面加上美元符号`$`就可以了，如：
```
usrname="Jay"
email="jay.wang.liu@gmail.com"
echo $username
echo $email
```
你可以使用`$var`或`${var}`的方式使用变量，这都是可以的，不过我觉得用最好用第二种，因为代码多了，或者用在字符串中第二种可以使变量与其他代码隔离,不会使解释器识别出错，例如：
```
firstName="Jay"
echo "Hello,${firstName}Wang!"
echo "Hello,$firstNameWang"
```
#### 变量的重新定义
已知的变量，可以重新定义，例如：
```
username="JayWang"
password="123456"
echo "${password} is ${username}'s old password "
password="abc123456"
echo "${password} is ${username}'s new password"
````
#### 只读变量
熟悉的java的人应该知道java中的`final static`的变量一旦定义只能读取不能修改，`shell`中使用`readonly`来表明这个变量为只读变量。例如下面多例子的更改一个`readonly`讲在运行时报错。
```
#!/bin/bash
username="Jay"
readonly username
username="JayWang"
echo ${username}
```
运行结果如下：
```
test.sh: line 3: username: readonly variable
```
#### 删除变量
使用unset命令可以删除变量
```
unset var_name
```
变量删除后不能在使用了，当然了`unset`不能删除一个`readonly`变量。

#### 变量的作用域
 1. 局部变量：也就是只在当前脚步代码中有效
 2. 环境变量：环境变量，也就是全局变量，相对于解释器的，所有的shell脚本和程序都能访问

#### Shell特殊变量
 我们在介绍定义一个shell变量时只能包含字母、数字、下划线，是因为有些包含其他字符的变量时系统的保留多特殊变量。

例如，0代表当前文件名，下面的代码：
```
echo ${0}
```
运行结果：输出了当前所执行脚本的文件名
```
test.sh
```
下面总结了一些特殊变量名

变量 |含义
------------|---------
0|当前执行脚本的文件名
n|传递给脚本或函数的参数。n是一个数字，表示第几个数字。例如：`$2`表示第二个参数
#|传递给脚本或函数的参数个数
*|传递给脚本或函数的所有参数
@|传递给脚本或函数的所有参数。被双引号（" ")包含时，与`*`会不同
?|上个命令的退出状态，或函数的返回值
$|当前Shell的进程id.对于Shell脚本，就是这些脚本所在的进程ID。

`${@}`__与__`${?}`**的区别**
它两都是表示传递给脚本或函数的所有参数，但区别是当包含在`" "`中情况就不同了，其他都是一样的。当以`"${*}"`多个参数会这样输出：`"${1}${2}{3}..."`，而`"${@}"`则会这样输出：`"${1}""${2}""${3}"....`,是分开输出的。

`${?}`__退出状态__
$? 可以获取上一个命令的推出状态，也就是上一个命令执行后的返回值。熟悉Linux命令的同学，应该知道管道，我们可以以一个命令的执行结果作为另一个命令的执行参数，如`ps -ef|grep mysql`。这里应该就是`${?}`发挥的作用吧。


#### 命令行参数

运行脚本时传递给脚本的参数，称为命令行参数。命令行参数用`$n`表示，在上一节中我已经介绍了一种Shell的特殊变量。不懂的可以看上面的图表。
下面是我写的一个例子，展示向脚本传输参数。
```
#!/bin/sh
echo "Shell Filename is:${0} "
echo "First Param :${1}"
echo "Second Param :${2}"
```
运行结果：
```
./test2.sh "Hello" "world"
Shell Filename:./test2.sh
First Param: Hello
Second Param: world
```
#### shell中注释
shell中没有多行注释，只能一行一行注释。注释以`#`开头，当解释器读到带`#`就会忽略
```
#----------------------
#Author:Jay
#Email:jay.wang.liu@gmail.com
#Create Date 1/1/2016 8:00
#这些都是注释
```

### Shell替换
如果表达式中包含特殊字符，Shell将会进行替换。例如在双`" "`中变量就是一种替换，转译字符也是一种替换。
举个例子：
```
#!/bin/sh
username="Jay"
echo -e "Hello ${username} \n"
```
运行结果：
```
Hello Jay
```
这里`-e`时表示对转义字符进行替换，如果不用就会原样输出：
```
Hello Jay \n
```
一些转义字符如下：

转义字符|含义
-----|------
\\\ |反斜杠
\\a|警报，响铃
\\b|退格
\\f|换页
\\n|换行
\\r|回车
\\t|水平制表符
\\v|垂直制表符
可以使用`echo -E`命令静止转义，默认也是不转义对。

#### 命令替换
命令替换是让shell先执行命令然后保存执行结果到一个变量，在稍后需要到地方进行处理。
命令替换的语法。
```
`command`
```
这里`command`是在反引号里面不是单引号。
例子：
```
DATE=`date`
echo $DATE
WHO=`who`
for w in $WHO; do
	echo $w
done

```
运行结果如下：
```
2016年 1月 3日 星期日 02时28分16秒 CST
Jay
console
Dec
27
03:48
Jay
ttys000
Jan
2
16:47
```
#### 变量替换
变量替换式根据变量的状态（是否为空、是否定义等）来改变它的值
可以使用的变量替换形式

形式|说明
----|---
${var}|变量本来的值
${var:-word}|如果变量var为空或删除(unset)，返回word,但不改变var的值
${var:=word}|如果变量var为空或删除(unset)，返回word,并将var对值设置为word
${var:?message}|如果变量 var 为空或已被删除(unset)，那么将消息 message 送到标准错误输出，可以用来检测变量 var 是否可以被正常赋值。若此替换出现在Shell脚本中，那么脚本将停止运行
${var:+word}|如果变量 var 被定义，那么返回 word，但不改变 var 的值。

例子：
```
echo ${var:-"Variable is not set"}
echo "1 - Value of var is ${var}"

echo ${var:="Variable is not set"}
echo "2 - Value of var is ${var}"

unset var
echo ${var:+"This is default value"}
echo "3 - Value of var is $var"

var="Prefix"
echo ${var:+"This is default value"}
echo "4 - Value of var is $var"

echo ${var:?"Print this message"}
echo "5 - Value of var is ${var}"
```
运行结果：
```
Variable is not set
1 - Value of var is
Variable is not set
2 - Value of var is Variable is not set

3 - Value of var is
This is default value
4 - Value of var is Prefix
Prefix
5 - Value of var is Prefix
```
### 运算符
Bash 支持很多运算符，包括算数运算、关系运算、布尔运算、字符串运算、文件检测运算
原生的bash不支持简单的数学运算，但可以通过其他的命令来实现，例如：awk、expr

expr表达式计算，可以完成表达式的的求值操作
例如，求两数相加：
```
#!/bin/bash
result=`expr 1 + 2`
echo "The result is:${result}"
```
脚本的运行结果：
```
The result is:3
```
注意事项：

* 表达式和运算符之间要有空格，例如`1+2`是不对的，必需写成`1 + 2`
* 完整的表达式是一个`command`,所以要被｀ ｀包含。

#### 算术运算符
算术运算符列表：

运算符|说明|举例
-----|----|-------
+|加法|｀expr $a + $b｀
-|减法| ｀expr $a - $b｀
*|乘法|｀expr $a \* $b｀这里乘的运算符需要用`\`转义
/|除法|｀expr $a / $b｀
%|取余|｀expr $a % $ b｀
=|赋值|a=$b
==|相等。|[$a == $b]
!=|不相等|[$ != $b]
注意：条件表达式必须放在`[ ]`之间，并且之间要有空格。`[ $a == $b]`。

#### 关系运算符
关系运算符只支持数字，不支持字符串，除非字符串的值是数字。
关系运算的一个脚本例子：
```
#!/bin/bash
a=10
b=20

#相等
if [ $a -eq $b ]
then 
    echo "$a -ea $b:a is equal to b"
else
    echo "$a -eq $b:a is not eual b"
fi

#不相等
if [ $a -ne $b ]
then 
    echo "$a -ne $b:a is not equal to b"
else 
    echo "$a -ne $b:a is equal to b"
fi

#大于
if [ $a -gt $b ]
then 
    echo "$a -gt $b:a is greater than b"
else
    echo "$a -get $b:a is not greater than b"
fi

#小于
if [ $a -lt $b ]
then
     echo "$a -lt $b:a is less than b"
else
    echo "$a -lt $b:a is not less than b"
fi

#大于等于
if [ $a -ge $b ]
then 
    echo "$a -ge $b:a is  greater or equal to b"
else
    echo "$a -ge $b:a is greater or equal to b"
fi

#小于等于
if [ $a -le $b ]
then
    echo "$a -le $b:a is less or equal to b"
else
    echo "$a -le $b:a is not less or equal to b"
fi
```
运行结果如下：
```
10 -eq 20:a is not eual b
10 -ne 20:a is not equal to b
10 -get 20:a is not greater than b
10 -lt 20:a is less than b
10 -ge 20:a is greater or equal to b
10 -le 20:a is less or equal to b
```
 关系运算符列表
 
 运算符|说明|举例
 -----|----|-----
 -eq|检测两个数是否相等|[ $a -eq $b ]
 -ne|检测两个数不相等|[ $a -ne $b ]
 -gt|检测左边的数大于右边的数|[ $a -gt $b ]
 -lt|检测左边的数小于右边的数|[ $a -lt $b ]
 -ge|检测左边的数大于等于右边的数|[ $a -ge $b ]
 -le|检测左边的数小于等于右边的数|[ $a -lr $b ]
 
#### 布尔运算符
脚本样例：
```
#!/bin/bash
a=10
b=20
c=30

#!非运算，也叫取反
if [ $a != $b ]
then
	echo "$a != $b:ture"
else
	echo "$ != $b:fasle"
fi

#-a and 运算
if [ $a -gt $b -a $a -lt $c ] 
then
	echo "$a -gt $b -a $a -lt $c:true"
else
	echo "$a -gt $b -a $a -lt $c:false"
fi

#-o or 运算
if [ $a -gt $b -o $a -lt $c ]
then
	echo "$a -gt $b -o $a -lt $c:true"
else 
	echo "$a -gt $b -o $a -lt $c:false"
fi
```

运行结果：
```
10 != 20:ture
10 -gt 20 -a 10 -lt 30:false
10 -gt 20 -o 10 -lt 30:true
```

布尔运算符列表：

运算符|说明|举例
----|-----|-----
!|非运算，也可取反|[ !false ]返回ture
-o|或运算|[ false -o ture ]返回true
-a|与运算|[ false -a true ]返回false

#### 字符串运算符
脚本例子：
```
#!/bin/bash
a="abc"
b="def"
c=""

#=判断字符串相等
if [ $a = $b ] 
then 
	echo "$a = $b:ture"
else
	echo "$a = $b:false" 
fi 

# !=判断字符串不相等
if [ $a != $b ] 
then
	echo "$a != $b:true"
else
	echo "$a != $b:false"
fi

#-z检测字符串的长度是否为0，为0返回ture
if ［ -z $a ］ 
then 
 	echo "-z $a:true"
 else
 	echo "-z $a:false"
 fi

 #-n 检测字符串是否为0,为0返回false
 if ［－n $a ］
 then
 	echo "-n $a:true"
 else
 	echo "-n $a:false"
 fi
 
 #str 检测字符串是否为空
 if [ str $c ] 
 then
 	echo "str $c:true"
 else
 	echo "str $c:false"
 fi
```
运行结果：
```
abc = def:false
abc !=def:ture
-z abc:false
-n abc:true
str  :ture
```

字符串运算符列表

运算符|说明|举例
-----|----|-----
=|字符串相等运算｜[ $a = $b]:false
!=|字符穿不相等运算｜[ $a != $b ]:ture
-z|字符长度为0检测，为0:true｜[ -z $a ]:false
-n|字符串长度为0计算，为0:false｜[ -n $a ]:ture
str|字符串为空计算，空：ture｜[ str $c ]:ture

####文件测试运算符
文件测试运算符用于检测Linux文件的各种属性。下面有一个脚本展示文件运算符。
```
#!/bin/bash
file="/vagrant/Shell.md"

#-b检测文件是否是块设备文件，如果是，返回ture
if [ -b $file ]
then
	echo "-b ${file}:ture"
else
	echo "-b ${file}:false"
fi

#-c检测文件是否为字符设备文件，如果是，返回ture
if [ -c $file ]
then
	echo "-c ${file}:ture"
else
	echo "-c ${file}:false"
fi

#-d检测文件是否为目录，如果是返回ture
if [ -d $file ]
then
	echo "-d ${file}:ture"
else
	echo "-d ${file}:false"
fi

#-f检测文件是否是普通文件（既不是目录，也不是设备文件），如果是返回ture
if [ -f $file ]
then
	echo "-f ${file}:ture "
else
	echo "-f ${file}:false"
fi

#-g检测文件是否设置了SGID位，如果是，则返回ture
if [ -g ${file} ]
then
	echo "-g ${file}:ture"
else
	echo "-g ${file}:false"
fi

#-k检测文件是否设置了粘着位（Sticky Bit）,如果是，返回ture
if [ -k ${file} ]
then
	echo "-k ${file}:ture"
else
	echo "-k ${file}:false"
fi

#-p检测文件是否具有管道，如果是，返回ture
if [ -p ${file} ]
then
	echo "-p ${file}:ture"
else
	echo "-p ${file}:false"
fi

#-u检测文件是否设置了SUID位，如果是，返回 ture
if [ -u ${file} ]
then
	echo "-u ${file}:ture"
else
	echo "-u ${file}:false"
fi


#-r检测问价是否为可读，如果是返回ture
if [ -r ${file} ]
then
	echo "-r ${file}:ture"
else
	echo "-r ${file}:false"
fi

#-w检测文件是否为可写，如果是就返回ture
if [ -w ${file} ]
then
	echo "-w ${file}:ture"
else
	echo "-w ${file}:false"
fi

#-x检测文件是否为可执行文件，如果是就返回ture
if [ -x ${file} ]
then
 	echo "-x ${file}:ture"
else
	echo "-x ${file}:false"
fi

#-s检测文件是否为空（文件大小是否大于0）如果是返回ture
if [ -s ${file} ]
then
	echo "-s ${file}:ture"
else
	echo "-s ${file}:false"
fi

#-e检测文件是否存在（包括目录），如果是就返回true
if [ -e ${file} ]
then
	echo "-e ${file}:ture"
else
	echo "-e ${file}:false"
fi
```
运行结果：
```
[vagrant@localhost vagrant]$ ./test9.sh
-b /vagrant/Shell.md:false
-c /vagrant/Shell.md:false
-d /vagrant/Shell.md:false
-f /vagrant/Shell.md:ture 
-g /vagrant/Shell.md:false
-k /vagrant/Shell.md:false
-p /vagrant/Shell.md:false
-u /vagrant/Shell.md:false
-r /vagrant/Shell.md:ture
-w /vagrant/Shell.md:ture
-x /vagrant/Shell.md:false
-s /vagrant/Shell.md:ture
-e /vagrant/Shell.md:ture
```

文件检测运算符列表

运算符|说明
-----|------
-b|检测文件是否为块设备文件，如果是返回ture
-c|检测文件是否为字符设备文件，如果是，就返回ture
-d|检测文件是否为目录，如果是，就返回ture
-f|检测文件是否为普通文件（既不是目文件，也不是设备块文件），如果是就返回ture
-g|检测文件是否设置了SGID位，如果是，就返回ture
-k|检测文件是否设置了粘着位（Stick Bit）,如果是，就返回ture
-p|检测文件是否具有名管道，如果是就返回ture
-u|检测文件是否设置了SUID位，如果是，就返回ture
-r|检测文件是否为可读，如果是，就返回ture
-w|检测文件是否是否为可写，如果是，就返回ture
-x|检测文件是否为可读，如果是，就返回ture
-e|检测文件是否为空，包括目录，如果是，则返回ture

### 字符串
字符串在编程中是最常用的数据类型，当然在shell中也是这样，shell中字符串可以用`" "`或`' '`。

####单引号
```
strg='this is a string'
```
单引号字符串的限制：
* 单引号是原样输出，里面的字符使用变量是无效的，`echo 'this is ${st}'`,输出结果是`this is ${st}`
* 单引号里面是不能出现单引号的，即使进行转义也不行。

####双引号
```
username="Jay"
email="jay.wang.liu@gmail.com"
echo "${username} is login and email is ${email} \n"
```
双引号的特点：
* 双引号里面可以有变量
* 双引号也可以有转义字符

####拼接字符串
```
firstName="Jay"
lastName="Wang'
email="jay.wang.liu@gmail.com"
username=${lastName},${firstName}
echo ${username}
```
输出结果为：
```
Wang,Jay
```
####获取字符穿长度
```
string="qazwsx"
echo ${#string}
```
输出：
```
6
```
####提取子字符串
```
string＝"Jay is learing linux shell"
echo ${string:0:2}
#｛string:index:length｝表示从哪里开始提取多长的字符串
```

####查找子字符串
```
string="Jay is learing linux shell"
echo `expr index "${string} is"`
```
###数组
数组很重要的，用来顺序存储一组数据，在`bash shell`中只支持一纬数组，但和`C`一样不限定数组长度，取数组中元素需要下标`index`，从0开始。

####定义数组
在shell中定义数组不像`C`和`Java`使用`{}`直接定义，这里是用`()`定义数组的。
例如：
```
#定义一个数组
#每个元素空格分开
array=(value0 value1 value2 value3 )
```
或者：
```
#这里和js一样不加分号，以行为执行单位，到行末结束
array=(
value0
value1
value2
)
```
单独定义数组中的元素：
```
array[0]="value1"
array[1]="value2"
array[2]="value3"
```
#### 读取数组元素
读取数组的一般格式为：
```
${array[index]}
```
可以使用`@`或`*`获取数组中所有的元素：
```
${array[*]}
${array[@]}
```

#### 获取数组的长度
获取数组长度和获取字符串的长度方法一样，字符串本身也是一个字符数组。
```
#取得数组元素的个数
length=${#array[*]}
#或者
length=${#array[@]}
#获取数组中的元素的长度
length=${#array[n]}
```
### echo和printf
echo和printf都是向屏幕终端输出只定字符。echo是普通的输出，printf像在C中一样时格式化输出。

#### echo
echo是Shell的一个内部指令。格式如下：
```
echo arg
```
###### 显示转义字符
```
echo "\"This is a test \" \n"
```
输出：
```
"This is a test"

```
######显示变量
```
username="Jay"
email="jay.wang.liu@gmail.com"
echo "${userame} has login"
echo ${email}
```
输出：
```
Jay has login
jay.wang.liu.wang@gmail.com
```
######显示转义字符
```
#换行
echo "test /n"
#不换行
echo "test /c"
```

######显示结构重定向
这个应该是在Linux上经常的操作
```
#创建一个文件把输出结果重定向到文件中
file=`touch test`
echo "Hello Jay" >${file}
```
######显示命令执行结果
```
#显示当前日期
echo `date`
```

####printf
printf是格式化输出，功能上比echo更强大。而且printf由POSIX标准定义，所以移植性比echo要好。
printf命令的语法：
```
printf format-string [arguments]
```
format-string 为格式控制字符串，argumetns为显示的字符参数数组
shell与C的printf的不同：
* 这里不需要加括号
* `ormat-string `可以没有引号，但最好加上，可以双引号，也可以双引号
* 参数多于格式控制符时`(%)`,`format-string`可以重用，可以将所有参数都转换
* `agruments`使用空格分开，不使用逗号`,`

完整的例子：
```
# format-string为双引号
$ printf "%d %s\n" 1 "abc"
1 abc
# 单引号与双引号效果一样 
$ printf '%d %s\n' 1 "abc" 
1 abc
# 没有引号也可以输出
$ printf %s abcdef
abcdef
# 格式只指定了一个参数，但多出的参数仍然会按照该格式输出，format-string 被重用
$ printf %s abc def
abcdef
$ printf "%s\n" abc def
abc
def
$ printf "%s %s %s\n" a b c d e f g h i j
a b c
d e f
g h i
j
# 如果没有 arguments，那么 %s 用NULL代替，%d 用 0 代替
$ printf "%s and %d \n" 
and 0
# 如果以 %d 的格式来显示字符串，那么会有警告，提示无效的数字，此时默认置为 0
$ printf "The first program always prints'%s,%d\n'" Hello Shell
-bash: printf: Shell: invalid number
The first program always prints 'Hello,0'
$
```
注意，根据POSIX标准，浮点格式`%e`、`%E`、`%f`、`%g`与`%G`是“不需要被支持”。这是因为awk支持浮点预算，且有它自己的printf语句。这样Shell程序中需要将浮点数值进行格式化的打印时，可使用小型的awk程序实现。然而，内建于bash、ksh93和zsh中的printf命令都支持浮点格式。

###流程控制
#### if else
if语句通过关系运算表达式来判断执行哪个分支。三种分支`if....else`语句
* `if...fi`语句
* `if...else...fi`语句
* `if...elif...fi`语句


#####if...fi语句
```
if [ expression ]
then
	Statement(s) to be executed if expression=true
fi
```

#####if...else...fi语句
```
if [ expression]
then
		Statement(s) to be executed if expression=true
else
		Statement(s) to be executed if expression=false
fi
```
#####if...elif..fi语句
```
if [ expression0 ]
then 
	Statement0 to be executed if expression0=ture
elif [ expression 1]
then
	Statement1 to executed if expressin1=ture
else 
	Last Statement to executed if expression0=false and expression1=false
fi
```

#### case esac
case...esac与其他的语言中的switch...case语句类似，是多分支结构
格式如下：
```
case var in
var1)
	command1
    command2
    command3
    ;;
var2)
	command1
    command2
    command3
    ;;
*)
	command1
    command2
    command3
    ;;
esac
```
`case`工作模式如上代码,取值必须为关键字`in`,每一行必须以`)`结束。取值可以是为变量或常数。匹配发现某值符合某一模式后，执行这一匹配分支，直到`;;`，这里`;;`相当`break`类似，跳出整个case。
这里有个`*)`匹配，这里和`default`的功能一样，如果其他的都匹配不到，那么久执行`*)`这个默认分支。

case脚本例子：
```
/!#/bin/bash
echo 'Input a number between 1 to 4'
echo 'Your numer is:\c'
read aNum
case $aNum in
	1) echo 'You select 1'
	;;
    2) echo 'You select 2'
    ;;
    3) echo 'You select 3'
    ;;
    4) echo 'You select 4'
    ;;
    *) echo 'You dont read the right num between 1 to 2'
    ;;
esac
```
运行结果：
```
Input a number between 1 to 4
Your numer is:\c
3
You select 3

```

#### for 循环
shell中for循环的格式如下：
```
for var in list
do
	command1
    command2
    ...
    comandN
done
```
`list`列表是一组值(数字、字符串)组成的序列，每个值通过空格分隔。没循环一次，列表中的下一个值就赋给变量。
`in`列表是可选的，如果不用它，for循环使用命令行参数
例如：
```
for var in 1 2 3 4 5
do
	echo "The value is:${var}"
done
```
运行结果如下
```
The value is 1
The value is 2
The value is 3
The value is 4
The value is 5
```
 顺序输出字符串中的字符：
```
for str in 'This is a string'
do 
	echo "${str}\n"
done
```
运行结果
```
This is a string
```
显示主目录下以.bash 开头的文件
```
for FILE in $HOME/.bash*
do
	echo ${FILE}
done
```
运行结果：
```
/home/vagrant/.bash_history
/home/vagrant/.bash_logout
/home/vagrant/.bash_profile
/home/vagrant/.bashrc
```

#### while循环
while循环用于不断执行一系列命令，也用于从文件中读取数据命令
```
while command
do
	Statement(s) to be executed if command is true
done
```
一个简单的`while`循环，从0开始循环递增直到5，终止。
```
#!/bin/bash
COUNTER=0
END=5
while [ ${COUNTER} -lt ${END} ]
do
        COUNTER=`expr ${COUNTER} + 1`
    echo ${COUNTER}
done
```
运行结果：
```
[vagrant@localhost vagrant]$ ./test17.sh
1
2
3
4
5
```
还可以写一个`while` 显示键盘的输入信息
```
while read input
do
	echo "you input ${input}"
done
```
####until循环
####跳出循环

###函数

