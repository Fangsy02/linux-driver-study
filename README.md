# 嵌入式Linux驱动学习日志
- 起点：2026年1月19日
- 目标：能独立写/维护中型外设驱动 + 看懂boot流程
- 计划：阶段0 → 内核模块 + 字符设备（零硬件先练）
- 当前进度：第0周（刚开始记录）
### 进度日志
- 2026.1.20：linux-6.18.5 源码解压 + make defconfig 成功
- 2026.1.20：第一次内核编译完成（make -j4, x86_64 defconfig），生成 arch/x86/boot/bzImage
- 2026.1.21：完成第一个内核模块 hello.ko 编写与编译（生成成功）；insmod 失败（Invalid module format，WSL2 默认内核限制），下一步配置自定义内核
* 2026.1.25：使用微软官方 WSL2 内核 6.6.121 成功替换（uname -r 确认）；重新编写 hello.c + Makefile；make 编译 hello.ko；sudo insmod 加载成功，dmesg 输出 "Hello from kernel!"；rmmod 卸载成功，输出 "Goodbye from kernel!" —— 第一个内核模块运行成功！
* 2026.1.28：完成带参数 hello 模块（module_param）；完成简单杂项字符设备（misc_register，能 echo/cat /dev/myhello）
* 2026.1.29：完成简单杂项字符设备（misc_register）；成功 echo/cat /dev/myhello 读写；dmesg 看到日志：
* * 2026.2.3：完成简单 platform_driver + 自动注册虚拟平台设备；insmod 加载成功，dmesg 看到 probe/remove 输出（平台匹配机制跑通）
* 2026.2.4：platform_driver 加资源获取（platform_get_resource）；虚拟设备注册成功，dmesg 看到 MEM (0x10000000-0x10000fff) 和 IRQ (42) 资源信息；probe/remove 全触发
