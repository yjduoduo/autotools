aclocal: `configure.ac' or `configure.in' is required


.3.2��ʵ��
������һ��ʵ����˵�����ʹ��autotools���ߡ���Ŀ�����ļ���main.c��test1.c��test2.c��test1.h��test2.h��
? ��һ��������autoscan
���ն������롰autoscan�����س�ִ�У�����configure.scan�����ļ���configure.in��ԭ�ͣ���configure.in��autoconf�Ľű������ļ��������ڽ�����һ������֮ǰҪ��configure.scan�����޸ģ�����������Ϊconfigure.in��configure.scan�ļ��������£�
...
AC_PREREQ([2.64])
AC_INIT([FULL-PACKAGE-NAME], [VERSION], [BUG-REPORT-ADDRESS])
AC_CONFIG_SRCDIR([main.c])
AC_CONFIG_HEADERS([config.h])
...
AC_OUTPUT
��configure.scan�����ݼ�Ҫ˵�����£�
v AC_PREREQ���������ļ�Ҫ���autoconf�汾��
v AC_INIT�궨����������ơ��汾����Ϣ������BUG-REPORT-ADDRESS����ʡ�ԡ�
v AC_CONFIG_SRCDIR���������ָ�����ļ��Ƿ���ڣ���ȷ��Դ��Ŀ¼����Ч�ԡ�
v AC_CONFIG_HEADER����������config.h�ļ����Ա�autoheaderʹ�á�
�޸ķ������£�
v ��дAC_INIT��Ҫ��������ݡ�
v ��Ӻ�AM_INIT_AUTOMAKE������������ݡ�
v ���AC_CONFIG_FILES([Makefile])��
v ���޸ĺ�configure.scan�ļ��󣬰������Ϊconfigure.in��
�����õ���configure.in�ļ��������£�
...
AC_PREREQ([2.64])
AC_INIT(appname, 1.0, panzhh_459@163.com) #�޸ĵĺ�
;AM_INIT_AUTOMAKE(appname, 1.0) #��ӵĺ�
;AC_CONFIG_SRCDIR([main.c])
AM_CONFIG_HEADERS([config.h])
...
AC_CONFIG_FILES([Makefile]) #��ӵĺ�
;AC_OUTPUT
? �ڶ���������aclocal
���ն������롰aclocal�����س�ִ�С����������configure.in����������aclocal.m4�ļ������ļ���Ҫ�����صĺ궨�塣
? ������������autoconf
���ն������롰autoconf�����س�ִ�С����������configure.in��aclocal.m4����������configure���ýű���configure�ű�����������Makefile�ġ�
? ���Ĳ�������autoheader
���ն������롰autoheader�����س�ִ�С���������������config.h.in�ļ���ͨ���ǻ�ӡ�acconfig.h���ļ��и����û����ӵķ��Ŷ��塣��Ϊ������û�и��ӵķ��Ŷ��壬���Բ���Ҫ������acconfig.h���ļ���
? ���岽����дMakefile.am
automake��Ҫ�ű������ļ�Makefile.am������ļ����ֹ��������������£�
1 AUTOMAKE_OPTIONS=foreign
2 bin_PROGRAMS=appname
3 appname_SOURCES=main.c test1.c test1.h test2.c test2.h
��˵����
��һ����AUTOMAKE_OPTIONS��������automake��ѡ�GNU���Լ�������������ϸ�Ĺ淶��������븽�����֤�����ļ�COPYING�ȵȣ�����automakeִ��ʱ�ᱨ��automake�ṩ��3������ȼ���foreign��gnu��gnits��Ĭ�ϵȼ���gnu��ʾ����ʹ�õ���foreign����ʾֻ����Ҫ���ļ���
�ڶ�����bin_PROGRAMS������Ҫ������ִ���ļ�����������������ִ���ļ���ÿ���ļ���Ҫ�ÿո������
��������file_SOURCES����file���ִ�г���������ļ������С�file_SOURCES���е�ǰ���֡�file��Ҫ��д�ɿ�ִ���ļ���������bin_PROGRAMS���������һֱ������ж����ִ���ļ����Ǿ�Ҫ������Ӧ��file_SOURCES��
? ��������ִ��automake
��һ������Ҫ��automake����ű������ļ�Makefile.am�� ����Makefile.in����һЩ����Ľű��ļ����硰install-sh������missing���ȣ����Դ�automake������︴�ƹ�����ֻ�� ��ִ��ʱʹ�á�--add-missing��ѡ��ɡ�Ĭ�ϵĴ���ʽ�Ǵ�����Щ�ļ��ķ������ӣ�����ټ��ϡ�--copy��ѡ�������ʹ�ø��Ʒ�ʽ��ִ �е������ʽ���£� 
# automake --add-missing --copy
? ���߲���ִ��configure
���ն������롰./configure�����س�ִ�У�����ִ�е��������ɵ�configure���ýű����ýű����ݵ��Ĳ����ɵ�config.h.in�͵��������ɵ�Makefile.in������������Makefile�ļ���


