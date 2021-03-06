# 面向报文和面向字节流


## 面向报文

- 面向报文的传输方式是应用层交给UDP多长的报文，UDP就照样发送，即一次发送一个报文。

- 因此，应用程序必须选择合适大小的报文。若报文太长，则IP层需要分片，降低效率。

- 若太短，会是IP太小。UDP对应用层交下来的报文，既不合并，也不拆分，而是保留这些报文的边界。

- 这也就是说，应用层交给UDP多长的报文，UDP就照样发送，即一次发送一个报文。

UDP socket 没有发送缓存区这个概念，应用程序

**核心**
 
 你发送多少过来，我就发送多少过去，然后不合并也拆分
 
## 面向字节流

- 虽然应用程序和TCP的交互是一次一个数据块（大小不等），但TCP把应用程序看成是一连串的无结构的字节流。
- TCP有一个缓冲，当应用程序传送的数据块太长，TCP就可以把它划分短一些再传送。
- 如果应用程序一次只发送一个字节，TCP也可以等待积累有足够多的字节后再构成报文段发送出去。
 
 
 **tcp可以对用户数据进行一个拆分和合并，只要保证字节流的顺序就行**
 
 
## 参考链接

[面向报文（UDP）和面向字节流（TCP）的区别](https://blog.csdn.net/liuyanfeier/article/details/52787037)

[TCP/UDP的接收缓冲区和发送缓冲区](https://blog.csdn.net/Swallow_he/article/details/84392285)