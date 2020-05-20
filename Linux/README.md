#### fd-File descriptor(文件描述符)

Linux系统中，所有都可以抽象成文件。如：文件、目录、socket、管道、线程start都会返回一个fd存起来

每个进程都有一个 打开文件数组。存放文件对象的指针，fd就是指针的下标

Linux中默认为1024

> /proc/sys/fs/file-max	所有进程允许打开最大fd‘数量
>
> /proc/sys/fs/file-nr	所有进程已经打开的fd数量及允许的最大数量
>
> ulimit -n	单个进程允许打开的最大fd数量
>
> ls -l /proc/5454/fd/	单个进程已经打开的fd