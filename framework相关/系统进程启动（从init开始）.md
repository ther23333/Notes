## 1、init进程

![image-20250512164749208](./assets/image-20250512164749208.png)

内核完成系统设置后，会在系统文件中启动init.rc文件

init进程是所有用户进程的鼻祖，进程号为1

## 2、zygote进程

![image-20250512164759786](./assets/image-20250512164759786.png)



init通过app_main.cpp来启动zygote进程

主要会启动虚拟机，注册jni方法，然后最后通过jni来调用`zygoteinit.main()`来实现从C++到java层

`zygoteinit.main()`的作用：

- 将zygote注册为socket的服务端
- 预加载类、资源
- fork出systemserver进程
- 开启一个死循环来等待被通知fork其他新进程

## 3、systemserver进程

初始化各种各样的service，并将他们注册到servicemanager中

## 4、serviceManager进程

前面可以看到serviceManager进程应该是早于systemServer进程的

查了下，它是由init进程启动的，由init.rc启动