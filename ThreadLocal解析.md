ThreadLocalMap是ThreadLocal的内部静态类，内部维护了一个初始容量为16的table数组。每一个线程内部单独维护了一个ThreadLocalMap对象。  

ThreadLocal存储数据实现了线程隔离。
```java
public T get() {
        Thread t = Thread.currentThread();
        ThreadLocalMap map = getMap(t);
        if (map != null) {
            ThreadLocalMap.Entry e = map.getEntry(this);
            if (e != null) {
                @SuppressWarnings("unchecked")
                T result = (T)e.value;
                return result;
            }
        }
        return setInitialValue();
    }
```
使用ThreadLocal获取数据时，根据当前线程获取ThreadLocalMap对象,若存在则获取，不存在执行下一层方法。

```java
private T setInitialValue() {
        T value = initialValue();
        Thread t = Thread.currentThread();
        ThreadLocalMap map = getMap(t);
        if (map != null)
            map.set(this, value);
        else
            createMap(t, value);
        return value;
    }
```
默认initialValue方法返回值为空，当ThreadLocalMap对象不为null时，存储当前值。反之创建一个ThreadLocalMap对象来存储。

```java
public void set(T value) {
        Thread t = Thread.currentThread();
        ThreadLocalMap map = getMap(t);
        if (map != null)
            map.set(this, value);
        else
            createMap(t, value);
    }

```
可以看到 无论获取还是设置value值时，都会根据当前Thread来获取Thread内部的ThreadLocalMap变量，以当前的ThreadLocal为key来存储value值。  

ThreadLocal实现了数据的线程隔离，为每一个线程创造一份空间来存储数据，牺牲空间来换取冲突，有效的解决了多线程导致的数据错乱问题。

总结来说就是：每个Thread内部维护了一个ThreadLocalMap对象，ThreadLocalMap对象内又维护了一个table数组，以ThreadLocal的具体转码的Hash值为下标
来进行存储数据。

用处：当数据是以线程为作用域并且，不同线程具有不同的数据副本时，就可以采用ThreadLocal。



