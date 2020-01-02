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
