Reference: CC3200 Networking Solution Programmer's Guide.pdf  
---
> The SimpleLink™ Wi-Fi® CC3100 and CC3200 are the next generation in embedded Wi-Fi. The CC3100 Internet-on-a-chip™ can add Wi-Fi and internet to any microcontroller (MCU), such as TI's ultra-low power MSP430™. The CC3200 is a programmable Wi-Fi MCU that enables true, integrated Internet-of-things (IoT) development. The Wi-Fi network processor subsystem in both SimpleLink Wi-Fi devices integrates all protocols for Wi-Fi and Internet, greatly minimizing MCU software requirements. With built-in security protocols, SimpleLink Wi-Fi provides a simple yet robust security experience.  

SimpleLink™Wi-Fi®CC3100和CC3200是下一代嵌入式Wi-Fi。CC3100“芯片上互联网”可以将Wi-Fi和互联网添加到任何微控制器（MCU），如TI的超低功耗MSP430™。CC3200是一款可编程Wi-Fi MCU，能够实现真正的集成物联网（IoT）开发。SimpleLink Wi-Fi设备中的Wi-Fi网络处理器子系统集成了Wi-Fi和Internet的所有协议，极大地降低了对MCU软件的要求。具有内置安全性协议，SimpleLink Wi-Fi提供了简单而强大的安全体验。

---
> The SimpleLink host driver includes a set of six logical and simple API modules:  

> - Device API – Manages hardware-related functionality such as start, stop, set, and get device configurations.
- WLAN API – Manages WLAN, 802.11 protocol-related functionality such as device mode (station, AP, or P2P), setting provisioning method, adding connection profiles, and setting connection policy.
- Socket API – The most common API set for user applications, and adheres to BSD socket APIs.
- NetApp API – Enables different networking services including the Hypertext Transfer Protocol (HTTP) server service, DHCP server service, and MDNS client\server service.
- NetCfg API – Configures different networking parameters, such as setting the MAC address, acquiring the IP address by DHCP, and setting the static IP address.
- File System API – Provides access to the serial flash component for read and write operations of networking or user proprietary data.

SimpleLink主机驱动程序包括一组六个逻辑和简单的API模块：

- Device API：管理与硬件相关的功能，如启动、停止、设置和获取设备配置。  
- WLAN API：管理WLAN、802.11协议相关功能，如设备模式（站点、AP或P2P）、设置设置方法、添加连接配置文件和设置连接策略。  
- Socket API：用户应用程序最常用的API集，遵循BSD Socket API。
- NetApp API：支持不同的网络服务，包括超文本传输协议（HTTP）服务器服务、DHCP服务器服务和MDNS客户机/服务器服务。
- NetCfg API：配置不同的网络参数，例如设置MAC地址、通过DHCP获取IP地址和设置静态IP地址。  
- File System API：提供对串行闪存组件的访问，用于网络或用户专有数据的读写操作。 

---

> This chapter explains the software blocks needed to build a networking application. In addition, this chapter describes the recommended flow for most applications. The information provided is for guidance only. Programmers have complete flexibility on how to use the various software blocks. Programs using the SimpleLink device consist of the following software blocks: 

> - Wi-Fi subsystem initialization – Wakes the Wi-Fi subsystem from the hibernate state.
- Configuration – Refers to init time configuration that occurs infrequently, such as when changing the Wi-Fi subsystem from a WLAN STA to WLAN soft AP, changing the MAC address, and so forth.
- WLAN connection – The physical interface must be established. There are numerous ways to do so; the simplest way is to manually connect to an AP as a wireless station.  
• DHCP – Although not an integral part of the WLAN connection, the user must wait for the receiving IP address before continuing to the next step of working with TCP and UDP sockets.
- Socket connection – At this point, the application must set up the TCP\IP layer. Separate this phase into the following parts:  
• Creating the socket – Choose TCP, UDP, or RAW sockets, whether to use a client or a server socket, defining socket characteristics such as blocking or non-blocking, socket timeouts, and so forth.  
• Querying for the server IP address – In most occasions, when implementing a client side communication, the remote server side IP address is unknown, which is required for establishing the socket connection. This can be done by using DNS protocol to query the server IP address by using the server name.  
• Creating socket connection – When using the TCP socket, a proper socket connection must beestablished before performing a data transaction.  
- Data transactions – Once the socket connection is established, transmit data both ways between the
client and the server, by implementing the application logic.
- Socket disconnection – Upon finishing the required data transactions, TI recommends performing a graceful closure of the socket communication channel.
- Wi-Fi subsystem hibernate – When not working with the Wi-Fi subsystem for a long period of time, TI recommends putting it into hibernate mode


••••••
本章介绍构建网络应用程序所需的软件模块。此外，本章介绍了大多数应用程序的推荐流程。提供的信息仅供参考。程序员在如何使用各种软件块方面具有完全的灵活性。使用SimpleLink设备的程序由以下软件块组成：

- Wi-Fi子系统初始化：将Wi-Fi子系统从休眠状态唤醒。
- 配置：指不经常发生的初始化时间配置，例如将Wi-Fi子系统从WLAN STA更改为WLAN软AP、更改MAC地址等。
- WLAN连接：必须建立物理接口。有很多方法可以做到这一点；最简单的方法是作为无线电台手动连接到AP。
	•DHCP–虽然不是WLAN连接的组成部分，但用户必须等待接收到的IP地址，然后才能继续下一步使用TCP和UDP套接字。

- 套接字连接：此时，应用程序必须设置TCP\IP层。将此阶段分为以下部分：
	•创建套接字：选择TCP、UDP或原始套接字，是使用客户端还是服务器套接字，定义套接字特性，如阻塞或非阻塞、套接字超时等。
	•查询服务器IP地址：在大多数情况下，在实现客户端通信时，远程服务器端IP地址未知，这是建立套接字连接所必需的。这可以通过使用DNS协议通过使用服务器名称查询服务器IP地址来完成。

	•创建套接字连接：使用TCP套接字时，必须在执行数据事务之前建立正确的套接字连接。

- 数据事务：一旦建立了套接字连接，就可以在客户端和服务器，通过实现应用程序逻辑。

- 套接字断开连接：在完成所需的数据事务后，TI建议对套接字通信通道执行正常关闭。

- Wi-Fi子系统休眠：当长时间不使用Wi-Fi子系统时，TI建议将其置于休眠模式
