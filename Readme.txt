aclocal: `configure.ac' or `configure.in' is required


.3.2、实例
下面结合一个实例来说明如何使用autotools工具。项目中有文件：main.c、test1.c、test2.c、test1.h、test2.h。
? 第一步：运行autoscan
在终端中输入“autoscan”并回车执行，生成configure.scan，该文件是configure.in的原型，而configure.in是autoconf的脚本配置文件。所以在进行下一步工作之前要对configure.scan进行修改，将其重命名为configure.in。configure.scan文件内容如下：
...
AC_PREREQ([2.64])
AC_INIT([FULL-PACKAGE-NAME], [VERSION], [BUG-REPORT-ADDRESS])
AC_CONFIG_SRCDIR([main.c])
AC_CONFIG_HEADERS([config.h])
...
AC_OUTPUT
对configure.scan的内容简要说明如下：
v AC_PREREQ宏声明本文件要求的autoconf版本。
v AC_INIT宏定义软件的名称、版本等信息，其中BUG-REPORT-ADDRESS可以省略。
v AC_CONFIG_SRCDIR宏用来侦测指定的文件是否存在，来确定源码目录的有效性。
v AC_CONFIG_HEADER宏用于生成config.h文件，以便autoheader使用。
修改方法如下：
v 填写AC_INIT宏要定义的内容。
v 添加宏AM_INIT_AUTOMAKE，及定义的内容。
v 添加AC_CONFIG_FILES([Makefile])。
v 在修改好configure.scan文件后，把其改名为configure.in。
这样得到的configure.in文件内容如下：
...
AC_PREREQ([2.64])
AC_INIT(appname, 1.0, panzhh_459@163.com) #修改的宏
;AM_INIT_AUTOMAKE(appname, 1.0) #添加的宏
;AC_CONFIG_SRCDIR([main.c])
AM_CONFIG_HEADERS([config.h])
...
AC_CONFIG_FILES([Makefile]) #添加的宏
;AC_OUTPUT
? 第二步：运行aclocal
在终端中输入“aclocal”并回车执行。该命令根据configure.in的内容生成aclocal.m4文件，该文件主要处理本地的宏定义。
? 第三步：运行autoconf
在终端中输入“autoconf”并回车执行。该命令根据configure.in和aclocal.m4的内容生成configure配置脚本，configure脚本是用来生成Makefile的。
? 第四步：运行autoheader
在终端中输入“autoheader”并回车执行。该命令用来生成config.h.in文件。通常是会从“acconfig.h”文件中复制用户附加的符号定义。因为本例中没有附加的符号定义，所以不需要创建”acconfig.h”文件。
? 第五步：编写Makefile.am
automake需要脚本配置文件Makefile.am，这个文件得手工建立。内容如下：
1 AUTOMAKE_OPTIONS=foreign
2 bin_PROGRAMS=appname
3 appname_SOURCES=main.c test1.c test1.h test2.c test2.h
简单说明：
第一行中AUTOMAKE_OPTIONS用来设置automake的选项。GNU对自己发布的软件有严格的规范，比如必须附带许可证声明文件COPYING等等，否则automake执行时会报错。automake提供了3种软件等级：foreign、gnu和gnits。默认等级是gnu。示例中使用的是foreign，表示只检测必要的文件。
第二行中bin_PROGRAMS定义了要产生的执行文件名。如果产生多个可执行文件，每个文件名要用空格隔开。
第三行中file_SOURCES定义file这个执行程序的依赖文件，其中“file_SOURCES”中的前部分“file”要改写成可执行文件名，即与bin_PROGRAMS定义的名称一直。如果有多个可执行文件，那就要定义相应的file_SOURCES。
? 第六步：执行automake
这一步很重要，automake处理脚本配置文件Makefile.am后， 生成Makefile.in。有一些必需的脚本文件，如“install-sh”、“missing”等，可以从automake软件包里复制过来，只需 在执行时使用“--add-missing”选项即可。默认的处理方式是创建这些文件的符号链接，如果再加上“--copy”选项则可以使用复制方式。执 行的命令格式如下： 
# automake --add-missing --copy
? 第七步：执行configure
在终端中输入“./configure”并回车执行，就是执行第三步生成的configure配置脚本，该脚本根据第四步生成的config.h.in和第六步生成的Makefile.in的内容来生成Makefile文件。


