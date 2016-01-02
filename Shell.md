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

    
	
    
    
 