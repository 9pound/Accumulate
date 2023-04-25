# WEB页面的请求历程

1、DHCP 广播UDP 报文，交换机接受，返回IP，DNS地址

2、拿着url 向DNS 发送UDP报文，获取URL对应的IP地址

3、TCP 三次握手，简历TCP连接

4、HTTP请求，别servelet拦截，返回带有