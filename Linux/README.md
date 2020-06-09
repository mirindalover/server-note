#### fd-File descriptor(文件描述符)

Linux系统中，所有都可以抽象成文件。如：文件、目录、socket、管道、线程start都会返回一个fd存起来

每个进程都有一个 打开文件数组。存放文件对象的指针，fd就是指针的下标

>cat /proc/sys/fs/file-max	所有进程允许打开最大fd数量
>
>cat /proc/sys/fs/file-nr	所有进程已经打开的fd数量及允许的最大数量
>
> ulimit -n	单个进程允许打开的最大fd数量
>
> ls -l /proc/5454/fd/	单个进程已经打开的fd

#### IO模式

1. 等待数据准备(数据->内核缓冲区)

2. 内核缓冲区到用户进程

#### select poll epoll

##### select 

> 维护fd数组,数组存放了需要监听的socket对象

用于监听：writefds、readfds、和exceptfds

1. 监听fds，调用后阻塞，直到fd就绪、超时

2. 返回函数，遍历fdset找到就绪的fd

fd数组大小Linux中默认为1024

##### poll

与select相同，返回后需要轮询 pollfd获取就绪的socket

##### epoll

1.  epoll_create() 初始化epoll的句柄，创建后占用一个fd值(使用完后使用close关闭)，同时维护了rdlist(引用收到socket的对象)

2.	epoll_ctl() 对指定fd执行指定(通过参数)的操作--添加或者删除监听的socket

3.	epoll_wait()获取监听的fd的io事件

- 过程

	阻塞：进程运行到epoll_wait时，内核将进程加入eventpoll的等待队列
	
	唤醒：socket接收到数据后，中断程序会做两件事：(1)修改rdlist（知道是哪个socket发生改变）(2) 唤醒eventpoll中的等待队列中的进程

>	epoll通过callback的回调机制,监听的fd就绪后激活这个fd(epoll的)


