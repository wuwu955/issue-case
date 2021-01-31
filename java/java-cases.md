### Java问题Cases

#### ThreadPool
##### ThreadPoolExecutor使用不当容易踩到的“坑”
* [Java中容易踩到的“坑”系列之线程池篇 – hellojavacases - 毕玄 - 林昊](http://hellojava.info/?p=13)
 * 对各种BlockingQueue(阻塞队列)理解不深刻（SynchronousQueue、LinkedTransferQueue、LinkedBlockingDeque、LinkedBlockingQueue、ArrayBlockingQueue、DelayQueue）


#### Memory
##### OOM-OutOfMemoryError: unable to create new native thread
* [问题分析：java.lang.OutOfMemoryError: unable to create new native thread](http://blog.csdn.net/ado1986/article/details/48286513)
 * 根本原因：线程池对象持有的线程泄漏引发OOM，进而无法创建本地线程。
 * 建议：线程池对象必须声明为类变量
 * 反例

    private ScheduledExecutorService executor = new ScheduledThreadPoolExecutor(50,
            new BasicThreadFactory.Builder().namingPattern("schedule-pool-%d").daemon(true).build()){
        @Override
        protected void afterExecute(Runnable r, Throwable t)
        {
            super.afterExecute(r, t);
            Threads.printException(r, t);
        }
    };
* [记一次线上OOM的问题](http://blog.csdn.net/ado1986/article/details/49491597)
 * 根本原因：静态全局的ConcurrentHashMap未释放缓存的对象，数量一直增长，从而引发内存溢出。


