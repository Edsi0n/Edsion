# TCP 协议

> TCP 协议简单来说是一种位于传输层的，面向连接的、可靠的、基于字节流的传输层通信协议.

TCP 协议的特点:

- TCP 是面向连接的传输层协议。比如说 TCP 的三次握手，四次分手，针对的都是连接。
- 每一条 TCP 连接只能有两个端点，每一条 TCP 连接是点对点的。也就是说 TCP 是不同计算机之间的进程的通信。
- TCP 提供可靠交付的服务，无差错，不丢失，不重复，按序到达。总结一下就是，可靠有序，不丢不重。
- TCP 提供全双工通信。全双工指的是连接双方可以同时收发数据。在收发两端都有发送缓存和接收缓存，发送缓存就是一个准备发送的队列，接收缓存是一个准备接收的队列。
- TCP 面向字节流。如下图，我们解释一下什么是面向字节流

<img src="/img/question/network/tcp.png" alt="tcp" title="tcp" class="zoom-custom-imgs">

图中的 1，2，3，4.....数据块，每一个表示一个字节。tcp 将应用层的数据变为了这样的字节进行发送.

TCP 报文的首部格式
如下图所示，我们看一下比较重要的一些首部字段，这里我们介绍固定的 20 字节的 TCP 首部

<img src="/img/question/network/tcphead.png" alt="tcp首部" title="tcp首部" class="zoom-custom-imgs">

- 源端口和目的端口分别是指发送方应用程序的端口和目的方应用程序的端口号。
- 序号是指在一个 TCP 连接中传送的字节流中的每一个字节都按顺序编号，本字段表示本报文段所发送数据的第一个字节的序号。

- 确认号是指期望收到对方下一个报文段的第一个数据字节的序号。弱确认好位 n，则证明到需要 N-1 为止所有的数据都已经正确收到。如下图，我们举例说明一下

<img src="/img/question/network/tcpqr.png" alt="tcp" title="tcp" class="zoom-custom-imgs">


接收方收到了 1，2，3 个字节组成的数据包，然后接收方就会发送一个确认报文给发送方，其中确认报文的确认号就应该是 4，因为 1，2，3 这三个字节的组成的数据包已经收到了。

- 数据偏移指的是 TCP 报文段的数据起始处举例 TCP 报文段的起始处有多远。
- 6 个控制位介绍如下
  |控制位|作用|
  |:-|:-|
  |ACK|置 1 时表示确认号合法，为 0 的时候表示数据段不包含确认信息，确认号被忽略|
  |PSH|置 1 时请求的数据段在接收方得到后就可直接送到应用程序，而不必等到缓冲区满时才传送|
  |RST|置 1 时重建连接。如果接收到 RST 位时候，通常发生了某些错|
  |SYN|置 1 时用来发起一个连接|
  |FIN|置 1 时表示发端完成发送任务。用来释放连接，表明发送方已经没有数据发送了|
  |URG|紧急指针，告诉接收 TCP 模块紧要指针域指着紧要数据|
