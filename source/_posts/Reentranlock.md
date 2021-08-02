Reentranlock



thread1 执行业务代码lock

把aqs里的state改成1  cas操作aba，aba操作加版本号

park和unpark可以指定线程

非公平锁的体现，前线程执行完以后，unpark的线程和新来的线程同时抢占锁

公平锁和非公平锁的区别：

只能队列里面的抢占，可以队列里面的线程和刚进来的线程