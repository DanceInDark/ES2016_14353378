#Lab1:DOL开发环境配置

###DOL简介：
Distributed Operation Layer : 
The distributed operation layer (DOL) is a software development framework to program parallel applications. The DOL allows to specify applications based on the Kahn process network model of computation and features a simulation engine based on SystemC. Moreover, the DOL provides an XML-based specification format to describe the implementation of a parallel application on a multi-processor systems, including binding and mapping.

###配置步骤：
1. 安装一些必要的开发环境（ubuntu为例）：
	* $	sudo apt-get update
	* $	sudo apt-get install ant
	* $ sudo apt-get install openjdk-7-jdk
	* $	sudo apt-get install unzip
2. 下载文件(使用Vmware虚拟机，也可以从主机拷贝到虚拟机中去
 [（下载地址点我）](http://jingyan.baidu.com/article/c33e3f48a5c153ea15cbb5b2.html)

   - sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz

   - sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip
3. 解压文件
 - 新建dol的文件夹：
	$ mkdir dol
 - 将dolethz.zip解压到 dol文件夹中：
    $ unzip dol_ethz.zip -d dol
 - 解压systemc：
    $ tar -zxvf systemc-2.3.1.tgz
 - 编译systemc
	 	- 解压后进入systemc-2.3.1的目录下： $	cd systemc-2.3.1
	    - 新建一个临时文件夹objdir：$	mkdir objdir
		- 进入该文件夹objdir：$	cd objdir
		- 运行configure(能根据系统的环境设置一下参数，用于编译)：
   		$	../configure CXX=g++ --disable-async-updates
  		![configure成功后就图](http://i1.piimg.com/567571/84db50cbf7f6c888.png)
		- 编译:   $	sudo make install , 编译完后文件目录如下($ cd ..        $ ls
        ![文件目录](http://i1.piimg.com/567571/28e9ca0e95e22ab1.png)
 		- 记录当前的工作路径(会输出当前所在路径，记下来，待会有用)：$	pwd
        ![工作路径](http://i1.piimg.com/567571/bf900ad17b103413.png)
4. 编译dol
 - 进入刚刚dol的文件夹:$	cd ../dol
 - 修改build_zip.xml文件:
	找到下面这段话，就是说上面编译的systemc位置在哪里，
	<property name="systemc.inc" value="YYY/include"/>
	<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>
	把YYY改成上页pwd的结果（注意，对于  64位 系统的机器，lib-linux要改成lib-linux64）
 - 然后是编译:$	ant -f build_zip.xml all;若成功会显示build successful
   ;接着可以试试运行第一个例子:进入build/bin/mian路径下:$	cd build/bin/main
   ;然后运行第一个例子:$	ant -f runexample.xml -Dnumber=1;成功结果如图:
   ![成功结果](http://p1.bpimg.com/567571/763125e8abb868e7.png)
