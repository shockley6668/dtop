# Jetson有Jtop,Linux有Htop,RDK也有Dtop！

> 作者：SkyXZ
>
> CSDN：[SkyXZ～-CSDN博客](https://blog.csdn.net/xiongqi123123?spm=1000.2115.3001.5343)
>
> 博客园：[SkyXZ - 博客园](https://www.cnblogs.com/SkyXZ)
>
> 本项目基于[btop](https://github.com/aristocratos/btop)开源项目进行二次开发，旨在为RDK平台提供更强大的系统监控工具。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Linux系统下有Htop可以作为系统监控，英伟达的Jetson也有第三方的Jtop，咱们RDK虽然也提供了`hrut_somstatus`来查看BPU的使用率，但终归不是很方便，超哥也做了一个[Web_RDK_Performance_Node](https://github.com/WuChao-2024/Web_RDK_Performance_Node)：

![image-20250730203240082](https://img2024.cnblogs.com/blog/3505969/202507/3505969-20250730203244517-348834443.png)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**但是在串口环境下无法快速的查看当前系统资源，于是！！！Dtop闪亮出炉！！！！！！！**目前已适配**RDKS600**、**RDKS100**和**RDKX5**，可以在这个界面快速的查看BPU等系统资源的占用率，以及可以点击右上角快速切换CPU的调度策略！

![image-20250730203625062](https://img2024.cnblogs.com/blog/3505969/202507/3505969-20250730203629184-2144438723.png)

## 快速安装

### RDK S600（Ubuntu 24.04 / ARM64）

以下预编译包适用于 **RDK S600、ARM64、Ubuntu 24.04、glibc 2.39 及以上版本**。r2 版本每 100 ms 采样一次四个 BPU 核心，可捕获默认 2 秒界面刷新容易漏掉的短推理任务；程序在未设置 `LANG` 或 `LC_*` 环境变量时会自动使用 `C.UTF-8`，可直接在全新系统中运行。

```bash
wget https://github.com/shockley6668/dtop/releases/download/s600-v1.1.0-r2-20260730/dtop-rdk-s600-ubuntu24.04-arm64.tar.gz
echo "0bdcf98ccc997e15e1842666b3ac9a85cf92d51b9738b808884b19f1239aa35d  dtop-rdk-s600-ubuntu24.04-arm64.tar.gz" | sha256sum -c -
tar -xzf dtop-rdk-s600-ubuntu24.04-arm64.tar.gz
cd dtop-rdk-s600-ubuntu24.04-arm64
sudo ./install.sh
sudo dtop
```

### RDK S100 / RDK X5（Ubuntu 22.04 / ARM64）

```bash
# 下载预编译文件
wget https://github.com/xiongqi123123/dtop/releases/download/v1.1.0/dtop-arm64-ubuntu22.04.tar.gz
# 解压安装
tar -xzf dtop-arm64-ubuntu22.04.tar.gz
sudo cp dtop /usr/local/bin/
# 即可体验
sudo dtop
```

## 从源码编译

```bash
git clone https://github.com/shockley6668/dtop.git
cd dtop
make -j$(nproc)
sudo make install
sudo dtop
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;当前代码已实现RDKS600上4个BPU核心、GPU、3个VPU和2个JPU的使用率监控，并根据`BPUx-TSx`传感器显示BPU平均温度；同时保留RDKS100和RDKX5的BPU、GPU、VPU、JPU监控，以及S100 Main和MCU域温度监控。

![image-20250802204402978](https://img2024.cnblogs.com/blog/3505969/202508/3505969-20250802204405140-1529566624.png)

![image-20250802204636895](https://img2024.cnblogs.com/blog/3505969/202508/3505969-20250802204638778-230886562.png)









