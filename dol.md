#Lab2: DOL 实例分析&编程

##任务：
1. 修改example2，让3个square模块变成2个, tips:修改xml的iterator
2. 修改example1，使其输出3次方数，tips:修改square.c
###提示：
  -  修改代码之后要重新编译、运行（sudo ant –f runexample.xml –Dnumber=XXX）XXX是运行example的号码，比如上面是2和1
##实验过程及结果
###example2
1. 打开example2.xml,将变量N的value改为2，这样迭代次数就变为了2，square模块变味了2个。
![](http://d3.freep.cn/3tb_161017002250xxrn576192.png)

2. 如果之前已经编译过example2，则进入/dol/build/bin/main,删掉example2整个文件夹;若显示文件加锁，则使用sudo chown -R username filename命令将修改文件权限为当前用户。
3. 输入如下命令编译运行example2：sudo ant -f runexample.xml -Dnumber=1。
4. 观察运行结果：

![](http://d2.freep.cn/3tb_161017003228t2iy576192.png)

5. 观察dot图,可以看到平方模块变为了2个：
![](http://d3.freep.cn/3tb_16101700364751li576192.png)
###example1
1. 进入/dol/examples/example1/src文件夹，找到square.c文件和square.h文件，改名为cube.c和cube.h;打开cube.c，将代码中i*i改为i*i*i,并将头文件改为cube.h,如下图:
![](http://d2.freep.cn/3tb_161017004359v5hm576192.png)
2. 回到/dol/examples/example1目录，用编辑器打开example1.xml，将里面的square换成cube:
![](http://d3.freep.cn/3tb_1610170050234f5j576192.png)
3. 打开map_1.xml和map_3.xml将square替换成cube。
4. 编译运行example1（如果之前已运行过，同样要先将/dol/build/bin/main中example1删除），观察运行结果，可以看到程序已有原来的算平方变为了算3次方：
![](http://d3.freep.cn/3tb_16101700554052w0576192.png)
5. 查看.dot图，可以看到模块名已经变为了cube，因为我们已经在系统架构即模块连接方式定义中将模块名修改了。
![](http://d3.freep.cn/3tb_161017005749w2ln576192.png)
##实验感想
这次实验其实非常简单，但还是不能粗心，尤其是我们队linux命令行界面编程还不是很熟悉；我之前就因为在修改代码时初心导致了一点语法错误，结果反复build失败，还以为是dol环境出问题了，后来我又重新去看编译过程的提示，这才发现了问题，浪费了不少时间。以后再linux中编程一定要更加小心，因为这里通常没有IDE来辅助你，出错了也要冷静，仔细查看命令行的提示，分析问题。