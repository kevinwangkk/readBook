## TCP状态机

TCP协议的运行可划分为三个阶段：

​	连接建立(*connection establishment*)、

​	数据传送（*data transfer*）和

​	连接终止（*connection* *termination*）



资源使用情况

- ​	服务器端的连接数量是无限的，只受内存的限制。

- ​	客户端的连接数量，过去由于在发送第一个SYN到服务器之前需要先分配一个随机空闲的端口，这限制了客户端IP地址的对外发出连接的数量上限。从Linux 4.2开始，有了socket选项IP_BIND_ADDRESS_NO_PORT，它通知Linux内核不保留usingbind使用端口号为0时内部使用的临时端口（ephemeral port），在connect时会自动选择端口以组成独一无二的四元组（同一个客户端端口可用于连接不同的服务器[套接字](https://zh.wikipedia.org/wiki/%E5%A5%97%E6%8E%A5%E5%AD%97)；同一个服务器端口可用于接受不同客户端套接字的连接）



### 1. TCP三次握手(three-way handshake)

1. client  发送SYN 到  server
2. server 响应SYN,回复ACK 到 client
3. client 响应 回复ACK 到 server

### 2. TCP四次挥手（four-way handshake）

1. 

### 3. int *tcp_v4_do_rcv*(struct sock *sk, struct sk_buff *skb)



