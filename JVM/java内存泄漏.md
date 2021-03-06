# 内存泄漏和内存溢出
内存泄漏是造成内存溢出的一种原因的，多次内存泄漏堆积后就会造成内存溢出的情况发生。
## 什么是内存泄漏

就是有部分内存使用完了，却没有正常释放给系统，
>内存泄露是指无用对象（不再使用的对象）持续占有内存或无用对象的内存得不到及时释放，从而造成的内存空间的浪费称为内存泄露


### 什么情况下会导致内存泄漏
长生命周期的对象持有短生命周期对象的引用就很可能发生内存泄露，尽管短生命周期对象已经不再需要，但是因为长生命周期对象持有它的引用而导致不能被回收，这就是java中内存泄露的发生场景

[造成内存泄漏的原因主要可以分为以下几种情况](https://www.cnblogs.com/wzyxidian/p/5860473.html)

(长生命周期对短声明周期的引用，导致短生明周期的对象占用的内存不能正常释放开来)
## 内存溢出

内存溢出：指程序运行过程中无法申请到足够的内存而导致的一种错误。

## 内存泄漏发生的原因

1. 程序本身编码不规范，没有正确地释放没有的内存

[java内存泄漏与内存溢出](https://www.cnblogs.com/panxuejun/p/5883044.html)

关于内存泄漏增加几条
1. 不合理使用ThreadLocal与线程池，解决方案是将remove放在finanlly语句之后
2. 没有正确的书写equals和hashcode()


**错误方式**
```java
public class Person {
    public String name;
     
    public Person(String name) {
        this.name = name;
    }
}

public void givenMap_whenEqualsAndHashCodeNotOverridden_thenMemoryLeak() {
    Map<Person, Integer> map = new HashMap<>();
    for(int i=0; i<100; i++) {
        map.put(new Person("jon"), 1);
    }
    //是错误的情况
    Assert.assertFalse(map.size() == 1);
}
```

**正确方式书写**

```java
public class Person {
    public String name;
     
    public Person(String name) {
        this.name = name;
    }
     
    @Override
    public boolean equals(Object o) {
        if (o == this) return true;
        if (!(o instanceof Person)) {
            return false;
        }
        Person person = (Person) o;
        return person.name.equals(name);
    }
     
    @Override
    public int hashCode() {
        int result = 17;
        result = 31 * result + name.hashCode();
        return result;
    }
}
````

```java
@Test
public void givenMap_whenEqualsAndHashCodeNotOverridden_thenMemoryLeak() {
    Map<Person, Integer> map = new HashMap<>();
    for(int i=0; i<2; i++) {
        map.put(new Person("jon"), 1);
    }
    //是正确的
    Assert.assertTrue(map.size() == 1);
}
```

[Understanding Memory Leaks in Java](https://www.baeldung.com/java-memory-leaks)

## 内存泄漏和内存溢出的关系，不是唯一因素
内存泄露是内存溢出的一种诱因，

起上一篇线上应用故障排查之一：高CPU占用介绍的PS命令，ps,top,等命令都是分析系统性能的常用的命令行

最后，总结下排查内存故障的方法和技巧有哪些：

1、top命令：Linux命令。可以查看实时的内存使用情况。  

2、jmap -histo:live [pid]，然后分析具体的对象数目和占用内存大小，从而定位代码。

3、jmap -dump:live,format=b,file=xxx.xxx [pid]，然后利用MAT工具分析是否存在内存泄漏等等。

# Java运行参数设置

Heap Size 最大最好不要超过可用物理内存的80％。建议将-Xms和-Xmx选项设置为相同，而-Xmn为1/4的-Xmx值。


-Xms：初始值 
-Xmx：最大值 
-Xmn：最小值

# FullGC频繁怎么排除？调优？ CPU沾满调优？
Jmap是一个可以输出所有内存中对象的

1. 分析dump文件，也叫做java 转储文件
2. 内存泄漏工具MAT


**如何生成转储文件**
1. jmap -dump:format=b,file=20170307.dump 16048  
>file 是自己定义的文件格式，后面一个数字是进程的pid

**使用jvisualvm来分析dump文件**
