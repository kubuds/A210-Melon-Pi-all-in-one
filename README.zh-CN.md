# 知合 A210 资源总汇（SODIMM V2 / V3 · 算力棒）

[简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [English](README.en.md) · [Русский](README.ru.md) · [日本語](README.ja.md) · [Deutsch](README.de.md) · [Español](README.es.md)

知合计算 A210（对外也叫「阿基米德 A210」）能公开找到的资源都收在这一页：官方文档与规格书、**可直接下载的官方镜像**、按板型分的烧录指南、硬件设计文件、上游内核与固件进展、GitHub 与 Gitee 项目，以及 B 站和 YouTube 上真的用了这块板子的视频。

本页不镜像任何固件与文档本体，只给出处。**记的是链接与事实，不是使用承诺** —— 刷机前请核对板卡版本、镜像说明与校验值。

> **先把名字对上，这块板子的叫法比一般开发板乱。**
>
> - **芯片**：知合计算 A210，产品系列名「阿基米德」（Archimedes A210），通推一体异构 AI SoC。
> - **板卡形态**：SODIMM 核心板 + 底板（**V1 / V2 / V3** 三代底板），另有 **A210 算力棒（Dongle）** 形态。
> - **「Melon Pi / MelonPi」是谁在叫**：知合官方文档与规格书里**没有**这个名字（官方只用「A210 SODIMM V1/V2/V3」）；它出现在上游 Linux 补丁的设备树文件名（`a210-melonpi-v1.dts` / `-v2.dts`）、玄铁在华秋开源硬件页的标题（「玄铁 MelonPi A210」）以及部分媒体报道里。看到 Melon Pi，指的是同一块板的内核/社区叫法。
> - **别和 A200 混**：知合还有 A200 平台，官方 Ubuntu 镜像只给 A200；A210 官方只出 Buildroot 与 Debian 桌面两套镜像。

---

## 1. 关键规格

| 项目 | 参数 |
| --- | --- |
| SoC | 知合计算 A210（通推一体异构 AI SoC） |
| CPU | 4× 达摩院玄铁 C920 + 4× 达摩院玄铁 C908，RV64GCV（带向量） |
| 频率 | 官方规格书写 1.9 GHz；CNX Software 报道写 C920 最高 2.3 GHz、C908 1.9 GHz（两处口径不一致，以你手上批次与规格书为准） |
| GPU | 支持 Vulkan 1.1/1.2/1.3、OpenCL 1.1/1.2/2.0、OpenGL ES 1.1/2.0/3.0/3.1/3.2（官方规格书未点名型号；「IMG BXM-4-64」出自 RuyiSDK 支持矩阵元数据） |
| NPU | 12 TOPS@INT8，支持 INT4/INT8/INT16/FP8/FP16/BF16 |
| 内存 | 4 / 8 / 16 GB 64-bit LPDDR4x，最高 4266 Mbps |
| 存储 | eMMC 5.1/5.0、NOR/NAND Flash、SD 3.0 |
| 网络 | 2× 10/100/1000 Mbps 千兆网口 |
| 显示 | 1× HDMI 2.0、1× 4-lane MIPI DSI、DP / eDP（受 USB 复用限制） |
| 摄像头 | 1× 4-lane + 1× 2-lane，或 3× 2-lane MIPI CSI |
| 扩展 | PCIe x4 / x2 + x1、x2 + 2× SATA、2× x1 + 2× SATA；2× SPI、1× QSPI、7× I²C、10× UART、3× 5ch PWM、2× 1ch ADC |
| USB | 1× USB 3.1（DP Alt）、2× USB 2.0 |
| 音频 | 3× 2ch I2S/PCM、1× TDM/PCM |
| 供电 / 温度 | 核心板 5V/5A（最低）；底板 12V DC 输入；-20 °C ~ 60 °C |
| 核心板尺寸 | 59.66 mm × 69.94 mm，260-pin SODIMM |
| 官方 OS | Linux（Debian 桌面 / Buildroot） |

**关于 RVA23 有两种说法**：OMG! Ubuntu 在 2025-07 的报道里说 A210 支持 RVA23 全部必选与可选扩展；CNX Software 随后在评论区与正文更正，认为 A210 属 RVA22、RVA23 是下一代的 A600。**这条没有权威结论，别拿它做选型依据。**

数据来源：官方「A210 产品规格书」与「核心板用户指南」，及[华秋开源硬件社区的产品页](https://p.eda.cn/d-1389550606774960128)（同一份规格表的转载）。

---

## 2. 官方文档（知合计算开发者文档中心）

官方文档站是 **developer.zhcomputing.com**，当前 **2.9.0**，另有 **2.8.1** 历史版本与 `/en/` 英文版。该站前端渲染，`curl` 取不到正文，用浏览器打开。

**总入口**

- [文档中心首页](https://developer.zhcomputing.com/zh/docs/intro) · [English](https://developer.zhcomputing.com/en/docs/intro/)
- [A210 文档目录](https://developer.zhcomputing.com/zh/docs/A210/) · [English](https://developer.zhcomputing.com/en/docs/A210/)
- [2.8.1 历史版本](https://developer.zhcomputing.com/zh/docs/2.8.1/category/sdk)

**规格书与烧录（按板型分册，选错会烧不进去）**

- [A210 产品规格书（HTML 全文）](https://developer.zhcomputing.com/zh/docs/A210/A210_Datasheet) —— 功能特性、封装、引脚定义与时序
- [镜像烧录指南（索引）](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/)
- [SODIMM V2 烧录指南](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V2_Burning_Instruction) —— 12V DC 供电、TTL 115200 调试口、USB-A 烧录口；按住烧录键 + 复位进 USB 模式；Windows 用 platform-tools r34.0.5 + usb_driver r13，Linux 用 android-sdk-platform-tools
- [SODIMM V3 烧录指南](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V3_Burning_Instruction)
- [算力棒（Dongle）烧录指南](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_Dongle_Burning_Instruction) —— 这个形态很容易被漏掉

**硬件平台**

- [核心板用户指南](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/核心板说明) —— 关键参数、尺寸、260-pin 引脚定义
- [SODIMM V2 底板用户指南](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V2_baseboard_developer_guide) —— 接口、BOOT_SEL、PCIe RC/EP 切换、UART4 调试串口
- [SODIMM V2 底板原理图](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V2)（V1/V3 与算力棒各有独立页）
- [硬件设计指南](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/) —— 自研载板前必读
- [PINMUX](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/A210-PINMUX) · **直接下载表格**：[A210-PINMUX_20260119.xlsx](https://developer.zhcomputing.com/zh/docs/pdf/A210/Hardware-Platform/A210-PINMUX_20260119.xlsx)（约 39 KB，实测可下）

**SDK**

- [SDK 总览](https://developer.zhcomputing.com/zh/docs/category/sdk) · [快速上手（含镜像下载表）](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/Basic_quick_start_guide)
- [Buildroot 开发指南](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/Buildroot_developer_guide) —— 从 zdocker 环境到 `./build.sh -b buildroot a210`
- [TORQ SDK 介绍](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ%20SDK%E4%BB%8B%E7%BB%8D) —— 12 TOPS NPU 的上手入口，配套 TORQ-Toolkit 与 TORQ-LLM API
- 其它分类：[快速上手](https://developer.zhcomputing.com/zh/docs/category/快速上手) · [开发环境构建](https://developer.zhcomputing.com/zh/docs/category/开发环境构建) · [多媒体](https://developer.zhcomputing.com/zh/docs/category/多媒体) · [AI](https://developer.zhcomputing.com/zh/docs/category/ai)

**厂商与制品牌**

- [玄铁官网 A210 产品页](https://www.xrvm.cn/product/board/4565261785988403200)（前端渲染，抓不到正文）
- [玄铁官网首页](https://www.xrvm.cn/) · [达摩院玄铁 C920](https://www.xrvm.cn/product/xuantie/C920) · [C908](https://www.xrvm.cn/product/xuantie/C908)
- 知合计算主站 `www.zhcomputing.com` 实测直连与走代理均 504，目前唯一可用的官方站点就是上面的文档中心；商务联系 business@zhcomputing.com

> 文档站页脚的「GitHub」链接是占位符（指向 `github.com/your-org`），不是真项目，不要引用。

---

## 3. 官方镜像（可直接下载）

只有两套：**Buildroot**（轻）与 **Debian 桌面**，统一以 `a210-evb` 命名，都走 fastboot 分区包。**没有官方 Ubuntu 镜像**（Ubuntu 只给 A200）。

| 镜像 | 版本 | 大小 | 下载 |
| --- | --- | --- | --- |
| Buildroot 预编译镜像 | v2.9.0（当前） | 179.4 MB | [br2image-v2.9.0-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/br2image-v2.9.0-a210_evb.tar.gz) |
| Debian 桌面镜像 | v2.9.0（当前） | 738.4 MB | [diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz) |
| Buildroot 预编译镜像 | v2.8.1（回滚用） | 175.9 MB | [br2image-v2.8.1-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/br2image-v2.8.1-a210_evb.tar.gz) |
| Debian 桌面镜像 | v2.8.1（回滚用） | 734.8 MB | [diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz) |

- 解压后得到 `emmc-*.img`、`bootzero-rvbl.bin`、`fastboot_images.sh` / `.bat`，进烧录模式后直接跑脚本
- **官方制品库目录索引**（比文档表格更全）：[downloads/release/](http://developer.zhcomputing.com/downloads/release/) —— `zhihesdk` 下有 v2.7.0 / v2.8.0 / v2.8.1 / v2.9.0，`npu` 下有 v1.3–v2.1（ovx-compiler、torq-llm、uca-nn、viplite），`tools` 下有 1.17 GB 的 `ubuntu-24.04-x86_64.v1.7.0.tar.gz` 构建容器
- 想用 RuyiSDK 复现安装：[ruyisdk/packages-index PR #208](https://github.com/ruyisdk/packages-index/pull/208) 把 fastboot 流程、2.8.1 的 Buildroot 与 Debian 镜像包、分区表都做成了 ruyi 条目，内含分区映射与校验和，可用于交叉核对

---

## 4. 硬件设计文件（开源底板 PDF 与原理图）

[玄铁 MelonPi A210 高性能开发板 —— SODIMM V3 开源底板](https://p.eda.cn/d-1389550606774960128)（华秋开源硬件社区，发布者 XuanTie 玄铁，**OpenAtom OHL 1.0**）提供：

- **A210 SODIMM 底板原理图.zip**（2.69 MB）
- **A210 最小系统 原理图设计建议.pdf**（7.80 MB）
- **A210 最小系统 PCB 设计建议.pdf**（15.55 MB）
- **A210 产品规格书.pdf**（399 KB）—— 目前能拿到 **PDF 版**规格书的唯一渠道（官方只提供 HTML）
- **A210-PINMUX_20260119.xlsx**（38.89 KB）

注意这是 **V3 底板**，与官方 V2 文档有一代差异。下载需在站内注册登录。

---

## 5. 上游内核、固件与发行版

**上游 Linux 主线**

- [[PATCH 00/18] riscv: add initial support for Zhihe A210 and Melon Pi](https://lists.infradead.org/pipermail/linux-riscv/2026-October/101909.html) —— 首版主线支持（UART/clock/reset/pinctrl + DT），已在 Melon Pi V2 上 8 核全开验证；设备树文件名 `a210-melonpi-v1.dts` / `-v2.dts` 就是「Melon Pi」这个名字的真正出处
- [[PATCH RFC 00/18] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-October/102222.html) —— 2026-10-27 的重做版（作者编号 v2）：A210 还有一颗 E902 管理核，时钟与复位寄存器实际由它运行的 Zephyr SCMI 固件掌管，这一版删掉原生 clk/reset 驱动、改走标准 SCMI clock/reset 协议，另加 AP→E902 门铃 mailbox 驱动；已在 Melon Pi V2 上 8 核起到 UART shell。原生驱动那版（上面那条）与这一版**截至 2026-11-02 都还没进主线**；最新的 v3 见下条
- [[PATCH RFC v3 00/17] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-November/102729.html) —— 2026-11-02 的 v3：rebase 到 v7.4-rc1；`arm_scmi` 去掉 ARM 架构依赖（RISC-V 也能编），SCMI clock/reset ID 从 dt-bindings 移进 DTS 旁的 header，mailbox 绑定改为固定的 local / remote 区域；Melon Pi V2 用 riscv defconfig 8 核起到串口 shell。仍因等知合固件原生支持 SCMI 而保持 RFC

**内核与设备树（还在各家的开发线里）**

- [RVCK Linux](https://github.com/RVCK-Project/rvck) —— `rvck-6.6` 分支里设备树最全： [a210.dtsi](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi) · [a210-melon-pi.dts](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts) · [知合设备树绑定](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml)；提交检索有 41 条 A210 相关提交，含 GPIO/UART/timer/DMA/sdhci
- [RVCK：A210 外设支持跟踪 issue](https://github.com/RVCK-Project/rvck/issues/381) · [已合并的外设支持 PR](https://github.com/RVCK-Project/rvck/pull/382)
- [RevyOS Linux](https://github.com/revyos/linux) —— [A210 维护条目](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d) · [温控与看门狗设备树](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4) · [PWM 驱动](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d) · [Melon Pi V2 音频走线](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146)。注意这些提交不在默认分支上
- [RISE Project：riseproject-dev/linux](https://github.com/riseproject-dev/linux) —— 存在 `alibaba-a210` 分支

**引导与固件**

- [riseproject-dev/u-boot](https://github.com/riseproject-dev/u-boot) —— `v2024.10-a210` 分支，树内含 `a210.dts`、`a210-soc.dtsi`、`board/zhihe/a200-evb`
- [riseproject-dev/opensbi](https://github.com/riseproject-dev/opensbi) —— `v1.5-a210` 分支，含 `platform/generic/zhihe/a210.c`
- [openeuler-riscv/opensbi-zhihe-a210](https://github.com/openeuler-riscv/opensbi-zhihe-a210) —— OpenSBI 厂商移植
- [revyos/ruyiedk2](https://github.com/revyos/ruyiedk2) —— EDK2/UEFI 平台固件，README 写明支持 Melon Pi V1 与 V2，`docs/melonpi.md` 记录原生 RAM 启动与 USB Fastboot
- SCMI 启动链（`a210/scmi-v3` 分支，2026-11-02）：[coreboot](https://github.com/revyos/coreboot/tree/a210/scmi-v3) · [OpenSBI](https://github.com/revyos/opensbi/tree/a210/scmi-v3) · [EDK2](https://github.com/revyos/edk2/tree/a210/scmi-v3) · [RevySR/linux 含其余外设的完整树](https://github.com/RevySR/linux/tree/a210/scmi-v3) —— 与 v3 RFC 配套；早期的 `a210/scmi` 分支仍在，`revyos/ruyiedk2` 也有 `a210/scmi-v3`
- [RevySR/zephyr `xuantie/scmi-v3`](https://github.com/RevySR/zephyr/tree/xuantie/scmi-v3) —— 跑在 E902 上的 SCMI 服务端固件（Zephyr），电源、PMIC 与 CPU DVFS 时序都由它负责
- [RevySR/linux `a210/vcodec-v3`](https://github.com/RevySR/linux/tree/a210/vcodec-v3) —— 2026-11-02 新增的视频解码开发线：hantro 驱动加入 A210 的 VC9000D 解码器（含 VP9），并补上对应的设备树节点

**发行版层**

- [riscv/meta-riscv](https://github.com/riscv/meta-riscv) —— OpenEmbedded/Yocto 的 RISC-V 层，机器表里有 `zhihe-a210`（"Zhihe Computing Archimedes A210"，OSU-OSL 主线内核，TFTP netboot），`conf/machine/zhihe-a210.conf` 实际存在
- [RevySR/rvck-image](https://github.com/RevySR/rvck-image) —— rootfs/磁盘镜像构建，README 给出「通过 Melon Pi EDK2 fastboot 刷写」流程（F9 进 Fastboot，`flash emmc0`）
- [riseproject-dev/android_manifest](https://github.com/riseproject-dev/android_manifest) —— RISE Android 17 BSP，覆盖 Alibaba A210 EVB，给出 lunch 目标 `aosp_a210_evb-trunk_staging-userdebug`
- [riseproject-dev/android_kernel_device](https://github.com/riseproject-dev/android_kernel_device) —— 上面的 Kleaf 设备片段（`alibaba/a210/`、`zhihe_a210.fragment`）
- [RuyiSDK 支持矩阵：A210 SODIMM V2](https://matrix.ruyisdk.org/zh-CN/boards/A210_SODIMM_V2/)（[源码目录](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2) · [others.yml](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml)）—— Debian 与 Buildroot 均标 `wip`；`wip` 是「在做，没做完」，不等于可用
- [ruyisdk/ruyi](https://github.com/ruyisdk/ruyi) —— 包管理器，有 zhihe 厂商命名规范，但**尚无 A210 专属设备条目**，别以为装上 ruyi 就有 A210 镜像

---

## 6. GitHub 项目一览

A210 的 GitHub 生态很薄，能归成四条线：**RVCK**（设备树最全）、**RevyOS**（内核提交 + EDK2 固件）、**RISE Project**（U-Boot / OpenSBI / Android BSP）、**meta-riscv**（Yocto 机器）。GitHub 上**没有知合的官方组织**（`orgs/zhcomputing` 404），官方资料全在文档站。

上面第 5 节已列出的不再重复；其余相关：

- [kubuds/A210-Melon-Pi-all-in-one](https://github.com/kubuds/A210-Melon-Pi-all-in-one) —— 本索引仓库
- `ruyisdk/packages-index` 的 [PR #208](https://github.com/ruyisdk/packages-index/pull/208) —— ruyi 侧的 A210 设备与烧录策略

---

## 7. Gitee 项目

Gitee 上直接面向 A210 的仓库很少，且 **Gitee 的站内搜索 API 目前对任何关键词都返回空**，所以这一节**不保证穷尽**：

- [agiros/yolov5_torq_camera](https://gitee.com/agiros/yolov5_torq_camera) —— 描述原文「主要用于 A210 单板，可以通过 torq 调用 yolov5 模型，并将识别的结果和画面发送为 AGIROS 话题」。注意 README 还是 Gitee 默认模板
- [agiros/ur5-demo](https://gitee.com/agiros/ur5-demo) —— AGIROS 的 A210 机械臂教程里 `git clone` 的就是这个仓，在 A210 + openEuler 24.03 上做 UR5 视觉抓取；仓库本身不提 A210，是「被 A210 项目实际使用」

> 坑：搜索「a210」会大量命中嘉楠 **K210** 的项目；`gitee.com/zhihe` 是「知和先生」个人号，与知合计算无关。

---

## 8. 视频

**B 站（全站只有 2 条，且没有一条以 Melon Pi 命名）**

- [知合计算 阿基米德 A210 RISC-V 开发板开箱 玄铁 C920 核心 + NPU 通推一体](https://www.bilibili.com/video/BV1fJrnBsENd/) · DSOE1024 · 2026-01-14 · 约 1.7k 播放 —— **目前唯一真正拍这块板子的视频**（2 分 48 秒）
- [知合计算 A210 问世，「产学研」闭环的标杆案例 A600 呼之欲出](https://www.bilibili.com/video/BV19R84zsEVH/) · 石榴派-袁德俊 · 2025-07-26 · 428 播放 —— 峰会资讯解读，不是板子实测

**YouTube（只有 1 条，且是规格罗列 + 导购）**

- [Struggling with local AI projects? This RISC-V dev kit might help](https://www.youtube.com/watch?v=yK5x93THqLE) · 스마트직구연구소 —— 描述写明 Sipeed ZHIHE A210 RISC-V AI Dev Kit，内容是规格罗列、非实测

**没有教程、没有开发实录、没有发布会录像**。知合计算在 B 站与 YouTube 都没有官方账号。这是这块板目前最真实的状况，不粉饰。

---

## 9. 中文教程、实操与报道

- [AGIROS + RISC-V 知合 A210 全栈打通并实机验证](https://ruyisdk.cn/t/topic/2362) —— **目前最完整的中文实操帖**：烧 openEuler 24.03 LTS（含 root 密码 `openEuler12#$`）、网络与静态 IP、一键装 AGIROS 25.12、ur5-moveit-demo、手眼标定、实体 UR5 抓取
- [知合计算 A210 开发板开箱（视频转帖）](https://ruyisdk.cn/t/topic/2412) —— 短帖，看外观与接口布局
- [玄铁 MelonPi A210 SODIMM V3 开源底板](https://p.eda.cn/d-1389550606774960128) —— 硬件侧最实用的一篇（含 22 个接口说明、BOOT_SEL、PCIe RC/EP、UART4）
- 阿里云开发者社区 [第二届 CIE 全国 RISC-V 高水平创新及应用大赛赛题说明](https://developer.aliyun.com/article/1749897) —— 赛题一「A210 边缘视觉 Agent 应用」，明确要求基于 A210（12 TOPS NPU）与官方 Debian 镜像，做图像采集 + 端侧 YOLOv5/v8 + 云端大模型对话。**想找 A210 练手项目，照这个题目做就行**
- 微博长文 [玄铁·践行：在产线、机器人和边缘算力上「跑起来」](https://weibo.com/ttarticle/x/m/geoshow/id/2309405355143666729355) —— 少见的实测数字：MobileNetV2 847 FPS、YOLOv8n 336 FPS、Qwen3-4B 本地推理 19 token/s；另有 AI NAS、16 路 1080P 边缘网关、12 TOPS 算力棒、4 颗 A210 互联的 48 TOPS PCIe 卡等方案
- [知合计算与您相约 AICC2025](https://mp.weixin.qq.com/s/e11WDCFZoI5CtObrTIFO5g) —— 公众号上唯一提及 A210 的文章，纯活动预告，零技术内容

**英文报道**

- CNX Software [Zhihe A210 octa-core RISC-V SoC with 12 TOPS NPU powers SoM-based development board](https://www.cnx-software.com/2026/06/17/zhihe-a210-octa-core-risc-v-soc-with-12-tops-npu-powers-som-based-development-board/) —— 最完整的一篇英文报道
- CNX Software [Three high-performance RISC-V processors to watch in H2 2025](https://www.cnx-software.com/2025/07/22/three-high-performance-risc-v-processors-to-watch-in-h2-2025-ultrarisc-ur-dp1000-zizhe-a210-and-spacemit-k3/) —— A210 首次进入国际视野
- OMG! Ubuntu [New RVA23 RISC-V chips are coming sooner than you think](https://www.omgubuntu.co.uk/2025/07/ubuntu-risc-v-rva23-hardware-coming-soon) —— 注意其 RVA23 说法与 CNX 的更正冲突（见第 1 节）

> 收不到的：CSDN、知乎、`bbs.21ic.com`、`eefocus.com` 在本机网络下返回 521 / 403 / 验证码页，正文不可核验，因此一条都没收。`x-techcon.com` 那篇 AGIROS 文已 404（同内容在 ruyisdk 那篇里）。openEuler 的 A210 镜像路径 `images.oerv.ac.cn/.../zhihe/a210-dev/` 实测 404，要用请走 openEuler RISC-V SIG 官方渠道确认。

---

## 10. 哪里买

- **苦芽科技淘宝企业店**：https://item.taobao.com/item.htm?id=1034868327078&skuId=6052940225420 —— 页面需登录淘宝才能看到商品详情，链接本身返回 200
- AliExpress 上的第三方（chipboard store）标「Sipeed ZHIHE A210」，8GB/64GB 配置约 $334（页面会跳到登录墙，价格只能作参考）
- 知合计算自身没有公开直销页与报价页

---

## 11. 上手前必看

1. **确认板型与版本**：SODIMM V1 / V2 / V3 还是算力棒；底板不同，烧录按键时序、供电、接口都不一样，**烧录指南是按板型分册的**。
2. **镜像只有两套**（Buildroot / Debian 桌面），都以 `a210-evb` 命名；官方没有 Ubuntu。想回滚就用 2.8.1 那一对。
3. **V2 底板是 12V DC 供电**，核心板本身 5V/5A；调试串口是 **UART4**，115200。
4. **不要热插拔底板**，操作前做防静电；启动模式靠 BOOT_SEL 上下拉电阻，PCIe 有 RC/EP 切换。
5. 支持矩阵里的 `wip` 不等于能用；碰到设备树或驱动问题，反馈时附板型、镜像与内核版本、完整串口日志。

---

## 12. 这个索引怎么维护

- 每天 13:00 自动跑一次全网增量扫描（官方制品库新版本、文档站新页、新视频、新仓库），有变化就更新
- 只收**能打开**的链接；每次更新跑一遍全量链接检查，死链下线或换新地址
- 视频要求确实拍了 A210；项目要求仓库里真的有 A210 的设备树、分支或 BSP（不是只提一句）
- 收录不代表背书。官方镜像之外的第三方构建、许可证与维护状态请自行判断
- 缺漏欢迎提 issue / PR，请注明原始来源、适用板型与访问日期

[返回语言索引](README.md)
