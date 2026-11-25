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
- [SODIMM V1 burning guide](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V1_Burning_Instruction) — the earliest of the four board-specific guides, valid only for V1 carrier boards
- [SODIMM V2 burning guide](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V2_Burning_Instruction) — 12V DC, TTL debug at 115200, USB-A flashing port; hold the flash key and press reset to enter USB mode; Windows needs platform-tools r34.0.5 + usb_driver r13, Linux uses android-sdk-platform-tools
- [SODIMM V3 burning guide](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V3_Burning_Instruction)
- [Compute stick (Dongle) burning guide](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_Dongle_Burning_Instruction) — an easily missed form factor

**Hardware platform**

- [Compute module user guide](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/核心板说明) — key specs, dimensions, 260-pin pin definition
- [SODIMM V2 carrier user guide](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V2_baseboard_developer_guide) — connectors, BOOT_SEL, PCIe RC/EP switch, UART4 as debug port
- User guides for the other two carriers: [SODIMM V1](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V1_baseboard_developer_guide) · [SODIMM V3](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V3_baseboard_developer_guide)
- Carrier schematics (one per board type, four in total): [SODIMM V1](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V1) · [SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V2) · [SODIMM V3](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V3) · [compute stick](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Dongle)
- [Hardware design guide](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/) — required reading before designing a carrier; the text comes in two parts: [schematic design suggestions](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/Schematic_Diagram_Design_Suggestions) (minimum system, the 24 MHz and 32.768 kHz clocks, reset and watchdog, BOOT_SEL and STRAP pull resistors, TEST_MODE/DEBUG_MODE handling) · [PCB design recommendations](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/PCB_Design_Recommendations)
- [PINMUX](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/A210-PINMUX) · **direct download**: [A210-PINMUX_20260119.xlsx](https://developer.zhcomputing.com/zh/docs/pdf/A210/Hardware-Platform/A210-PINMUX_20260119.xlsx) (~39 KB, verified downloadable)

**SDK**

- [SDK overview](https://developer.zhcomputing.com/zh/docs/category/sdk) · [Quick start (includes the image table)](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/Basic_quick_start_guide) · [Multimedia quick start](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/Multimedia_quick_start_guide) · [AI quick start](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/AI_quick_start_guide)
- Build environment: [Buildroot developer guide](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/Buildroot_developer_guide) — from the zdocker environment to `./build.sh -b buildroot a210`; [BSP developer guide](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/BSP_developer_guide) · [Partition layout](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/分区介绍)
- Multimedia: [MPI API reference](https://developer.zhcomputing.com/zh/docs/SDK/多媒体/MPI_API_Reference/)
- [TORQ SDK introduction](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ%20SDK%E4%BB%8B%E7%BB%8D) — entry point for the 12 TOPS NPU, with TORQ-Toolkit and TORQ-LLM APIs; reference manuals: [TORQ-Toolkit Python API](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ-Toolkit%20API%E5%8F%82%E8%80%83) · [TORQ C API](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ%20C%20API%E5%8F%82%E8%80%83) · [TORQ-LLM C API](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ-LLM%20C%20API%E5%8F%82%E8%80%83) · [Platform operator support list](https://developer.zhcomputing.com/zh/docs/SDK/AI/Platform_operators_support_list)
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
- **The official artefact host returned 503 site-wide from 2026-11-13 and is back as of the 2026-11-18 recheck**: the directory index and all four image links above answer 200 again, `br2image-v2.9.0-a210_evb.tar.gz` with 188,113,587 bytes (179.4 MB) and `usb_driver_r13-windows.zip` with 8,682,039 bytes, matching the sizes listed; during the outage the same paths served a 4.6 MB JFrog Platform loading page
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
- [[PATCH RFC v3 00/17] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-November/102729.html) — v3, posted 2026-11-02: rebased onto v7.4-rc1; `arm_scmi` drops its ARM architecture dependency so it builds on RISC-V too, the SCMI clock/reset IDs move from dt-bindings into a header next to the DTS, and the mailbox binding switches to fixed local / remote regions; with the riscv defconfig a Melon Pi V2 boots all eight cores to a serial shell. It stays an RFC until Zhihe's firmware supports SCMI natively. Note also that in these bindings the V3 baseboard reuses the V2 compatible (`zhihe,a210-melonpi-v2`), so upstream has no separate v3 board name and running the V2 DTB on V3 hardware is expected behaviour (Conor Dooley acked that binding). On the review side only a non-RFC version is missing: both the pinctrl dt-binding and the driver patch have Linus Walleij's LGTM ([102916](https://lists.infradead.org/pipermail/linux-riscv/2026-November/102916.html)), and Conor Dooley suggests splitting pinctrl — which does not depend on SCMI — into its own series ([103213](https://lists.infradead.org/pipermail/linux-riscv/2026-November/103213.html)).
- [[PATCH v4 00/13] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-November/104545.html) — v4 of 2026-11-20, **RFC dropped and sent as a regular series**: with Zhihe agreeing to use SCMI in firmware the old reservation is gone. It is rebased on v7.4-rc3 and split per review — the `arm_scmi` architecture dependency goes separately, and `vendor-prefixes` plus the pin controller became their own series (the author says both are in linux-next) — so the series shrinks from 18 to **13 patches** and now carries only the mailbox, the UARTs with bindings, the DT, defconfig and MAINTAINERS. A Melon Pi V2 boots to a serial shell with all eight CPUs online on riscv defconfig; the board binding `zhihe,a210-melonpi-v1/v2` still carries `Acked-by: Conor Dooley` (v4 05/13). Not in mainline as of 2026-11-25; all 13 patches still sit at `new` in patchwork, and no review replies yet after the posting

**Kernels and device trees (still in vendor and community trees)**

- [RVCK Linux](https://github.com/RVCK-Project/rvck) — `rvck-6.6` has the most complete device trees: [a210.dtsi](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi) · [a210-melon-pi.dts](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts) · [Zhihe DT binding](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml); commit search returns 56 A210-related commits covering GPIO/UART/timer/DMA/sdhci
- [RVCK: A210 peripheral-support issue](https://github.com/RVCK-Project/rvck/issues/381) · [merged peripheral-support PR](https://github.com/RVCK-Project/rvck/pull/382)
- [RVCK: A210 USB support PR #437](https://github.com/RVCK-Project/rvck/pull/437) — opened 2026-10-22 and **merged on 2026-11-23**; it spent 2026-11-11 onward as a **draft** and went back to **ready on 11-18**: the series had been rebased onto the updated `rvck-6.6` (20 patches, adding the second GMAC on Melon Pi, a UART pinctrl fix, GPIO ranges, Zicbop block size and device-tree cleanups), and that day Icenowy raised three device-tree points on `a210.dtsi` (nodes with overlapping regs should go back to syscon or get an aux device registered from clk_usb; the two independent PHYs should each get their own node; a `syscon` property needs a vendor prefix); the 11-13 CI run passes end to end (check-patch, kunit, kernel-build and a LAVA QEMU boot with result collection), after which the author asked @unicornx and Icenowy for review in public and Icenowy added two more: `clk_usb` should not be split into separate nodes — it should cover the whole register space and expose syscon from the clk driver; the two USB2 PHYs may each become their own node with the pulldown expressed as a DT property such as `zhihe,pulldown-mask`, and the DWC3-side USB2 PHY should be a reg-less node or folded into the glue, with a descriptive property name like `zhihe,usb-syscon` (plain `syscon` is not acceptable). The head commit is now `4990a7ac`. **Where it landed on 2026-11-18**: the author reworked and rebased the series along those lines and moved the PR out of draft; the PR description now records the final arrangement — the two DWC2 PHYs each get their own register block with the pulldown bits expressed as `zhihe,pulldown-mask`, while the DWC3-side USB2 PHY shares its MMIO window with the USB clock controller, so the clk driver registers the regmap with syscon and the PHY picks it up through the `zhihe,usb-syscon` phandle instead of describing a `reg` that overlaps the clock node. It is still 20 patches over 24 files, +2296/−257; Icenowy replied LGTM the same day, all four CI checks (check-patch, kunit, kernel-build, LAVA QEMU) passed, and unicornx built and boot-tested it on QEMU/virt and Pioneerbox — **merged into `rvck-6.6` on 11-23** (merge commit `f8351c85`): `a210.dtsi` now carries the `zhihe,a210-dwc3-usb2-phy` node (registers via `zhihe,usb-syscon`) and the USB3 PHY, while `a210-melon-pi.dts` wires the `usb2_0`/`usb2_1` vbus regulators and the `usb3` Type-C role switch. The payload: two DWC2 controllers and three USB 2.0 PHY instances, the DWC3 glue and the USB 3.1/DP combo PHY, plus board-level FUSB302 Type-C support for Melon Pi; [PCIe and SATA support issue #477](https://github.com/RVCK-Project/rvck/issues/477) is open as well
- [RevyOS Linux](https://github.com/revyos/linux) — the default branch `revyos/7.3.y` has been rewritten end to end once a day for four days running since 11-21, and now sits at **[`9c93e241`](https://github.com/revyos/linux/commit/9c93e241b3) (2026-11-24)**. The 11-24 rebuild carries the upstream patches on the default branch: [`FROMGIT: pinctrl: zhihe: add A210 support`](https://github.com/revyos/linux/commit/0e533424) (tagged FROMGIT, so it is already in the pinctrl subsystem tree), [`FROMLIST: mailbox: add Zhihe A210 AP to E902 mailbox driver`](https://github.com/revyos/linux/commit/d5ce9954), [`FROMLIST: dt-bindings: riscv: add Melon Pi V1 and V2`](https://github.com/revyos/linux/commit/12dde5ea) and [`FROMLIST: riscv: dts: zhihe: add Melon Pi V1 and V2`](https://github.com/revyos/linux/commit/ed2dc077) (with A210 core / UARTs / module memory DTS in the same batch); mainline still takes none of it — `drivers/pinctrl/zhihe` and `arch/riscv/boot/dts/zhihe` do not exist in torvalds/linux. The A210 defconfig commit is now [`REVYOS: config: enable Zhihe A210 support`](https://github.com/revyos/linux/commit/a774c69b95): it turns on `CONFIG_ARCH_ZHIHE`, `CONFIG_PINCTRL_ZHIHE_A210` and `CONFIG_ZHIHE_A210_MBOX`, promotes `ARM_SCMI_PROTOCOL` and `COMMON_CLK_SCMI` from `=m` to `=y`, and adds `ARM_SCMI_PERF_DOMAIN=m`, `ARM_SCMI_POWER_DOMAIN=m` and `RESET_SCMI=m` — A210 takes both clocks and resets over SCMI, so the first two have to be built in. The rewrite pushed the earlier `62df2f69` and `96b82eb6` off the default branch (`62df2f69` has diverged from the current head: 339 ahead / 334 behind); [A210 maintainer entry](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d) · [thermal and watchdog DT](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4) · [PWM driver](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d) · [Melon Pi V2 audio routing](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146) are still only on `rv/a210-upstream-local`
- [RISE Project: riseproject-dev/linux](https://github.com/riseproject-dev/linux) — has an `alibaba-a210` branch

**Boot and firmware**

- [riseproject-dev/u-boot](https://github.com/riseproject-dev/u-boot) — `v2024.10-a210` branch containing `a210.dts`, `a210-soc.dtsi` and `board/zhihe/a200-evb`; there is also a [`fix/a210-sdhci-1v8-phy`](https://github.com/riseproject-dev/u-boot/tree/fix/a210-sdhci-1v8-phy) branch whose 2026-11-17 commit makes `zhihe_sdhci` pick the right PHY for a fixed-1.8V eMMC
- [riseproject-dev/opensbi](https://github.com/riseproject-dev/opensbi) — `v1.5-a210` branch with `platform/generic/zhihe/a210.c`
- [openeuler-riscv/opensbi-zhihe-a210](https://github.com/openeuler-riscv/opensbi-zhihe-a210) — vendor OpenSBI port
- [revyos/ruyiedk2](https://github.com/revyos/ruyiedk2) — EDK2/UEFI platform firmware; the README covers Melon Pi V1 and V2, and `docs/melonpi.md` documents native RAM boot and USB fastboot
- [openeuler-riscv/bootloader-build · zhihe-a210](https://github.com/openeuler-riscv/bootloader-build/tree/master/zhihe-a210) — prebuilt boot firmware from the openEuler RISC-V SIG: `binman-emmc_boot-loader.img` (flashed to the eMMC BOOT1 partition), `bootzero-rvbl.bin` and `binman-spl-with-fit-rvbl.bin` (the two Fastboot payloads), plus `a210-opensbi.dtb`; the README gives the K1+K2 Fastboot entry, the two-stage `fastboot flash ram` sequence, the `mmc0boot0` write, and the `env set fdtfile zhihe/a210-dev.dtb` + `env save` step over serial. Follow it when flashing an openEuler 24.03 LTS image onto A210.
- SCMI boot chain (`a210/scmi-v3` branches, 2026-11-02): [coreboot](https://github.com/revyos/coreboot/tree/a210/scmi-v3) · [OpenSBI](https://github.com/revyos/opensbi/tree/a210/scmi-v3) · [EDK2](https://github.com/revyos/edk2/tree/a210/scmi-v3) · [RevySR/linux, the full tree with the remaining peripherals](https://github.com/RevySR/linux/tree/a210/scmi-v3) — matches the v3 RFC; the earlier `a210/scmi` branches are still there, and `revyos/ruyiedk2` has `a210/scmi-v3` as well; the tree behind the v4 series is [RevySR/linux `a210/scmi-v4`](https://github.com/RevySR/linux/tree/a210/scmi-v4) (2026-11-18, with CPU DVFS over SCMI Performance plus the remaining peripherals), while the boot-chain repositories keep their branch names
- [RevySR/zephyr `xuantie/scmi-v3`](https://github.com/RevySR/zephyr/tree/xuantie/scmi-v3) — the SCMI server firmware (Zephyr) running on the E902; it owns power, the PMIC and CPU DVFS timing; a second branch, `xuantie/vcodec-v3` (2026-11-02), prepares the VP clocks, resets and power domains for the VC9000D and exports the video codec resources to the AP through the SCMI server
- [RevySR/linux `a210/vcodec-v3`](https://github.com/RevySR/linux/tree/a210/vcodec-v3) — new 2026-11-02 development branch for video decoding: it adds the A210's VC9000D decoder (including VP9) to the hantro driver plus the matching device-tree nodes
- RevySR/linux carries more A210 branches than the SCMI one: [a210/bringup-v7.3](https://github.com/RevySR/linux/tree/a210/bringup-v7.3) (bring-up, 2026-10-22), [a210/scmi-bootchain-v7.3](https://github.com/RevySR/linux/tree/a210/scmi-bootchain-v7.3) (SCMI boot chain, 10-27) and [b4/a210-init](https://github.com/RevySR/linux/tree/b4/a210-init) (the first patch series, 10-21) — pick the one matching what you want to test

**Distribution layer**

- [riscv/meta-riscv](https://github.com/riscv/meta-riscv) — the OpenEmbedded/Yocto RISC-V layer lists a `zhihe-a210` machine ("Zhihe Computing Archimedes A210"), and `conf/machine/zhihe-a210.conf` exists; [PR #744](https://github.com/riscv/meta-riscv/pull/744), merged on 2026-11-07, switched the BSP kernel source to the `v7.2.12-a210` tag of `riseproject-dev/linux` (`a210_evb_defconfig`) and added `test-zhihe-a210.yml`: cloud build plus a TFTP netboot run on the OSU-OSL board farm; [PR #748](https://github.com/riscv/meta-riscv/pull/748), merged on 2026-11-10, widens that workflow's path filters and switches to `readlink -f`
- [git.osuosl.org/osuosl/zhihe-a210-kernel](https://git.osuosl.org/osuosl/zhihe-a210-kernel) — OSU-OSL's own A210 kernel tree, 11 branches (`osl/a210-mainline`, `osl/a210-6.6.x-lts` and per-version backups); tag `v7.2.12-osl-a210` (2026-10-23, marks the OpenSBI region `no-map`) is exactly the kernel meta-riscv's TFTP netboot instructions point at, next to v2.9.0 / v2.8.1 / v2.8.0 / v2.7.0 and vendor 2.6.0-rc0
- [openRuyi-BSP-RPM/zhihe-a210](https://git.openruyi.cn/openRuyi-BSP-RPM/zhihe-a210) — openRuyi's A210 BSP RPM spec repo (4 commits, last one on 2026-08-21) packaging `firmware-zhihe-a210`, `linux-zhihe-a210-vendor-6.6` and `linux-zhihe-a210-vendor-6.6-rogue`; the same group also holds `rvck`, `spacemit-k1` and `spacemit-k3`
- irradium 3.8 `zhihe_a210` images — core and xfce variants, with a **fresh batch rebuilt on 2026-11-21**: core 6.6.0 (1.55 GB), core 7.2.15 (1.64 GB) and xfce 6.6.0 (2.88 GB), plus one core 6.6.157 image built 09-21 (1.50 GB): [mirror directory](http://ubuntu-releases.acc.umu.se/mirror/irradium.org/images/zhihe_a210/) (the official `dl.irradium.org` answers 403 for that tree and the official boards page does not list A210, so treat it as a community build); the `kernel/` subdirectory carries three package sets — `kernel-a210#6.6.0` / `#6.6.157` / `#7.2.15`, each with kernel (387 MB / 371 MB / 505 MB), kernel-firmware (~1.0 GB) and kernel-source (~285 MB); the 7.2.15 set is new on 11-21, so swapping kernels no longer needs a full reflash; the boot tarballs are still `boot-20260908.tar.xz` and `boot-20260921.tar.xz`. Its README documents the A210 fastboot bootloader flash and the u-boot variables (`/EFI/irradium/grubriscv64.efi` and `/dtb/zhihe/a210-dev.dtb`)
- **FreeBSD bring-up (2026-10-30)**: [RevySR/freebsd-src `a210/bringup`](https://github.com/RevySR/freebsd-src/tree/a210/bringup) — a non-Linux port attempt for the A210: 48 commits on top of FreeBSD main (base is the 10-29 commit), including `riscv: Add Zhihe A210 support`, a PCIe host controller driver with the E16 PCIe/SATA PHY, `sdhci_zhihe` HS400 ES, dual-role dwc3 and dwc_otg buffer DMA, an FDT attachment for ig4 plus the tca64xx PMIC, eqos fixes, and `clk: Add a GPIO gated clock driver`, with SCMI / mmio_sram / FDT AHCI enabled; everything stops at 10-30, it is bring-up stage only — not upstream and no images
- **NixOS bring-up (third party, 2026-11-20)**: [NixOS bring-up on an Alibaba RISC-V board](https://feyor.sh/blog/nixos-bringup-on-an-alibaba-riscv-board/) — George Huebner turned an A210 into a NixOS build server; it is the most detailed third-party distro write-up so far. Cross compilation needs only `crossSystem.system = "riscv64-linux"`; across more than a thousand packages only two failures showed up and neither was RISC-V-specific (`rust-bindgen` picking the wrong clang, `ministream` missing cross settings), while linking heavy packages like Clang and GFortran peaked above 9 GB per process and had to be run with parallelism turned down. The boot flow follows the vendor chain U-Boot FSBL → OpenSBI → U-Boot SSBL → Linux; the real trap was OpenSBI built with `-march=rv64gv`, whose vector code hit an illegal instruction on `vsetivli` because the vector context in `mstatus` was not enabled — rebuilding with `-march=generic` fixed it. After that UART went silent at `clk: Disabling unused clocks`; adding `clk_ignore_unused` (the vendor cmdline does the same) reached userspace. The GPU is a PowerVR BXM-4-64, already supported by upstream `drm/imagination` and Mesa; the author ported the 6.18 driver onto the vendor 6.6 kernel and scored 2445 in vkmark 2025.01, with HDMI, audio, Wi-Fi/Bluetooth and Ethernet verified. Two environment traps are also documented: macOS refusing to enumerate the board in Fastboot mode, and a floating `vRef` on a Black Magic Probe killing UART output.
- [RevySR/rvck-image](https://github.com/RevySR/rvck-image) — rootfs/disk image build; the README documents the "flash through Melon Pi EDK2" flow (F9 into Fastboot, `flash emmc0`)
- [riseproject-dev/android_manifest](https://github.com/riseproject-dev/android_manifest) — RISE Android 17 BSP covering the Alibaba A210 EVB, with lunch target `aosp_a210_evb-trunk_staging-userdebug`; the [android-17-v1.0 release](https://github.com/riseproject-dev/android_manifest/releases/tag/android-17-v1.0) of 2026-10-14 also ships a prebuilt `rise-android-17-v1.0-a210-evb.tar.gz` (1.24 GB) plus `SHA256SUMS`, with a K3 Pico-ITX image under the same tag — android-mainline 7.1 kernel, graphics on upstream `drm/imagination` and Mesa; the nightly pipeline was **rewritten wholesale on 2026-11-20** (commit `195084be`, `ci: publish nightly pre-releases and releases`): new `.github/scripts/release.py` (367 lines) and `package-android.sh`, [nightly.yml](https://github.com/riseproject-dev/android_manifest/blob/android-17/.github/workflows/nightly.yml) rewritten at 258 lines (01:23 UTC every night, builds only when the pinned manifest differs, K3 first then a210, keeps the last seven pre-releases), plus `release.yml` and [release-tags.yml](https://github.com/riseproject-dev/android_manifest/blob/android-17/.github/workflows/release-tags.yml) — the latter tags every riseproject-dev repository named in the manifest with the release tag once a final release is published, provided the commit is on the branch. The rewrite did wipe the old nightlies at the time (the tags `android-17-nightly-20261119` / `-20261120` / `-20261121` were all 404 and the [releases page](https://github.com/riseproject-dev/android_manifest/releases) held only `android-17-v1.0`), but the rewritten pipeline ran successfully for the first time on **2026-11-21**: the 08:22 UTC nightly passed and published the pre-release [android-17-nightly-20261121](https://github.com/riseproject-dev/android_manifest/releases/tag/android-17-nightly-20261121) at 11:46, carrying `rise-android-17-nightly-20261121-a210-evb.tar.gz` (1.24 GB) plus a K3 Pico-ITX build, `default.xml` pinning every project to the commit that was built, and `SHA256SUMS`; `release-tags.yml` skipped as designed on a nightly tag. The release notes state it was not tested on hardware. Always cite the newest entry on the releases page rather than a specific tag.
- [riseproject-dev/android_kernel_device](https://github.com/riseproject-dev/android_kernel_device) — the Kleaf device fragments behind that BSP (`alibaba/a210/`, `zhihe_a210.fragment`)
- [riseproject-dev/android_bootloader_build](https://github.com/riseproject-dev/android_bootloader_build) — RISE's boot-chain build repository; the `alibaba-android-17` branch produces the U-Boot + OpenSBI pair for a210 (AVB verification disabled, Android GPT layout for the 64 GB eMMC)
- [riseproject-dev/android_vendor_rise](https://github.com/riseproject-dev/android_vendor_rise) — RISE's repository of prebuilt boot chains and firmware (`alibaba/a210/bootloader/`): `u-boot.bin`, `spl-with-fit-rvbl.bin`, `bootzero-rvbl.bin`, `riscv-boot.itb`, `emmc-gpt_primary.img`, `a210.dtb` and the RTL8822CS Bluetooth firmware; CI rebuilds them every three hours from the upstream bootloader repositories, so you do not have to build a U-Boot + OpenSBI pair for the A210 EVB yourself
- [BayLibre/android_device_alibaba_a210](https://github.com/BayLibre/android_device_alibaba_a210) — an AOSP device tree maintained by BayLibre (`android-17` branch, `PRODUCT_SHIPPING_API_LEVEL` 37): the lunch target is the same `aosp_a210_evb-trunk_staging-userdebug`, but `TARGET_ARCH_VARIANT := a210`, because neither the C920 nor the C908 implements Zvbb and the riscv64 baseline will not build; U-Boot/OpenSBI and the kernel are staged as prebuilts, and the debug console is `ttyS4` at 115200. It already carries RTL8822CS WiFi/Bluetooth, HDMI audio, the PowerVR Vulkan declarations and a riscv64 WebView. This is a separate Android 17 tree from the RISE one above
- [BayLibre/android_device_alibaba_a210_kernel](https://github.com/BayLibre/android_device_alibaba_a210_kernel) — the prebuilt kernel repository for that device tree: `mainline/` holds `Image`, `a210-evb.dtb`, `System.map`, `vmlinux.symvers` and the dlkm directories, plus development branches `glaroque/a210-fixes` and `jmasson/a210-fixes-wifi-bt`
- [RuyiSDK support matrix: A210 SODIMM V2](https://matrix.ruyisdk.org/boards/A210_SODIMM_V2/) ([source directory](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2) · [others.yml](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml)) — Debian and Buildroot are both marked `wip`; `wip` means in progress, not working
- [ruyisdk/ruyi](https://github.com/ruyisdk/ruyi) — the package manager **does have an A210 device entry now** (`entities/device/zhihe-a210-sodimm.toml`, with V2 / V3 variants, merged with [PR #208](https://github.com/ruyisdk/packages-index/pull/208) on 2026-08-27); the board image packages `zhihe-br2image-a210-evb` and `zhihe-diskimage-a210-evb-debian` only go up to **2.8.1** (2.9.0 is not packaged yet) and come with the `zhihe-a210-v1` provisioning strategy and partition map — so ruyi recognises the board and can flash the 2.8.1 images by partition table, while 2.9.0 still means the official artifact server

---

## 6. GitHub at a glance

The A210 GitHub ecosystem is thin and falls into four lines: **RVCK** (most complete device trees), **RevyOS** (kernel commits + EDK2 firmware), **RISE Project** (U-Boot / OpenSBI / Android BSP) and **meta-riscv** (Yocto machine). There is **no official Zhihe GitHub organisation** (`orgs/zhcomputing` returns 404); all official material lives on the documentation site.

Everything already listed in section 5 is not repeated here; the remainder:

- [kubuds/A210-Melon-Pi-all-in-one](https://github.com/kubuds/A210-Melon-Pi-all-in-one) — this index
- [ruyisdk/packages-index PR #208](https://github.com/ruyisdk/packages-index/pull/208) — the ruyi-side A210 device and flashing strategy
- [riseproject-dev/developer-cloud](https://github.com/riseproject-dev/developer-cloud) (formerly `board-farm`, renamed 2026-11-11) — the RISE RISC-V Developer Cloud management repo: the first 20 Zhihe A210 boards (donated by Alibaba) sit at Oregon State University's OSU-OSL, with a Labgrid `a210-yocto` pool in Phase 1, plus Scaleway (France) and SOPIC (China) sites; the repo holds `boards/zhihe-a210/` client/exporter configs and pytest cases, and four A210 pipelines under `.github/workflows/` (`a210_netboot.yml` TFTP in-memory boot for a210-board-01 to 05, `a210_labgrid_uboot.yml`, `yocto-zhihe-a210.yml`, and `a210_telemetry.yml`, added 2026-11-11 for non-destructive hardware telemetry); the hub side also gained board tag publishing with tag/search filtering and Android board detection via ADB or UART, and fixed a zhihe-a210 UART echo issue that broke kernel version probing; a [PR #5](https://github.com/riseproject-dev/developer-cloud/pull/5) opened 2026-11-13 (**closed unmerged on 2026-11-20**; neither document is on `main`) adds two status documents: `docs/status/current_status.md` covers the OSU-OSL A210 fleet (`a210-1` to `a210-5`), the Shelf 1 `a210-s1-b01` to `b10` assembly milestones, the Shelf 2 BayLibre Copilot and Relay Hat DFU design, the three-tier x86 host topology (`osl-labgrid` and `proj-rise` Chef cookbooks) and the `pool=a210-yocto` / `pool=a210-android` CI pools, while `docs/status/2026_weekly_progress.md` is a reverse-chronological sync log; on 2026-11-14 the Yocto netboot tests moved off the hand-rolled pyserial UART parsing and `===CI_PROBE_START===` sentinels onto Labgrid's native UBootDriver and ShellDriver, adding a `ZhiheA210TftpBootStrategy` (`boards/zhihe-a210/strategy.py`, `helpers.py`, with `client.yaml` wiring SerialDriver / UBootDriver / ShellDriver and the tests collapsed to `test_uname_a` / `test_smp_cores` / `test_opensbi_reserved_memory`), see [commit c7d058e](https://github.com/riseproject-dev/developer-cloud/commit/c7d058e8a6dd53a180c9fbd741d3032c460bc8be) by Puneetha Ramachandra of Google. The commits from 2026-11-17 to 11-18 wired AOSP into Labgrid as well: a new AOSP hardware CI workflow (`ci(a210-aosp)`, with `runs-on` pinning the Developer-Cloud-HW runner group) and a Labgrid AOSP UDP fastboot strategy; the AOSP tests now read `/proc/mounts` to detect boot, relax the kernel version prefix match, load a staged `zhihe_wdt.ko` before rebooting when present, and the `SHA256SUMS` parsing tolerates a `./` prefix; on the hub side `serial_port` is pinned to `/dev/serial/by-path/` and the serial probe recognises the `u-boot#` prompt; 11-18 added Labgrid export, driver and a smoke test for ADB over USB-C (commit `ef4e93e0`).

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
