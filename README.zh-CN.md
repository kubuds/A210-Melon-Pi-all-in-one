# 知合 A210 / Melon Pi 资源汇总

[简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [English](README.en.md) · [Русский](README.ru.md) · [日本語](README.ja.md) · [Deutsch](README.de.md) · [Español](README.es.md)

本文汇集目前可核验的 A210 开发板公开资料。各页面可能随上游更新；链接所指原文是规格、镜像和支持状态的最终依据。此列表持续补充，不代表已经穷尽网络资源。

## 板卡概览

[RuyiSDK 开发板支持矩阵](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2)收录了 **A210 SODIMM V2**，并给出以下信息：

| 项目 | 支持矩阵所列信息 |
| --- | --- |
| 厂商 | ZHIHE COMPUTING（知合） |
| SoC | A210 |
| CPU 核心 | XuanTie C920 + XuanTie C908 |
| GPU | IMG BXM-4-64 |
| 内存配置 | 4 GB / 8 GB / 16 GB |

以上是该支持矩阵页面的信息，不应据此推断其他硬件版本的配置。请以手中板卡的丝印、产品资料和当前版本文档为准。

## 板卡专属资源

### 硬件资料与系统支持

- [RuyiSDK A210 SODIMM V2 支持矩阵页面](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2)：板卡条目及项目状态。
- [硬件与处理器信息（README）](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/README.md)：处理器、核心、GPU、内存和厂商信息。
- [系统支持状态（others.yml）](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml)：目前记录 Debian 和 Buildroot 状态为 `wip`；状态可能变化，请查看最新文件。
- [RuyiSDK 第 075 期双周报告](https://github.com/ruyisdk/wechat-articles/blob/main/20260901-ruyisdk-biweekly-75.md)：记录了 RuyiSDK 软件源新增对知合 A210 SODIMM 官方 EVB 系统镜像的兼容支持。该报告不是镜像下载页；使用前请核对原始镜像说明、板卡版本和校验值。

### Linux 内核与驱动进展

以下是 RevyOS Linux 仓库中明确提及 A210 / Melon Pi 的变更，可用于追踪设备树、驱动和板级支持。它们是具体开发提交，并不等同于任意发行版均已支持。

- [A210 平台维护条目及支持文件范围](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d)：列出 A210 设备树、绑定和驱动目录。
- [A210 温控与看门狗设备树](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4)。
- [PWM 驱动支持 A210](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d)：提交说明指出复用 TH1520 驱动。
- [Melon Pi V2 音频走线](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146)。
- [RevyOS Linux 源码仓库](https://github.com/revyos/linux)：查看当前分支、设备树、驱动、提交和后续更新。
- [在 RevyOS Linux 中搜索 A210 代码](https://github.com/revyos/linux/search?q=A210&type=code)：按当前仓库内容检索。
- [RVCK Linux 的 Melon Pi 设备树](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts)：板级 Linux 配置，不是完整硬件手册。
- [RVCK Linux 的 A210 SoC 设备树](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi)及[知合设备树绑定](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml)：SoC 和兼容字符串的实现参考。
- [RVCK A210 外设支持跟踪](https://github.com/RVCK-Project/rvck/issues/381)与[已合并的外设支持变更](https://github.com/RVCK-Project/rvck/pull/382)：查看 GPIO、定时器、I²C、SPI、DMA 等支持讨论和代码。该仓库是另一条 Linux 开发线，不能据此推断 RevyOS 或其他系统已包含相同支持。

## 上手前建议

1. 确认板卡的准确型号、版本及内存容量；A210 SoC 不代表所有载板或版本相同。
2. 先看支持矩阵和镜像发布说明，确认镜像适用对象、状态、启动介质和校验值。不要把其他 A210 板卡的镜像直接刷入。
3. 阅读对应镜像的原始安装说明，并保留现有数据备份。本文未验证任何具体烧录命令或镜像文件。
4. 遇到设备树、驱动或启动问题时，附上板卡版本、镜像/内核版本、完整日志和来源链接，再向相应项目反馈。

## 资料边界与贡献

公开且可核验的 A210 专属资料目前主要来自支持矩阵和 RevyOS Linux 开发记录。未能确认的官方产品手册、原理图、引脚表、下载地址和社区联系方式不在此猜测补写。欢迎提交遗漏资料；请注明原始来源、适用硬件版本、访问日期，并尽可能保留校验和及许可信息。
