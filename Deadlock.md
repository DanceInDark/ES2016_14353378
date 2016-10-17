#Lab4:死锁
##死锁发生的必要条件：
1. 互斥：即资源不能被多个进程同时占有。
2. 占有且等待：一个进程占有一些资源，但它还需要的一些资源被其它进程占有，处于等待状态。
3. 非抢占：资源不能被中途抢占。
4. 循环等待：{P0,P1,P2...Pn},P0等待P1占用的资源，P1等待P2...Pn等待P1。
##实验流程：
1. 编译java代码：javac Deadlock.java。
2. 让系统执行上面的代码编译所得的Deadlock.class文件100遍，观察结果，linux下的批处理脚代码为：
![](http://d3.freep.cn/3tb_161018002120inm4576192.png)
windows下代码如下（保存为.bat格式）：
`
cd /d %~dp0
@echo off
:start
set /a var+=1
echo %var%
java Deadlock
if %var% leq 1000 GOTO start
pause
`
运行批处理脚本，观察什么时候发生死锁，运行多少次死锁会发生是随机的，如果多次试验仍不发生死锁则修改程序中count的值，使其发生死锁，我在第11次观察到死锁：
![](http://d2.freep.cn/3tb_161018003005n1eh576192.png)
##对程序产生死锁的解释
Deadlock.java代码如下：
```java
class A{
	synchronized void methodA(B b){
		b.last();
	}
	
	synchronized void last(){
		System.out.println("Inside A.last()");
	}

}

class B{
	synchronized void methodB(A a){
		a.last();
	}
	
	synchronized void last(){
		System.out.println("Inside B.last()");
	}

}

class Deadlock implements Runnable{
	A a=new A();
	B b=new B();

	Deadlock(){
		Thread t = new Thread(this);
		int count = 10000;
		
		t.start();
		while(count-->0);
		a.methodA(b);
	}
	public void run(){
		b.methodB(a);
	}
	
	public static void main(String args[]){
		new Deadlock();
	}
}
```
###关键字 synchronized:

- 当它用来修饰一个方法或者一个代码块的时候，能够保证在同一时刻最多只有一个线程执行该段代码。
- 当一个线程访问object的一个synchronized同步代码块或同步方法时，其他线程对object中所有其它synchronized同步代码块或同步方法的访问将被阻塞。
![](http://d3.freep.cn/3tb_161018003950jjg1576192.png)
Deadlock()先创建一个子线程t，然后调用t.start()函数让线程t运行，同时父线程继续运行，计数10000后调用a.method(b)函数，由于调用t.start()函数让t运行然后调用run()的延时大多数情况下要比计数10000的时间长（可以将count改大验证，我将count增大10倍两句话输出顺序就颠倒过来了），故不发生死锁的情况下a.method(b)限制性输出“Inside B.last()”,然后t线程在run()里调用b.method(a)函数输出“Inside A.last()”。但也可能出现这两个延时接近的情况导致同时调用a.method(b)和a.last()或同时调用b.method(a)和b.last()函数，这都是同时调用两个线程同时访问同一对象的两个synchronized同步代码块的情况，两个线程均被阻塞，死锁发生。
