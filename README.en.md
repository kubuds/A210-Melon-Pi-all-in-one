# Zhihe A210 resource index (SODIMM V2 / V3 · compute stick)

[简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [English](README.en.md) · [Русский](README.ru.md) · [日本語](README.ja.md) · [Deutsch](README.de.md) · [Español](README.es.md)

Everything publicly findable about the Zhihe Computing A210 (also marketed as "Archimedes A210"): official documentation and datasheet, **directly downloadable official images**, per-board flashing guides, hardware design files, upstream kernel and firmware work, GitHub and Gitee projects, and the Bilibili / YouTube videos that actually show the board.

This page mirrors no firmware and no document — it only points at the origin. **It records links and facts, not promises**; check your board revision, image notes and checksums before flashing.

> **Get the names straight first — this board has more aliases than most.**
>
> - **Chip**: Zhihe Computing A210, product family "Archimedes" (Archimedes A210), a heterogeneous AI SoC sharing compute and inference on one die set.
> - **Board shapes**: a SODIMM compute module plus carrier board (**V1 / V2 / V3** carriers), and a separate **A210 compute stick (Dongle)**.
> - **Who says "Melon Pi / MelonPi"**: Zhihe's own documentation and datasheet **never** use that name (officially it is "A210 SODIMM V1/V2/V3"). It appears in the upstream Linux device-tree filenames (`a210-melonpi-v1.dts` / `-v2.dts`), in the XuanTie open-hardware page title ("XuanTie MelonPi A210"), and in some press coverage. If you see "Melon Pi", it is the kernel/community name for the same board.
> - **Don't confuse it with the A200**: Zhihe also has an A200 platform, and the official Ubuntu images are for A200 only. For A210 the official images are Buildroot and Debian desktop, nothing else.

---

## 1. Key specifications

| Item | Specification |
| --- | --- |
| SoC | Zhihe Computing A210 (heterogeneous AI SoC) |
| CPU | 4× XuanTie C920 + 4× XuanTie C908, RV64GCV (with vector) |
| Clock | The official datasheet says 1.9 GHz; CNX Software reports C920 up to 2.3 GHz and C908 at 1.9 GHz (the two sources disagree — trust your batch and the datasheet) |
| GPU | Vulkan 1.1/1.2/1.3, OpenCL 1.1/1.2/2.0, OpenGL ES 1.1/2.0/3.0/3.1/3.2 (the datasheet does not name the model; "IMG BXM-4-64" comes from the RuyiSDK support-matrix metadata) |
| NPU | 12 TOPS @ INT8, supports INT4/INT8/INT16/FP8/FP16/BF16 |
| Memory | 4 / 8 / 16 GB 64-bit LPDDR4x, up to 4266 Mbps |
| Storage | eMMC 5.1/5.0, NOR/NAND flash, SD 3.0 |
| Networking | 2× 10/100/1000 Mbps Gigabit Ethernet |
| Display | 1× HDMI 2.0, 1× 4-lane MIPI DSI, DP / eDP (limited by USB multiplexing) |
| Camera | 1× 4-lane + 1× 2-lane, or 3× 2-lane MIPI CSI |
| Expansion | PCIe x4 / x2 + x1, x2 + 2× SATA, 2× x1 + 2× SATA; 2× SPI, 1× QSPI, 7× I²C, 10× UART, 3× 5ch PWM, 2× 1ch ADC |
| USB | 1× USB 3.1 (DP Alt), 2× USB 2.0 |
| Audio | 3× 2ch I2S/PCM, 1× TDM/PCM |
| Power / temperature | Module 5V/5A (minimum); carrier 12V DC input; −20 °C to 60 °C |
| Module size | 59.66 mm × 69.94 mm, 260-pin SODIMM |
| Official OS | Linux (Debian desktop / Buildroot) |

**Two conflicting claims about RVA23**: in July 2025 OMG! Ubuntu reported that A210 supports all mandatory and optional RVA23 extensions; CNX Software later corrected this, saying A210 is RVA22 and RVA23 belongs to the next-generation A600. **There is no authoritative conclusion — do not use this for procurement decisions.**

Sources: the official "A210 product datasheet" and "compute module user guide", plus the [Huaqiu open-hardware product page](https://p.eda.cn/d-1389550606774960128) (a repost of the same tables).

---

## 2. Official documentation (Zhihe Computing developer documentation centre)

The documentation site is **developer.zhcomputing.com**, currently **2.9.0**, with a **2.8.1** archive and an `/en/` English edition. It is client-rendered, so `curl` returns no body — open it in a browser.

**Entry points**

- [Documentation home](https://developer.zhcomputing.com/zh/docs/intro) · [English](https://developer.zhcomputing.com/en/docs/intro/)
- [A210 documentation section](https://developer.zhcomputing.com/zh/docs/A210/) · [English](https://developer.zhcomputing.com/en/docs/A210/)
- [2.8.1 archive](https://developer.zhcomputing.com/zh/docs/2.8.1/category/sdk)

**Datasheet and flashing (one guide per board — the wrong one will not flash)**

- [A210 product datasheet (full HTML)](https://developer.zhcomputing.com/zh/docs/A210/A210_Datasheet) — features, package, pin definitions, timing
- [Image burning guides (index)](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/)
- [SODIMM V2 burning guide](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V2_Burning_Instruction) — 12V DC, TTL debug at 115200, USB-A flashing port; hold the flash key and press reset to enter USB mode; Windows needs platform-tools r34.0.5 + usb_driver r13, Linux uses android-sdk-platform-tools
- [SODIMM V3 burning guide](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V3_Burning_Instruction)
- [Compute stick (Dongle) burning guide](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_Dongle_Burning_Instruction) — an easily missed form factor

**Hardware platform**

- [Compute module user guide](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/核心板说明) — key specs, dimensions, 260-pin pin definition
- [SODIMM V2 carrier user guide](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V2_baseboard_developer_guide) — connectors, BOOT_SEL, PCIe RC/EP switch, UART4 as debug port
- [SODIMM V2 carrier schematic](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V2) (V1/V3 and the compute stick have their own pages)
- [Hardware design guide](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/) — required reading before designing a carrier
- [PINMUX](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/A210-PINMUX) · **direct download**: [A210-PINMUX_20260119.xlsx](https://developer.zhcomputing.com/zh/docs/pdf/A210/Hardware-Platform/A210-PINMUX_20260119.xlsx) (~39 KB, verified downloadable)

**SDK**

- [SDK overview](https://developer.zhcomputing.com/zh/docs/category/sdk) · [Quick start (includes the image table)](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/Basic_quick_start_guide)
- [Buildroot developer guide](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/Buildroot_developer_guide) — from the zdocker environment to `./build.sh -b buildroot a210`
- [TORQ SDK introduction](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ%20SDK%E4%BB%8B%E7%BB%8D) — entry point for the 12 TOPS NPU, with TORQ-Toolkit and TORQ-LLM APIs
- Other categories: [quick start](https://developer.zhcomputing.com/zh/docs/category/快速上手) · [build environment](https://developer.zhcomputing.com/zh/docs/category/开发环境构建) · [multimedia](https://developer.zhcomputing.com/zh/docs/category/多媒体) · [AI](https://developer.zhcomputing.com/zh/docs/category/ai)

**Vendor and IP side**

- [XuanTie product page for A210](https://www.xrvm.cn/product/board/4565261785988403200) (client-rendered; no readable body)
- [XuanTie home](https://www.xrvm.cn/) · [XuanTie C920](https://www.xrvm.cn/product/xuantie/C920) · [C908](https://www.xrvm.cn/product/xuantie/C908)
- Zhihe's main site [www.zhcomputing.com](http://www.zhcomputing.com/) — re-checked on 2026-11-08: **HTTP only** (`https://` returns 504 every time and the certificate chain is incomplete; direct and via proxy alike). The Archimedes section lists only A200 / A300, the news centre stops at 2025-07 and there is no A210 page; the English site `en.zhcomputing.com` redirects to a "site coming soon" placeholder — the documentation centre above remains the authoritative source for A210. Business contact: business@zhcomputing.com

> The "GitHub" link in the docs site footer is a placeholder (`github.com/your-org`) — not a real project, do not cite it.

---

## 3. Official images (direct downloads)

There are only two: **Buildroot** (light) and **Debian desktop**, both named `a210-evb`, both delivered as fastboot partition bundles. **There is no official Ubuntu image** — Ubuntu is A200 only.

| Image | Version | Size | Download |
| --- | --- | --- | --- |
| Buildroot prebuilt | v2.9.0 (current) | 179.4 MB | [br2image-v2.9.0-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/br2image-v2.9.0-a210_evb.tar.gz) |
| Debian desktop | v2.9.0 (current) | 738.4 MB | [diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz) |
| Buildroot prebuilt | v2.8.1 (rollback) | 175.9 MB | [br2image-v2.8.1-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/br2image-v2.8.1-a210_evb.tar.gz) |
| Debian desktop | v2.8.1 (rollback) | 734.8 MB | [diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz) |

- Extract to get `emmc-*.img`, `bootzero-rvbl.bin` and `fastboot_images.sh` / `.bat`, then run the script once the board is in flashing mode
- **Official artefact index** (more complete than the docs table): [downloads/release/](http://developer.zhcomputing.com/downloads/release/) — `zhihesdk` holds v2.7.0 / v2.8.0 / v2.8.1 / v2.9.0 plus two development snapshot directories, `develop/` and `develop-test/` (the newest a210 image there is dated 2026-02-05, older than v2.9.0 — do not mistake it for a newer build), `npu` holds v1.3–v2.1 (ovx-compiler, torq-llm, uca-nn, viplite), and `tools` has a 1.17 GB `ubuntu-24.04-x86_64.v1.7.0.tar.gz` build container
- To reproduce the install through RuyiSDK: [ruyisdk/packages-index PR #208](https://github.com/ruyisdk/packages-index/pull/208) turns the fastboot flow, the 2.8.1 Buildroot and Debian bundles and the partition table into ruyi entries, with partition maps and checksums you can cross-check against the official images

---

## 4. Hardware design files (open-source carrier PDFs and schematics)

[Open-source carrier for the XuanTie MelonPi A210 — SODIMM V3](https://p.eda.cn/d-1389550606774960128) (Huaqiu open-hardware community, published by XuanTie, **OpenAtom OHL 1.0**) provides:

- **A210 SODIMM carrier schematics.zip** (2.69 MB)
- **A210 minimal-system schematic design recommendations.pdf** (7.80 MB)
- **A210 minimal-system PCB design recommendations.pdf** (15.55 MB)
- **A210 product datasheet.pdf** (399 KB) — the only way to get a **PDF** datasheet; the official site publishes HTML only
- **A210-PINMUX_20260119.xlsx** (38.89 KB)

Note this is the **V3** carrier, one generation away from the official V2 documentation. Downloading requires an account on that site.

---

## 5. Upstream kernel, firmware and distributions

**Upstream Linux**

- [[PATCH 00/18] riscv: add initial support for Zhihe A210 and Melon Pi](https://lists.infradead.org/pipermail/linux-riscv/2026-October/101909.html) — the first mainline support (UART/clock/reset/pinctrl + DT), validated booting all eight cores on Melon Pi V2; the device-tree files `a210-melonpi-v1.dts` / `-v2.dts` are where the "Melon Pi" name actually comes from
- [[PATCH RFC 00/18] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-October/102222.html) — the 2026-10-27 rework (v2 by the author's numbering): the A210 also carries an E902 management core, and the clock and reset registers are actually owned by the Zephyr SCMI firmware running on it, so this version drops the native clk/reset drivers for the standard SCMI clock/reset protocols and adds an AP-to-E902 doorbell mailbox driver; it boots to a UART shell on Melon Pi V2 with all eight cores. **Neither series is in mainline as of 2026-11-02**; the latest is v3, see the next item
- [[PATCH RFC v3 00/17] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-November/102729.html) — v3, posted 2026-11-02: rebased onto v7.4-rc1; `arm_scmi` drops its ARM architecture dependency so it builds on RISC-V too, the SCMI clock/reset IDs move from dt-bindings into a header next to the DTS, and the mailbox binding switches to fixed local / remote regions; with the riscv defconfig a Melon Pi V2 boots all eight cores to a serial shell. It stays an RFC until Zhihe's firmware supports SCMI natively

**Kernels and device trees (still in vendor and community trees)**

- [RVCK Linux](https://github.com/RVCK-Project/rvck) — `rvck-6.6` has the most complete device trees: [a210.dtsi](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi) · [a210-melon-pi.dts](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts) · [Zhihe DT binding](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml); commit search returns 41 A210-related commits covering GPIO/UART/timer/DMA/sdhci
- [RVCK: A210 peripheral-support issue](https://github.com/RVCK-Project/rvck/issues/381) · [merged peripheral-support PR](https://github.com/RVCK-Project/rvck/pull/382)
- [RVCK: A210 USB support PR #437](https://github.com/RVCK-Project/rvck/pull/437) — opened 2026-10-22 and **still open**, but the author turned it into a **draft** on 2026-11-11: the series had been rebased onto the updated `rvck-6.6` (20 patches, adding the second GMAC on Melon Pi, a UART pinctrl fix, GPIO ranges, Zicbop block size and device-tree cleanups), and that day Icenowy raised three device-tree points on `a210.dtsi` (nodes with overlapping regs should go back to syscon or get an aux device registered from clk_usb; the two independent PHYs should each get their own node; a `syscon` property needs a vendor prefix), while the 11-13 CI run passes end to end (check-patch, kunit, kernel-build and a LAVA QEMU boot with result collection). The payload: two DWC2 controllers and three USB 2.0 PHY instances, the DWC3 glue and the USB 3.1/DP combo PHY, plus board-level FUSB302 Type-C support for Melon Pi; [PCIe and SATA support issue #477](https://github.com/RVCK-Project/rvck/issues/477) is open as well
- [RevyOS Linux](https://github.com/revyos/linux) — [A210 maintainer entry](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d) · [thermal and watchdog DT](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4) · [PWM driver](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d) · [Melon Pi V2 audio routing](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146). These commits are all on the `rv/a210-upstream-local` branch, not on the default branch
- [RISE Project: riseproject-dev/linux](https://github.com/riseproject-dev/linux) — has an `alibaba-a210` branch

**Boot and firmware**

- [riseproject-dev/u-boot](https://github.com/riseproject-dev/u-boot) — `v2024.10-a210` branch containing `a210.dts`, `a210-soc.dtsi` and `board/zhihe/a200-evb`
- [riseproject-dev/opensbi](https://github.com/riseproject-dev/opensbi) — `v1.5-a210` branch with `platform/generic/zhihe/a210.c`
- [openeuler-riscv/opensbi-zhihe-a210](https://github.com/openeuler-riscv/opensbi-zhihe-a210) — vendor OpenSBI port
- [revyos/ruyiedk2](https://github.com/revyos/ruyiedk2) — EDK2/UEFI platform firmware; the README covers Melon Pi V1 and V2, and `docs/melonpi.md` documents native RAM boot and USB fastboot
- SCMI boot chain (`a210/scmi-v3` branches, 2026-11-02): [coreboot](https://github.com/revyos/coreboot/tree/a210/scmi-v3) · [OpenSBI](https://github.com/revyos/opensbi/tree/a210/scmi-v3) · [EDK2](https://github.com/revyos/edk2/tree/a210/scmi-v3) · [RevySR/linux, the full tree with the remaining peripherals](https://github.com/RevySR/linux/tree/a210/scmi-v3) — matches the v3 RFC; the earlier `a210/scmi` branches are still there, and `revyos/ruyiedk2` has `a210/scmi-v3` as well
- [RevySR/zephyr `xuantie/scmi-v3`](https://github.com/RevySR/zephyr/tree/xuantie/scmi-v3) — the SCMI server firmware (Zephyr) running on the E902; it owns power, the PMIC and CPU DVFS timing; a second branch, `xuantie/vcodec-v3` (2026-11-02), prepares the VP clocks, resets and power domains for the VC9000D and exports the video codec resources to the AP through the SCMI server
- [RevySR/linux `a210/vcodec-v3`](https://github.com/RevySR/linux/tree/a210/vcodec-v3) — new 2026-11-02 development branch for video decoding: it adds the A210's VC9000D decoder (including VP9) to the hantro driver plus the matching device-tree nodes
- RevySR/linux carries more A210 branches than the SCMI one: [a210/bringup-v7.3](https://github.com/RevySR/linux/tree/a210/bringup-v7.3) (bring-up, 2026-10-22), [a210/scmi-bootchain-v7.3](https://github.com/RevySR/linux/tree/a210/scmi-bootchain-v7.3) (SCMI boot chain, 10-27) and [b4/a210-init](https://github.com/RevySR/linux/tree/b4/a210-init) (the first patch series, 10-21) — pick the one matching what you want to test

**Distribution layer**

- [riscv/meta-riscv](https://github.com/riscv/meta-riscv) — the OpenEmbedded/Yocto RISC-V layer lists a `zhihe-a210` machine ("Zhihe Computing Archimedes A210"), and `conf/machine/zhihe-a210.conf` exists; [PR #744](https://github.com/riscv/meta-riscv/pull/744), merged on 2026-11-07, switched the BSP kernel source to the `v7.2.12-a210` tag of `riseproject-dev/linux` (`a210_evb_defconfig`) and added `test-zhihe-a210.yml`: cloud build plus a TFTP netboot run on the OSU-OSL board farm; [PR #748](https://github.com/riscv/meta-riscv/pull/748), merged on 2026-11-10, widens that workflow's path filters and switches to `readlink -f`
- [RevySR/rvck-image](https://github.com/RevySR/rvck-image) — rootfs/disk image build; the README documents the "flash through Melon Pi EDK2" flow (F9 into Fastboot, `flash emmc0`)
- [riseproject-dev/android_manifest](https://github.com/riseproject-dev/android_manifest) — RISE Android 17 BSP covering the Alibaba A210 EVB, with lunch target `aosp_a210_evb-trunk_staging-userdebug`
- [riseproject-dev/android_kernel_device](https://github.com/riseproject-dev/android_kernel_device) — the Kleaf device fragments behind that BSP (`alibaba/a210/`, `zhihe_a210.fragment`)
- [riseproject-dev/android_bootloader_build](https://github.com/riseproject-dev/android_bootloader_build) — RISE's boot-chain build repository; the `alibaba-android-17` branch produces the U-Boot + OpenSBI pair for a210 (AVB verification disabled, Android GPT layout for the 64 GB eMMC)
- [riseproject-dev/android_vendor_rise](https://github.com/riseproject-dev/android_vendor_rise) — RISE's repository of prebuilt boot chains and firmware (`alibaba/a210/bootloader/`): `u-boot.bin`, `spl-with-fit-rvbl.bin`, `bootzero-rvbl.bin`, `riscv-boot.itb`, `emmc-gpt_primary.img`, `a210.dtb` and the RTL8822CS Bluetooth firmware; CI rebuilds them every three hours from the upstream bootloader repositories, so you do not have to build a U-Boot + OpenSBI pair for the A210 EVB yourself
- [BayLibre/android_device_alibaba_a210](https://github.com/BayLibre/android_device_alibaba_a210) — an AOSP device tree maintained by BayLibre (`android-17` branch, `PRODUCT_SHIPPING_API_LEVEL` 37): the lunch target is the same `aosp_a210_evb-trunk_staging-userdebug`, but `TARGET_ARCH_VARIANT := a210`, because neither the C920 nor the C908 implements Zvbb and the riscv64 baseline will not build; U-Boot/OpenSBI and the kernel are staged as prebuilts, and the debug console is `ttyS4` at 115200. It already carries RTL8822CS WiFi/Bluetooth, HDMI audio, the PowerVR Vulkan declarations and a riscv64 WebView. This is a separate Android 17 tree from the RISE one above
- [BayLibre/android_device_alibaba_a210_kernel](https://github.com/BayLibre/android_device_alibaba_a210_kernel) — the prebuilt kernel repository for that device tree: `mainline/` holds `Image`, `a210-evb.dtb`, `System.map`, `vmlinux.symvers` and the dlkm directories, plus development branches `glaroque/a210-fixes` and `jmasson/a210-fixes-wifi-bt`
- [RuyiSDK support matrix: A210 SODIMM V2](https://matrix.ruyisdk.org/boards/A210_SODIMM_V2/) ([source directory](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2) · [others.yml](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml)) — Debian and Buildroot are both marked `wip`; `wip` means in progress, not working
- [ruyisdk/ruyi](https://github.com/ruyisdk/ruyi) — the package manager has a Zhihe vendor naming convention but **no A210 device entry yet**, so having ruyi installed does not give you A210 images

---

## 6. GitHub at a glance

The A210 GitHub ecosystem is thin and falls into four lines: **RVCK** (most complete device trees), **RevyOS** (kernel commits + EDK2 firmware), **RISE Project** (U-Boot / OpenSBI / Android BSP) and **meta-riscv** (Yocto machine). There is **no official Zhihe GitHub organisation** (`orgs/zhcomputing` returns 404); all official material lives on the documentation site.

Everything already listed in section 5 is not repeated here; the remainder:

- [kubuds/A210-Melon-Pi-all-in-one](https://github.com/kubuds/A210-Melon-Pi-all-in-one) — this index
- [ruyisdk/packages-index PR #208](https://github.com/ruyisdk/packages-index/pull/208) — the ruyi-side A210 device and flashing strategy
- [riseproject-dev/developer-cloud](https://github.com/riseproject-dev/developer-cloud) (formerly `board-farm`, renamed 2026-11-11) — the RISE RISC-V Developer Cloud management repo: the first 20 Zhihe A210 boards (donated by Alibaba) sit at Oregon State University's OSU-OSL, with a Labgrid `a210-yocto` pool in Phase 1, plus Scaleway (France) and SOPIC (China) sites; the repo holds `boards/zhihe-a210/` client/exporter configs and pytest cases, and four A210 pipelines under `.github/workflows/` (`a210_netboot.yml` TFTP in-memory boot for a210-board-01 to 05, `a210_labgrid_uboot.yml`, `yocto-zhihe-a210.yml`, and `a210_telemetry.yml`, added 2026-11-11 for non-destructive hardware telemetry); the hub side also gained board tag publishing with tag/search filtering and Android board detection via ADB or UART, and fixed a zhihe-a210 UART echo issue that broke kernel version probing

---

## 7. Gitee projects

Very few Gitee repositories target the A210 directly, and **Gitee's search API currently returns empty for every keyword**, so this section is **not exhaustive**:

- [agiros/yolov5_torq_camera](https://gitee.com/agiros/yolov5_torq_camera) — its description reads "mainly for the A210 board, calls a YOLOv5 model through torq and publishes the detections and frames as AGIROS topics". The README is still the default template
- [agiros/ur5-demo](https://gitee.com/agiros/ur5-demo) — the repository cloned by the AGIROS A210 robot-arm tutorial, used to do UR5 visual grasping on A210 + openEuler 24.03; the repository itself doesn't mention A210, it is "used by an A210 project"

> Trap: searching "a210" mostly returns Canaan **K210** projects; `gitee.com/zhihe` is an unrelated personal account.

---

## 8. Videos

**Bilibili (only four on the whole site, and just one is named Melon Pi)**

- [Zhihe XuanTie A210 Melon Pi dev board hands-on](https://www.bilibili.com/video/BV1wdx969Exj/) · donatello1996 · 2026-11-04 · ~34 views — a 21-second clip of two LED matrix panels showing temperature, humidity, pressure and gesture status plus a face animation; **the board itself never appears in frame**, so the only evidence that this is the A210 is the title and the tags (RISC-V, XuanTie, dev board). The first Bilibili video with Melon Pi in its title
- [Robotics solutions built on A210 x AGIROS](https://www.bilibili.com/video/BV12KFKzkELG/) · AGIROS open-source community · 2026-02-02 · ~62 views — part 5 of the AGIROS Meetup in Beijing; the speaker, Shen Zhuang, is a senior AI engineer at Zhihe Computing Technology (Hangzhou); **the only video so far where a serving Zhihe engineer talks about the A210** (14 min 10 s), about the solution rather than benchmark numbers
- [Zhihe Archimedes A210 RISC-V board unboxing — XuanTie C920 core + NPU](https://www.bilibili.com/video/BV1fJrnBsENd/) · DSOE1024 · 2026-01-14 · ~1.7k views — **the only unboxing footage of this board** (2 min 48 s)
- [Zhihe A210 arrives; the A600 "industry–academia" loop](https://www.bilibili.com/video/BV19R84zsEVH/) · 石榴派-袁德俊 · 2025-07-26 · 428 views — summit commentary, not a hands-on

**YouTube (only one, and it is a spec sheet plus a shopping link)**

- [Struggling with local AI projects? This RISC-V dev kit might help](https://www.youtube.com/watch?v=yK5x93THqLE) · 스마트직구연구소 — description names the Sipeed ZHIHE A210 RISC-V AI Dev Kit; the content lists specs rather than testing them

**No tutorials, no development logs, no launch recording.** Zhihe Computing has no official account on either platform. That is the honest state of this board today.

---

## 9. Tutorials, hands-on posts and coverage

- [AGIROS + RISC-V on Zhihe A210: full stack working and verified on hardware](https://ruyisdk.cn/t/topic/2362) — **the most complete Chinese hands-on post**: flashing openEuler 24.03 LTS (root password `openEuler12#$`), networking and static IP, installing AGIROS 25.12, ur5-moveit-demo, eye-to-hand calibration, and real UR5 grasping
- [Zhihe A210 board unboxing (video repost)](https://ruyisdk.cn/t/topic/2412) — a short post showing the board and its connectors
- [XuanTie MelonPi A210 SODIMM V3 open-source carrier](https://p.eda.cn/d-1389550606774960128) — the most useful hardware page (22 connector descriptions, BOOT_SEL, PCIe RC/EP, UART4)
- Alibaba Cloud developer community: [2nd CIE national RISC-V innovation contest problem statement](https://developer.aliyun.com/article/1749897) — problem 1 is an "A210 edge vision agent", explicitly requiring an A210 (12 TOPS NPU) with the official Debian image, image capture plus on-device YOLOv5/v8 plus a cloud LLM dialogue. **If you want a practice project for the A210, build this**
- Weibo long read: [XuanTie in production lines, robots and edge compute](https://weibo.com/ttarticle/x/m/geoshow/id/2309405355143666729355) — rare measured numbers: MobileNetV2 847 FPS, YOLOv8n 336 FPS, Qwen3-4B local inference at 19 token/s; also AI NAS, a 16-channel 1080p edge gateway, a 12 TOPS compute stick and a 48 TOPS PCIe card built from four A210s
- [Zhihe Computing at AICC2025](https://mp.weixin.qq.com/s/e11WDCFZoI5CtObrTIFO5g) — the only WeChat article mentioning A210; a pure event announcement, no technical content

**English coverage**

- CNX Software: [Zhihe A210 octa-core RISC-V SoC with 12 TOPS NPU powers SoM-based development board](https://www.cnx-software.com/2026/06/17/zhihe-a210-octa-core-risc-v-soc-with-12-tops-npu-powers-som-based-development-board/) — the most complete English write-up
- CNX Software: [Three high-performance RISC-V processors to watch in H2 2025](https://www.cnx-software.com/2025/07/22/three-high-performance-risc-v-processors-to-watch-in-h2-2025-ultrarisc-ur-dp1000-zizhe-a210-and-spacemit-k3/) — where A210 first reached an international audience
- OMG! Ubuntu: [New RVA23 RISC-V chips are coming sooner than you think](https://www.omgubuntu.co.uk/2025/07/ubuntu-risc-v-rva23-hardware-coming-soon) — note its RVA23 claim conflicts with CNX's correction (see section 1)

> Not included: CSDN, Zhihu, `bbs.21ic.com` and `eefocus.com` return 521 / 403 / CAPTCHA pages from this machine, so their bodies cannot be verified and no link from them is listed. The `x-techcon.com` AGIROS article is now 404 (the same content is in the ruyisdk post). The openEuler A210 image path `images.oerv.ac.cn/.../zhihe/a210-dev/` returns 404 — go through the openEuler RISC-V SIG channel instead.

---

## 10. Where to buy

- **Kubuds Taobao enterprise store** (苦芽科技): https://item.taobao.com/item.htm?id=1034868327078&skuId=6052940225420 — the page needs a Taobao login before it shows the listing; the link itself returns 200
- A third-party AliExpress listing (chipboard store) sells it as "Sipeed ZHIHE A210", 8GB/64GB around $334 — the page bounces to a login wall, so treat the price as indicative
- Zhihe Computing itself publishes no direct sales or quotation page

---

## 11. Before you start

1. **Confirm the board revision**: SODIMM V1 / V2 / V3, or the compute stick. Flashing key sequence, power and connectors all differ — **the burning guides are split per board**.
2. **There are only two images** (Buildroot / Debian desktop), both named `a210-evb`; there is no official Ubuntu. Keep the 2.8.1 pair for rollback.
3. **The V2 carrier takes 12V DC**; the module itself is 5V/5A. The debug UART is **UART4** at 115200.
4. **Do not hot-plug the carrier**, and take ESD precautions; boot mode is set by BOOT_SEL pull resistors, and PCIe has an RC/EP switch.
5. `wip` in the support matrix does not mean usable. When reporting device-tree or driver problems, include board revision, image and kernel version, and a full serial log.

---

## 12. How this index is maintained

- A full incremental sweep runs daily at 13:00 (new artefact versions, new documentation pages, new videos, new repositories) and updates this file when something changes
- Only links that actually open are listed; every update runs a full link check and dead links are dropped or replaced
- Videos must actually film an A210; projects must actually carry A210 device trees, branches or BSPs, not just mention the chip
- Listing is not endorsement — judge third-party builds, licences and maintenance status yourself
- Missing something? Open an issue or PR with the original source, applicable board revision and date checked

[Back to the language index](README.md)
