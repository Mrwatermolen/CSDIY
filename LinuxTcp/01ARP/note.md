# ARP Protocol: The Address Resolution Protocol

> See more:
> Note: [CS144-week_1](../../CS144/week-1/note.md)
> Lab: [CS144-lab_6](../../CS144/lab5/note.md)
>

ARP协议能实现任意网络层地址到任意物理地址的转换，不过本书仅讨论从IP地址到以太网地址（MAC地址）的转换。其工作原理是：主机向自己所在的网络广播一个ARP请求，该请求包含目标机器的网络地址。此网络上的其他机器都将收到这个请求，但只有被请求的目标机器会回应一个ARP应答，其中包含自己的物理地址。
