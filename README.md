# KernelMode AntiCheat Demo Project
---------------------------------------------------------------------------------------------------------

这个项目里面有很多驱动的CallBack可以参考。Start不多，简单看看即可。基本功能是在驱动中进行驱动保护。

Just a sample of how you can code a basic AntiCheat nowadays. Please note that this project is completely unfinished as it was just a part of my Bachelor's Final Project.
This shit has been developed in less that a week so don't expect something serious here as I only made basic process protection as well as basic manually mapped drivers detection.
I'll probably contribute more in the future if I'll get more free time.

只是一个例子，用来展示如何编写一个基本的反作弊程序（反外挂）。请注意，这个项目是完全未完成的，因为它只是原作者的学士学位期末项目的一部分。这个东西在不到一周的时间里就开发出来了，所以不要指望会有什么严重的问题，因为原作者只做了基本的进程保护以及基本的手动映射驱动检测。

# What's done here?

## Driver
- Uses IOCTL for UM client to communicate with the Driver (access allowed for Client & Game only)
- Dynamic imports resolver for both ntoskrnl.exe & CI.dll
- Strip handles for Protected Process via PreObCallback
- Runtime Protected Process pickup via LoadImage Callback
- Protected Process validation by verifying it's Digital Signature via MS Code Integrity (CI.dll) -> honestly the most interesting part here.
- Various System Threads scans for mapped drivers (Win32StartAddress + KernelStack)
- Driver Dispatch scanning for mapped drivers
- PiDDBCache scanning (doing this in 2021 is pretty meme but who cares lol)
- 使用IOCTL为UM客户端与驱动程序通信(仅允许客户端和游戏访问)
- 动态导入解析器的ntoskrnl.exe和CI.dll
- 通过PreObCallback条带化受保护进程的句柄
- 运行时保护进程拾取通过LoadImage回调
- 通过MS Code Integrity (CI.dll)验证它的数字签名来保护进程验证
- 各种系统线程扫描映射的驱动程序(Win32StartAddress + KernelStack)
— Driver分配扫描映射的驱动程序
- PiDDBCache扫描(2021年做这个很有趣，但谁在乎呢，哈哈)


### TODO:
MINIFILTER!!! Never do that shitty LoadLibrary hooking in UM I've done here!
The only reason I made it this way is that I had no time to develop proper MiniFilter.
That's probably the first thing I should fix in this project.

## Client
- Load the Driver, spawning Protected Process
- Dump ntoskrnl's PDB for some offsets
- Send requests for Driver to collect Kernel Detection info
- Scan and collect all Windows on-top of test "Game" Window
- Send all the info to the server via sockets

## Server
- Multithreaded TCP done via Poco Library
- Receive data from Clients and update SQL DB using collected data

## DLL
- The most useless part here as only thing it does is just hooking LoadLibrary
- No real internal detection were done here


