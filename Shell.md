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
<<<<<<< HEAD
#|传递给脚本或函数的参数个数
*|传递给脚本或函数的所有参数
@|传递给脚本或函数的所有参数。被双引号（" ")包含时，与`*`会不同
?|上个命令的退出状态，或函数的返回值
=======
＃|传递给脚本或函数的参数个数
*|传递给脚本或函数的所有参数
@|传递给脚本或函数的所有参数。被双引号（" ")包含时，与`*`会不同
？|上个命令的退出状态，或函数的返回值
>>>>>>> 3bd46c6ceecad67ec75d155422b3d334a2d2a692
$|当前Shell的进程id.对于Shell脚本，就是这些脚本所在的进程ID。

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




