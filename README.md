# CVE-2020-0796-CNA

根据[danigargu](https://github.com/danigargu/CVE-2020-0796)提供的POC进行修改，实现了Windows 10的提权复现并根据[stephenfewer](https://github.com/stephenfewer/ReflectiveDLLInjection)的反射DLL项目与CobaltStrike文档提供的接口开发了AggressorScripts。

**本仓库仅仅为了交流反射DLL注入的实现与测试，因此不提供Release版本，请自行编译**

> 具体还未进行稳定性测试，欢迎交流

## 影响版本（本地提权+远程蓝屏）

- Windows 10 Version 1903 for 32-bit Systems
- Windows 10 Version 1903 for x64-based Systems
- Windows 10 Version 1903 for ARM64-based Systems
- Windows Server, Version 1903 (Server Core installation)
- Windows 10 Version 1909 for 32-bit Systems
- Windows 10 Version 1909 for x64-based Systems
- Windows 10 Version 1909 for ARM64-based Systems
- Windows Server, Version 1909 (Server Core installation)

## 漏洞加固

1. 更新系统

操作步骤：设置->更新和安全->Windows更新，点击“检查更新”。

2. 禁止SMB的压缩功能

运行`regedit.exe`，打开注册表编辑器，在`HKLM\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters`建立一个名为`DisableCompression`的`DWORD`，值为`1`。

3. 使用防火墙对SMB通信445端口进行封禁

补丁地址：https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB4551762

