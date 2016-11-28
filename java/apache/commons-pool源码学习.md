# 深入学习Apache Commons Pool

+ Apache Commons Pool介绍
+ 如何使用Apache Commons Pool
+ 源代码分析研究
+ 小结

## Apache Commons Pool介绍

Apache Commons Pool有两个版本，1.x 和 2.x，2.x是对1.x的完全重写版本，一般项目都采用2.x（jdk版本1.6+），此工具的作用是做对象池，防止对象的重复创建，一般用在数据库连接池等使用场景。更具体的信息可以参考 [apache官方网站](http://commons.apache.org/proper/commons-pool/)

 

## 如何使用Apache Commons Pool

**重要的几个类：**

```
org.apache.commons.pool2.PooledObjectFactory
org.apache.commons.pool2.impl.GenericObjectPoolConfig
org.apache.commons.pool2.impl.GenericObjectPool
```

GenericObjectPoolConfig 用来做参数配置，一般都会通过Spring的xml配置。

PooledObjectFactory 需要客户端自己实现。

```java
public interface PooledObjectFactory<T> {
    PooledObject<T> makeObject(); //创建对象
    void activateObject(PooledObject<T> obj); 
    void passivateObject(PooledObject<T> obj);
    boolean validateObject(PooledObject<T> obj); //验证对象
    void destroyObject(PooledObject<T> obj); //销毁对象
}
```

GenericObjectPool 需要传入PooledObjectFactory实现类和GenericObjectPoolConfig对象。

```java
public interface ObjectPool<T> {  
    T borrowObject() throws Exception, NoSuchElementException,IllegalStateException; 
    void returnObject(T obj) throws Exception;
    void invalidateObject(T obj) throws Exception;
    void addObject() throws Exception, IllegalStateException,UnsupportedOperationException;
    int getNumIdle();
    int getNumActive();
    void clear() throws Exception, UnsupportedOperationException;
    void close();
}
```

 GenericObjectPool 类图：

![](http://ww4.sinaimg.cn/large/006y8lVagw1fa89qrmv01j311q07k0tq.jpg)



## 源代码分析研究



## 小结

