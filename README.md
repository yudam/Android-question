### 操作系统问题？
* 操作系统中进程和线程的区别？
* 死锁的产生和避免？

### Android基础问题？
* Android Studio中V1、V2签名的区别？
* Handler中looper.loop()阻塞状态时为什么不会导致ANR？
* ThreadLocal的使用和作用？



#### Android Studio中V1、V2签名的区别？
* V1 是对jar进行签名。应该是通过ZIP条目验证进行验证，APK签署后可以进行很多修改，移动甚至重新压缩文件。  
* V2 是对整个apk进行签名。验证压缩文件的所有字节，而不是单个的ZIP条目。签名后无法更改。在编译过程中压缩。   
* v2签名是在整个APK文件的二进制内容上计算和验证的，v1是在归档文件中解压缩文件内容。V2签名更安全而且缩短了在设备上验证的事件（不需要解压缩）。

#### Handler中looper.loop()阻塞状态时为什么不会导致ANR？
* 线程是一段可执行代码，当可执行代码执行完毕后，线程的生命周期便该终止了，但对于主线程，我们希望它能够一直运行下去，简单来说就是可执行代码能够
继续执行，死循环便可以保证主线程一直运行下去。没有消息时会进行休眠。通过新线程的方式来发送事务给主线程，唤醒主线程。真正会卡死主线程的操作是
在onCreate、onStart和onResume中等待操作时间错长，导致掉帧甚至ANR。Looper.loop本身并不会导致主线程卡死。  
* MessageQueue中没有消息时，主线程会释放CPU资源进入休眠，不会特别消耗CPU资源。  
* 注意：当我们创建一个线程时，线程本身并不会创建Looper对象，如果我们创建了Looper对象，并调用了loop方法，要注意loop方法之后的方法不会继续执行。
所以在线程执行完成后，需要调用quit方法 来退出线程。  
[handler、looper死循环](https://www.cnblogs.com/chenxibobo/p/9640472.html)

#### ThreadLocal的使用和作用？  
[ThreadLocal的使用](https://github.com/yudam/Android-question/blob/master/ThreadLocal%E8%A7%A3%E6%9E%90.md)

#### SharedPreferences原理？能否跨进程实现？


#### Intent 能传递多大 Size 的数据? Intent中用法和序列化的作用？

#### 多线程并发问题？(volatile，Synchronized,ReentranLock和集合)

#### volatile的原理？以及为什么没有实现原子性？
[volatile的操作原理](https://www.cnblogs.com/monkeysayhi/p/7654460.html)

#### ViewGroup中添加View为什么不显示？如果显示的话为什么在手动测量View？
