#安装ROS
##ROS简介
Robot operation system，一套框架，底层提供硬件驱动，软件层
面支持通用的文件格式。安装ROS首先需要安装一个Ubuntu。
##参考资料
 - Ubuntu 14.04，15.04 请参考：<http://wiki.ros.org/jade/Installation/Ubuntu>
 - Ubuntu 15.10，16.04 请参考：<http://wiki.ros.org/kinetic/Installation/Ubuntu>
##安装步骤：
###我实在Ubuntu16.04 64位系统下安装ROS的，具体步骤如下：
1. Configure your Ubuntu repositories：Configure your Ubuntu repositories to allow "restricted," "universe," and "multiverse."<br>
我的系统这三个权限都已经允许了，故跳过这步。 
2. Setup your sources.list<br>
Setup your computer to accept software from packages.ros.org.
`sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'`
3. Set up your keys
`sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116`
4. Installation<br>
 First, make sure your Debian package index is up-to-date: 
 `sudo apt-get update`<br>
 接下来，选择Desktop-Full Install<br>
 `sudo apt-get install ros-kinetic-desktop-full`
5. Initialize rosdep<br>
`sudo rosdep init`<br>
`rosdep update`
6. Environment setup 
 `echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc`<br>
 `source ~/.bashrc`
7. Getting rosinstall<br>
 `sudo apt-get install python-rosinstall`
8. Build farm status<br>
 The packages that you installed were built by the [ROS build farm](http://build.ros.org/). You can check the status of individual packages [here](http://repositories.ros.org/status_page/ros_kinetic_default.html). 
###测试
Now, to test your installation, please proceed to the ROS [Tutorials](http://wiki.ros.org/ROS/Tutorials). 
##总结
ROS安装耗时较长，主要是下载各种文件花时间，建议在下载时先去做其它事。都是按照步骤做就行，也没什么其它的了。