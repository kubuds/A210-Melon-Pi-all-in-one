# Zhihe A210 / Melon Pi Resource Guide

[简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [English](README.en.md) · [Русский](README.ru.md) · [日本語](README.ja.md) · [Deutsch](README.de.md) · [Español](README.es.md)

This guide collects publicly verifiable resources for the A210 development board. Upstream pages are the source of truth for specifications, images, and support status, and may change. This is a growing index, not a claim that every resource on the internet has been found.

## Board overview

The [RuyiSDK board support matrix](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2) lists the **A210 SODIMM V2** with these details:

| Item | Information in the support matrix |
| --- | --- |
| Vendor | ZHIHE COMPUTING |
| SoC | A210 |
| CPU cores | XuanTie C920 + XuanTie C908 |
| GPU | IMG BXM-4-64 |
| Memory configurations | 4 GB / 8 GB / 16 GB |

These details come from that matrix entry and should not be assumed to apply to other hardware revisions. Check the board markings and documentation for the exact board in hand.

## Board-specific resources

### Hardware information and operating-system status

- [RuyiSDK A210 SODIMM V2 support-matrix page](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2): board entry and project status.
- [Hardware and processor details (README)](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/README.md): processor, cores, GPU, memory, and vendor.
- [Operating-system status (others.yml)](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml): Debian and Buildroot are currently marked `wip`; check the file for changes.
- [RuyiSDK biweekly report No. 75](https://github.com/ruyisdk/wechat-articles/blob/main/20260901-ruyisdk-biweekly-75.md): records that the RuyiSDK package repository added compatibility for the official Zhihe A210 SODIMM EVB system image. This is an announcement, not an image download page; check the original image instructions, board revision, and checksum before use.

### Linux kernel and driver work

These RevyOS Linux changes explicitly mention A210 / Melon Pi and help track device-tree, driver, and board support. Individual development commits do not imply support in every distribution.

- [A210 platform maintainership and supported file areas](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d): lists A210 device trees, bindings, and driver directories.
- [A210 thermal and watchdog device tree](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4).
- [PWM driver support for A210](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d): the commit description says it reuses the TH1520 driver.
- [Melon Pi V2 audio routing](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146).
- [RevyOS Linux source repository](https://github.com/revyos/linux): browse the current branch, device trees, drivers, commits, and ongoing work.
- [Search A210 code in RevyOS Linux](https://github.com/revyos/linux/search?q=A210&type=code): search the current repository contents.
- [Melon Pi device tree in RVCK Linux](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts): board-level Linux configuration, not a complete hardware manual.
- [A210 SoC device tree in RVCK Linux](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi) and [Zhihe device-tree binding](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml): implementation references for the SoC and compatible strings.
- [RVCK A210 peripheral-support issue](https://github.com/RVCK-Project/rvck/issues/381) and [merged peripheral-support change](https://github.com/RVCK-Project/rvck/pull/382): discussion and code for GPIO, timers, I²C, SPI, DMA, and other peripherals. RVCK is a separate Linux development line; this does not imply the same support is present in RevyOS or another system.

## Before getting started

1. Identify the exact board model, revision, and memory size; sharing the A210 SoC does not mean every carrier board or revision is identical.
2. Check the support matrix and image announcement for the target board, status, boot media, and checksum. Do not flash an image for a different A210 board without confirmation.
3. Follow the original installation instructions for the specific image and back up existing data. This guide does not verify any flashing command or image file.
4. When reporting device-tree, driver, or boot problems, include the board revision, image/kernel version, complete logs, and source links.

## Scope and contributions

The A210-specific public material that can currently be verified is mainly in the support matrix and RevyOS Linux development history. Unverified product manuals, schematics, pinouts, download URLs, and community contacts are intentionally not guessed. Contributions are welcome: include the original source, applicable hardware revision, date checked, and checksums or licensing information when available.
