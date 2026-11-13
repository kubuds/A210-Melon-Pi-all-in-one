# 知合 A210 資源總匯（SODIMM V2 / V3 · 算力棒）

[簡體中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [English](README.en.md) · [Русский](README.ru.md) · [日本語](README.ja.md) · [Deutsch](README.de.md) · [Español](README.es.md)

知合計算 A210（對外也叫「阿基米德 A210」）能公開找到的資源都收在這一頁：官方文件與規格書、**可直接下載的官方映像檔**、按板型分的燒錄指南、硬體設計檔案、上游核心與韌體進展、GitHub 與 Gitee 專案，以及 B 站和 YouTube 上真的用了這塊板子的影片。

本頁不鏡像任何韌體與文件本身，只給出處。**記的是連結與事實，不是使用承諾** —— 刷機前請核對板卡版本、映像檔說明與校驗值。

> **先把名字對上，這塊板子的叫法比一般開發板亂。**
>
> - **晶片**：知合計算 A210，產品系列名「阿基米德」（Archimedes A210），通推一體異構 AI SoC。
> - **板卡形態**：SODIMM 核心板 + 底板（**V1 / V2 / V3** 三代底板），另有 **A210 算力棒（Dongle）** 形態。
> - **「Melon Pi / MelonPi」是誰在叫**：知合官方文件與規格書裡**沒有**這個名字（官方只用「A210 SODIMM V1/V2/V3」）；它出現在上游 Linux 補丁的裝置樹檔名（`a210-melonpi-v1.dts` / `-v2.dts`）、玄鐵在華秋開源硬體頁的標題（「玄鐵 MelonPi A210」）以及部分媒體報導裡。看到 Melon Pi，指的是同一塊板的核心／社群叫法。
> - **別和 A200 混**：知合還有 A200 平台，官方 Ubuntu 映像檔只給 A200；A210 官方只出 Buildroot 與 Debian 桌面兩套映像檔。

---

## 1. 關鍵規格

| 項目 | 參數 |
| --- | --- |
| SoC | 知合計算 A210（通推一體異構 AI SoC） |
| CPU | 4× 達摩院玄鐵 C920 + 4× 達摩院玄鐵 C908，RV64GCV（帶向量） |
| 頻率 | 官方規格書寫 1.9 GHz；CNX Software 報導寫 C920 最高 2.3 GHz、C908 1.9 GHz（兩處說法不一致，以你手上批次與規格書為準） |
| GPU | 支援 Vulkan 1.1/1.2/1.3、OpenCL 1.1/1.2/2.0、OpenGL ES 1.1/2.0/3.0/3.1/3.2（官方規格書未點名型號；「IMG BXM-4-64」出自 RuyiSDK 支援矩陣中繼資料） |
| NPU | 12 TOPS@INT8，支援 INT4/INT8/INT16/FP8/FP16/BF16 |
| 記憶體 | 4 / 8 / 16 GB 64-bit LPDDR4x，最高 4266 Mbps |
| 儲存 | eMMC 5.1/5.0、NOR/NAND Flash、SD 3.0 |
| 網路 | 2× 10/100/1000 Mbps Gigabit 網路埠 |
| 顯示 | 1× HDMI 2.0、1× 4-lane MIPI DSI、DP / eDP（受 USB 共用限制） |
| 攝影機 | 1× 4-lane + 1× 2-lane，或 3× 2-lane MIPI CSI |
| 擴充 | PCIe x4 / x2 + x1、x2 + 2× SATA、2× x1 + 2× SATA；2× SPI、1× QSPI、7× I²C、10× UART、3× 5ch PWM、2× 1ch ADC |
| USB | 1× USB 3.1（DP Alt）、2× USB 2.0 |
| 音訊 | 3× 2ch I2S/PCM、1× TDM/PCM |
| 供電 / 溫度 | 核心板 5V/5A（最低）；底板 12V DC 輸入；-20 °C ~ 60 °C |
| 核心板尺寸 | 59.66 mm × 69.94 mm，260-pin SODIMM |
| 官方 OS | Linux（Debian 桌面 / Buildroot） |

**關於 RVA23 有兩種說法**：OMG! Ubuntu 在 2025-07 的報導裡說 A210 支援 RVA23 全部必選與可選擴充；CNX Software 隨後在留言區與正文更正，認為 A210 屬 RVA22、RVA23 是下一代的 A600。**這條沒有權威結論，別拿它做選型依據。**

資料來源：官方「A210 產品規格書」與「核心板使用者指南」，及[華秋開源硬體社群的產品頁](https://p.eda.cn/d-1389550606774960128)（同一份規格表的轉載）。

---

## 2. 官方文件（知合計算開發者文件中心）

官方文件站是 **developer.zhcomputing.com**，目前 **2.9.0**，另有 **2.8.1** 歷史版本與 `/en/` 英文版。該站前端渲染，`curl` 取不到正文，請用瀏覽器開啟。

**總入口**

- [文件中心首頁](https://developer.zhcomputing.com/zh/docs/intro) · [English](https://developer.zhcomputing.com/en/docs/intro/)
- [A210 文件目錄](https://developer.zhcomputing.com/zh/docs/A210/) · [English](https://developer.zhcomputing.com/en/docs/A210/)
- [2.8.1 歷史版本](https://developer.zhcomputing.com/zh/docs/2.8.1/category/sdk)

**規格書與燒錄（按板型分冊，選錯會燒不進去）**

- [A210 產品規格書（HTML 全文）](https://developer.zhcomputing.com/zh/docs/A210/A210_Datasheet) —— 功能特性、封裝、腳位定義與時序
- [映像檔燒錄指南（索引）](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/)
- [SODIMM V2 燒錄指南](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V2_Burning_Instruction) —— 12V DC 供電、TTL 115200 偵錯埠、USB-A 燒錄埠；按住燒錄鍵 + 重置進 USB 模式；Windows 用 platform-tools r34.0.5 + usb_driver r13，Linux 用 android-sdk-platform-tools
- [SODIMM V3 燒錄指南](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V3_Burning_Instruction)
- [算力棒（Dongle）燒錄指南](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_Dongle_Burning_Instruction) —— 這個形態很容易被漏掉

**硬體平台**

- [核心板使用者指南](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/核心板说明) —— 關鍵參數、尺寸、260-pin 腳位定義
- [SODIMM V2 底板使用者指南](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V2_baseboard_developer_guide) —— 介面、BOOT_SEL、PCIe RC/EP 切換、UART4 偵錯序列埠
- [SODIMM V2 底板原理圖](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V2)（V1/V3 與算力棒各有獨立頁）
- [硬體設計指南](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/) —— 自研載板前必讀
- [PINMUX](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/A210-PINMUX) · **直接下載表格**：[A210-PINMUX_20260119.xlsx](https://developer.zhcomputing.com/zh/docs/pdf/A210/Hardware-Platform/A210-PINMUX_20260119.xlsx)（約 39 KB，實測可下）

**SDK**

- [SDK 總覽](https://developer.zhcomputing.com/zh/docs/category/sdk) · [快速上手（含映像檔下載表）](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/Basic_quick_start_guide)
- [Buildroot 開發指南](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/Buildroot_developer_guide) —— 從 zdocker 環境到 `./build.sh -b buildroot a210`
- [TORQ SDK 介紹](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ%20SDK%E4%BB%8B%E7%BB%8D) —— 12 TOPS NPU 的上手入口，搭配 TORQ-Toolkit 與 TORQ-LLM API
- 其它分類：[快速上手](https://developer.zhcomputing.com/zh/docs/category/快速上手) · [開發環境建置](https://developer.zhcomputing.com/zh/docs/category/开发环境构建) · [多媒體](https://developer.zhcomputing.com/zh/docs/category/多媒体) · [AI](https://developer.zhcomputing.com/zh/docs/category/ai)

**廠商與製品牌**

- [玄鐵官網 A210 產品頁](https://www.xrvm.cn/product/board/4565261785988403200)（前端渲染，抓不到正文）
- [玄鐵官網首頁](https://www.xrvm.cn/) · [達摩院玄鐵 C920](https://www.xrvm.cn/product/xuantie/C920) · [C908](https://www.xrvm.cn/product/xuantie/C908)
- 知合計算主站 [www.zhcomputing.com](http://www.zhcomputing.com/) —— 2026-11-08 複測：**只能走 http**（`https://` 一律 504 且憑證鏈不完整，直連與代理結果一致）；站上「阿基米德系列」只列 A200 / A300，新聞中心最新一則停在 2025-07，**沒有 A210 頁面**，英文站 `en.zhcomputing.com` 跳轉後是「網站待上線」佔位頁 —— A210 的官方資料仍以文件中心為準；商務聯絡 business@zhcomputing.com

> 文件站頁尾的「GitHub」連結是佔位符（指向 `github.com/your-org`），不是真的專案，不要引用。

---

## 3. 官方映像檔（可直接下載）

只有兩套：**Buildroot**（輕）與 **Debian 桌面**，統一以 `a210-evb` 命名，都走 fastboot 分割映像包。**沒有官方 Ubuntu 映像檔**（Ubuntu 只給 A200）。

| 映像檔 | 版本 | 大小 | 下載 |
| --- | --- | --- | --- |
| Buildroot 預編譯映像檔 | v2.9.0（目前） | 179.4 MB | [br2image-v2.9.0-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/br2image-v2.9.0-a210_evb.tar.gz) |
| Debian 桌面映像檔 | v2.9.0（目前） | 738.4 MB | [diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz) |
| Buildroot 預編譯映像檔 | v2.8.1（回滾用） | 175.9 MB | [br2image-v2.8.1-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/br2image-v2.8.1-a210_evb.tar.gz) |
| Debian 桌面映像檔 | v2.8.1（回滾用） | 734.8 MB | [diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz) |

- 解壓縮後得到 `emmc-*.img`、`bootzero-rvbl.bin`、`fastboot_images.sh` / `.bat`，進燒錄模式後直接跑腳本
- **官方製品庫目錄索引**（比文件表格更完整）：[downloads/release/](http://developer.zhcomputing.com/downloads/release/) —— `zhihesdk` 下有 v2.7.0 / v2.8.0 / v2.8.1 / v2.9.0，另有 `develop/`、`develop-test/` 兩個開發快照目錄（其中 a210 映像檔最新一份是 2026-02-05，比 v2.9.0 舊，別當新版用），`npu` 下有 v1.3–v2.1（ovx-compiler、torq-llm、uca-nn、viplite），`tools` 下有 1.17 GB 的 `ubuntu-24.04-x86_64.v1.7.0.tar.gz` 建置容器
- 想用 RuyiSDK 重現安裝：[ruyisdk/packages-index PR #208](https://github.com/ruyisdk/packages-index/pull/208) 把 fastboot 流程、2.8.1 的 Buildroot 與 Debian 映像檔包、分割表都做成了 ruyi 條目，內含分割對應與校驗和，可用於交叉核對

---

## 4. 硬體設計檔案（開源底板 PDF 與原理圖）

[玄鐵 MelonPi A210 高效能開發板 —— SODIMM V3 開源底板](https://p.eda.cn/d-1389550606774960128)（華秋開源硬體社群，發佈者 XuanTie 玄鐵，**OpenAtom OHL 1.0**）提供：

- **A210 SODIMM 底板原理圖.zip**（2.69 MB）
- **A210 最小系統 原理圖設計建議.pdf**（7.80 MB）
- **A210 最小系統 PCB 設計建議.pdf**（15.55 MB）
- **A210 產品規格書.pdf**（399 KB）—— 目前能拿到 **PDF 版**規格書的唯一管道（官方只提供 HTML）
- **A210-PINMUX_20260119.xlsx**（38.89 KB）

注意這是 **V3 底板**，與官方 V2 文件有一代差異。下載需在站內註冊登入。

---

## 5. 上游核心、韌體與發行版

**上游 Linux 主線**

- [[PATCH 00/18] riscv: add initial support for Zhihe A210 and Melon Pi](https://lists.infradead.org/pipermail/linux-riscv/2026-October/101909.html) —— 首版主線支援（UART/clock/reset/pinctrl + DT），已在 Melon Pi V2 上 8 核全開驗證；裝置樹檔名 `a210-melonpi-v1.dts` / `-v2.dts` 就是「Melon Pi」這個名字的真正出處
- [[PATCH RFC 00/18] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-October/102222.html) —— 2026-10-27 的重做版（作者編號 v2）：A210 還有一顆 E902 管理核，時鐘與復位暫存器實際上由它執行的 Zephyr SCMI 韌體掌管，這一版刪掉原生 clk/reset 驅動、改走標準 SCMI clock/reset 協定，另加 AP→E902 門鈴 mailbox 驅動；已在 Melon Pi V2 上 8 核起到 UART shell。原生驅動那版（上面那條）與這一版**截至 2026-11-02 都還沒進主線**；最新的 v3 見下條
- [[PATCH RFC v3 00/17] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-November/102729.html) —— 2026-11-02 的 v3：rebase 到 v7.4-rc1；`arm_scmi` 移除 ARM 架構依賴（RISC-V 也能編），SCMI clock/reset ID 從 dt-bindings 移到 DTS 旁的 header，mailbox 綁定改為固定的 local / remote 區域；Melon Pi V2 用 riscv defconfig 8 核開到序列埠 shell。仍因等知合韌體原生支援 SCMI 而保持 RFC

**核心與裝置樹（還在各家的開發線裡）**

- [RVCK Linux](https://github.com/RVCK-Project/rvck) —— `rvck-6.6` 分支裡裝置樹最完整： [a210.dtsi](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi) · [a210-melon-pi.dts](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts) · [知合裝置樹繫結](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml)；提交檢索有 41 筆 A210 相關提交，含 GPIO/UART/timer/DMA/sdhci
- [RVCK：A210 周邊支援追蹤 issue](https://github.com/RVCK-Project/rvck/issues/381) · [已合併的周邊支援 PR](https://github.com/RVCK-Project/rvck/pull/382)
- [RVCK：A210 USB 支援 PR #437](https://github.com/RVCK-Project/rvck/pull/437) —— 2026-10-22 開出、**仍 open**，但作者在 2026-11-11 把它轉成了 **draft**：此前已 rebase 到更新後的 `rvck-6.6`（20 個補丁，新增 Melon Pi 第二個 GMAC、UART pinctrl 修正、GPIO ranges、Zicbop block size 與裝置樹整理），當天 Icenowy 又對 `a210.dtsi` 提出三條裝置樹意見（節點 reg 重疊的，建議改回 syscon 或由 clk_usb 註冊一個 aux device；兩個獨立 PHY 應各建一個節點；`syscon` 屬性名要加廠商前綴），11-13 的 CI 全流程通過（check-patch、kunit、kernel-build 與 LAVA QEMU 啟動回收）。功能本體：補 USB 2.0 的兩個 DWC2 控制器與三個 PHY 實例、USB 3.1 的 DWC3 glue 與 USB3.1/DP combo PHY，板級帶上 Melon Pi 的 FUSB302 Type-C 控制器；[PCIe 與 SATA 支援 issue #477](https://github.com/RVCK-Project/rvck/issues/477) 同樣 open
- [RevyOS Linux](https://github.com/revyos/linux) —— [A210 維護條目](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d) · [溫控與看門狗裝置樹](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4) · [PWM 驅動](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d) · [Melon Pi V2 音訊走線](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146)。注意這些提交都在 `rv/a210-upstream-local` 分支上，不在預設分支
- [RISE Project：riseproject-dev/linux](https://github.com/riseproject-dev/linux) —— 存在 `alibaba-a210` 分支

**引導與韌體**

- [riseproject-dev/u-boot](https://github.com/riseproject-dev/u-boot) —— `v2024.10-a210` 分支，樹內含 `a210.dts`、`a210-soc.dtsi`、`board/zhihe/a200-evb`
- [riseproject-dev/opensbi](https://github.com/riseproject-dev/opensbi) —— `v1.5-a210` 分支，含 `platform/generic/zhihe/a210.c`
- [openeuler-riscv/opensbi-zhihe-a210](https://github.com/openeuler-riscv/opensbi-zhihe-a210) —— OpenSBI 廠商移植
- [revyos/ruyiedk2](https://github.com/revyos/ruyiedk2) —— EDK2/UEFI 平台韌體，README 寫明支援 Melon Pi V1 與 V2，`docs/melonpi.md` 記錄原生 RAM 開機與 USB Fastboot
- SCMI 啟動鏈（`a210/scmi-v3` 分支，2026-11-02）：[coreboot](https://github.com/revyos/coreboot/tree/a210/scmi-v3) · [OpenSBI](https://github.com/revyos/opensbi/tree/a210/scmi-v3) · [EDK2](https://github.com/revyos/edk2/tree/a210/scmi-v3) · [RevySR/linux 含其餘周邊的完整樹](https://github.com/RevySR/linux/tree/a210/scmi-v3) —— 與 v3 RFC 配套；早期的 `a210/scmi` 分支仍在，`revyos/ruyiedk2` 也有 `a210/scmi-v3`
- [RevySR/zephyr `xuantie/scmi-v3`](https://github.com/RevySR/zephyr/tree/xuantie/scmi-v3) —— 跑在 E902 上的 SCMI 服務端韌體（Zephyr），電源、PMIC 與 CPU DVFS 時序都由它負責；另一條 `xuantie/vcodec-v3`（2026-11-02）替 VC9000D 備好 VP 時脈、重置與電源域，並透過 SCMI 服務端把視訊編解碼資源匯出給 AP
- [RevySR/linux `a210/vcodec-v3`](https://github.com/RevySR/linux/tree/a210/vcodec-v3) —— 2026-11-02 新增的視訊解碼開發線：hantro 驅動加入 A210 的 VC9000D 解碼器（含 VP9），並補上對應的裝置樹節點
- RevySR/linux 的 A210 分支不止 SCMI 一條：[a210/bringup-v7.3](https://github.com/RevySR/linux/tree/a210/bringup-v7.3)（2026-10-22 的 bring-up）、[a210/scmi-bootchain-v7.3](https://github.com/RevySR/linux/tree/a210/scmi-bootchain-v7.3)（10-27 的 SCMI 啟動鏈）、[b4/a210-init](https://github.com/RevySR/linux/tree/b4/a210-init)（10-21 的首版補丁系列）—— 按你要驗證的環節挑

**發行版層**

- [riscv/meta-riscv](https://github.com/riscv/meta-riscv) —— OpenEmbedded/Yocto 的 RISC-V 層，機器表裡有 `zhihe-a210`（"Zhihe Computing Archimedes A210"），`conf/machine/zhihe-a210.conf` 實際存在；[PR #744](https://github.com/riscv/meta-riscv/pull/744) 於 2026-11-07 合併，把 BSP 核心源切到 `riseproject-dev/linux` 的 `v7.2.12-a210` 標籤（`a210_evb_defconfig`），並加上 `test-zhihe-a210.yml`：雲端建置 + OSU-OSL 板場 TFTP 網路啟動實測；[PR #748](https://github.com/riscv/meta-riscv/pull/748) 於 2026-11-10 合併，擴充該工作流的觸發路徑過濾並改用 `readlink -f`
- [RevySR/rvck-image](https://github.com/RevySR/rvck-image) —— rootfs／磁碟映像檔建置，README 給出「透過 Melon Pi EDK2 fastboot 刷寫」流程（F9 進 Fastboot，`flash emmc0`）
- [riseproject-dev/android_manifest](https://github.com/riseproject-dev/android_manifest) —— RISE Android 17 BSP，涵蓋 Alibaba A210 EVB，給出 lunch 目標 `aosp_a210_evb-trunk_staging-userdebug`
- [riseproject-dev/android_kernel_device](https://github.com/riseproject-dev/android_kernel_device) —— 上面的 Kleaf 裝置片段（`alibaba/a210/`、`zhihe_a210.fragment`）
- [riseproject-dev/android_bootloader_build](https://github.com/riseproject-dev/android_bootloader_build) —— RISE 的啟動鏈建置倉，`alibaba-android-17` 分支產出 a210 用的 U-Boot + OpenSBI（關掉 AVB 校驗，64 GB eMMC 的 Android GPT 分割布局）
- [riseproject-dev/android_vendor_rise](https://github.com/riseproject-dev/android_vendor_rise) —— RISE 的預編譯啟動鏈與韌體倉（`alibaba/a210/bootloader/`）：`u-boot.bin`、`spl-with-fit-rvbl.bin`、`bootzero-rvbl.bin`、`riscv-boot.itb`、`emmc-gpt_primary.img`、`a210.dtb`，外加 RTL8822CS 的藍牙韌體；CI 每 3 小時依上游 bootloader 倉重建一次，想要一份現成的 U-Boot + OpenSBI 組合給 A210 EVB 時不用自己編
- [BayLibre/android_device_alibaba_a210](https://github.com/BayLibre/android_device_alibaba_a210) —— BayLibre 維護的 AOSP 裝置樹（`android-17` 分支，`PRODUCT_SHIPPING_API_LEVEL` 37）：lunch 目標同樣是 `aosp_a210_evb-trunk_staging-userdebug`，但 `TARGET_ARCH_VARIANT := a210`（C920 與 C908 都沒有 Zvbb，不能用 riscv64 基線），U-Boot/OpenSBI 與核心都按預編譯放進樹裡，偵錯序列埠 `ttyS4` 115200；樹內已帶 RTL8822CS 的 WiFi/藍牙、HDMI 音訊、PowerVR 的 Vulkan 宣告與 riscv64 WebView。與上面 RISE 那套是各自獨立的 Android 17 樹
- [BayLibre/android_device_alibaba_a210_kernel](https://github.com/BayLibre/android_device_alibaba_a210_kernel) —— 上面那套裝置樹用的核心預編譯倉，`mainline/` 下有 `Image`、`a210-evb.dtb`、`System.map`、`vmlinux.symvers` 與 dlkm 目錄；另有 `glaroque/a210-fixes`、`jmasson/a210-fixes-wifi-bt` 兩條開發分支
- [RuyiSDK 支援矩陣：A210 SODIMM V2](https://matrix.ruyisdk.org/zh-CN/boards/A210_SODIMM_V2/)（[原始碼目錄](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2) · [others.yml](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml)）—— Debian 與 Buildroot 均標 `wip`；`wip` 是「在做，沒做完」，不等於可用
- [ruyisdk/ruyi](https://github.com/ruyisdk/ruyi) —— 套件管理器，有 zhihe 廠商命名規範，但**尚無 A210 專屬裝置條目**，別以為裝上 ruyi 就有 A210 映像檔

---

## 6. GitHub 專案一覽

A210 的 GitHub 生態很薄，能歸成四條線：**RVCK**（裝置樹最完整）、**RevyOS**（核心提交 + EDK2 韌體）、**RISE Project**（U-Boot / OpenSBI / Android BSP）、**meta-riscv**（Yocto 機器）。GitHub 上**沒有知合的官方組織**（`orgs/zhcomputing` 404），官方資料全在文件站。

上面第 5 節已列出的不再重複；其餘相關：

- [kubuds/A210-Melon-Pi-all-in-one](https://github.com/kubuds/A210-Melon-Pi-all-in-one) —— 本索引倉庫
- `ruyisdk/packages-index` 的 [PR #208](https://github.com/ruyisdk/packages-index/pull/208) —— ruyi 側的 A210 裝置與燒錄策略
- [riseproject-dev/developer-cloud](https://github.com/riseproject-dev/developer-cloud)（原 `board-farm`，2026-11-11 改名）—— RISE 的 RISC-V Developer Cloud 管理倉：首批 20 塊知合 A210（阿里捐贈）放在奧勒岡州立大學 OSU-OSL，Phase 1 用 Labgrid 起 `a210-yocto` 板池，另有 Scaleway（法國）與 SOPIC（中國）機房；倉內有 `boards/zhihe-a210/` 的 client/exporter 設定與 pytest 用例，`.github/workflows/` 下四條 A210 流水線（`a210_netboot.yml` 的 TFTP 記憶體啟動 a210-board-01 至 05、`a210_labgrid_uboot.yml`、`yocto-zhihe-a210.yml`，以及 2026-11-11 新增的 `a210_telemetry.yml` 非破壞性硬體遙測）；同期 hub 側加了板卡標籤發布與標籤/搜尋過濾、用 ADB 或 UART 自動辨識 Android 板，並修掉 zhihe-a210 的 UART 回顯干擾核心版本探測的問題

---

## 7. Gitee 專案

Gitee 上直接面向 A210 的倉庫很少，且 **Gitee 的站內搜尋 API 目前對任何關鍵字都回傳空**，所以這一節**不保證窮盡**：

- [agiros/yolov5_torq_camera](https://gitee.com/agiros/yolov5_torq_camera) —— 描述原文「主要用於 A210 單板，可以透過 torq 呼叫 yolov5 模型，並將辨識的結果和畫面發送為 AGIROS 話題」。注意 README 還是 Gitee 預設範本
- [agiros/ur5-demo](https://gitee.com/agiros/ur5-demo) —— AGIROS 的 A210 機械臂教學裡 `git clone` 的就是這個倉，在 A210 + openEuler 24.03 上做 UR5 視覺抓取；倉庫本身不提 A210，是「被 A210 專案實際使用」

> 坑：搜尋「a210」會大量命中嘉楠 **K210** 的專案；`gitee.com/zhihe` 是「知和先生」個人號，與知合計算無關。

---

## 8. 影片

**B 站（全站只有 4 條，其中只有 1 條標題帶 Melon Pi）**

- [知合玄鐵A210 Melon Pi開發板試用](https://www.bilibili.com/video/BV1wdx969Exj/) · donatello1996 · 2026-11-04 · 約 34 播放 —— 21 秒的點陣屏片段：兩塊點陣屏在刷溫濕度、氣壓讀數與手勢狀態，外加一個表情動畫；**全程沒拍到板子本體**，只能靠標題與標籤（RISC-V、玄鐵、開發板）判斷跑的是這塊板。B 站上第一條標題帶 Melon Pi 的影片
- [基於 A210 x AGIROS 的智慧機器人解決方案](https://www.bilibili.com/video/BV12KFKzkELG/) · AGIROS 開源社群 · 2026-02-02 · 約 62 播放 —— AGIROS Meetup 北京站 Part5，講者申壯是知合計算技術（杭州）的資深 AI 工程師；**這是目前唯一由知合在職工程師講 A210 的影片**（14 分 10 秒），談方案不談跑分
- [知合計算 阿基米德 A210 RISC-V 開發板開箱 玄鐵 C920 核心 + NPU 通推一體](https://www.bilibili.com/video/BV1fJrnBsENd/) · DSOE1024 · 2026-01-14 · 約 1.7k 播放 —— **目前唯一一條開箱實拍**（2 分 48 秒）
- [知合計算 A210 問世，「產學研」閉環的標竿案例 A600 呼之欲出](https://www.bilibili.com/video/BV19R84zsEVH/) · 石榴派-袁德俊 · 2025-07-26 · 428 播放 —— 峰會資訊解讀，不是板子實測

**YouTube（只有 1 條，且是規格羅列 + 導購）**

- [Struggling with local AI projects? This RISC-V dev kit might help](https://www.youtube.com/watch?v=yK5x93THqLE) · 스마트직구연구소 —— 描述寫明 Sipeed ZHIHE A210 RISC-V AI Dev Kit，內容是規格羅列、非實測

**沒有教學、沒有開發實錄、沒有發表會錄影**。知合計算在 B 站與 YouTube 都沒有官方帳號。這是這塊板目前最真實的狀況，不粉飾。

---

## 9. 中文教學、實作與報導

- [AGIROS + RISC-V 知合 A210 全棧打通並實機驗證](https://ruyisdk.cn/t/topic/2362) —— **目前最完整的中文實作帖**：燒 openEuler 24.03 LTS（含 root 密碼 `openEuler12#$`）、網路與靜態 IP、一鍵裝 AGIROS 25.12、ur5-moveit-demo、手眼標定、實體 UR5 抓取
- [知合計算 A210 開發板開箱（影片轉帖）](https://ruyisdk.cn/t/topic/2412) —— 短帖，看外觀與介面佈局
- [玄鐵 MelonPi A210 SODIMM V3 開源底板](https://p.eda.cn/d-1389550606774960128) —— 硬體側最實用的一篇（含 22 個介面說明、BOOT_SEL、PCIe RC/EP、UART4）
- 阿里雲開發者社群 [第二屆 CIE 全國 RISC-V 高水準創新及應用大賽賽題說明](https://developer.aliyun.com/article/1749897) —— 賽題一「A210 邊緣視覺 Agent 應用」，明確要求基於 A210（12 TOPS NPU）與官方 Debian 映像檔，做影像擷取 + 端側 YOLOv5/v8 + 雲端大型模型對話。**想找 A210 練手專案，照這個題目做就行**
- 微博長文 [玄鐵·踐行：在產線、機器人和邊緣算力上「跑起來」](https://weibo.com/ttarticle/x/m/geoshow/id/2309405355143666729355) —— 少見的實測數字：MobileNetV2 847 FPS、YOLOv8n 336 FPS、Qwen3-4B 本地推理 19 token/s；另有 AI NAS、16 路 1080P 邊緣閘道、12 TOPS 算力棒、4 顆 A210 互聯的 48 TOPS PCIe 卡等方案
- [知合計算與您相約 AICC2025](https://mp.weixin.qq.com/s/e11WDCFZoI5CtObrTIFO5g) —— 公眾號上唯一提及 A210 的文章，純活動預告，零技術內容

**英文報導**

- CNX Software [Zhihe A210 octa-core RISC-V SoC with 12 TOPS NPU powers SoM-based development board](https://www.cnx-software.com/2026/06/17/zhihe-a210-octa-core-risc-v-soc-with-12-tops-npu-powers-som-based-development-board/) —— 最完整的一篇英文報導
- CNX Software [Three high-performance RISC-V processors to watch in H2 2025](https://www.cnx-software.com/2025/07/22/three-high-performance-risc-v-processors-to-watch-in-h2-2025-ultrarisc-ur-dp1000-zizhe-a210-and-spacemit-k3/) —— A210 首次進入國際視野
- OMG! Ubuntu [New RVA23 RISC-V chips are coming sooner than you think](https://www.omgubuntu.co.uk/2025/07/ubuntu-risc-v-rva23-hardware-coming-soon) —— 注意其 RVA23 說法與 CNX 的更正衝突（見第 1 節）

> 取不到的：CSDN、知乎、`bbs.21ic.com`、`eefocus.com` 在本機網路下回傳 521 / 403 / 驗證碼頁，正文無法核驗，因此一條都沒收。`x-techcon.com` 那篇 AGIROS 文已 404（同內容在 ruyisdk 那篇裡）。openEuler 的 A210 映像檔路徑 `images.oerv.ac.cn/.../zhihe/a210-dev/` 實測 404，要用請走 openEuler RISC-V SIG 官方管道確認。

---

## 10. 哪裡買

- **苦芽科技淘寶企業店**：https://item.taobao.com/item.htm?id=1034868327078&skuId=6052940225420 —— 頁面需登入淘寶才能看到商品詳情，連結本身回傳 200
- AliExpress 上的第三方（chipboard store）標「Sipeed ZHIHE A210」，8GB/64GB 配置約 $334（頁面會跳到登入牆，價格只能作參考）
- 知合計算本身沒有公開直銷頁與報價頁

---

## 11. 上手前必看

1. **確認板型與版本**：SODIMM V1 / V2 / V3 還是算力棒；底板不同，燒錄按鍵時序、供電、介面都不一樣，**燒錄指南是按板型分冊的**。
2. **映像檔只有兩套**（Buildroot / Debian 桌面），都以 `a210-evb` 命名；官方沒有 Ubuntu。想回滾就用 2.8.1 那一對。
3. **V2 底板是 12V DC 供電**，核心板本身 5V/5A；偵錯序列埠是 **UART4**，115200。
4. **不要熱插拔底板**，操作前做防靜電；開機模式靠 BOOT_SEL 上拉／下拉電阻，PCIe 有 RC/EP 切換。
5. 支援矩陣裡的 `wip` 不等於能用；碰到裝置樹或驅動問題，回報時附上板型、映像檔與核心版本、完整序列埠日誌。

---

## 12. 這個索引怎麼維護

- 每天 13:00 自動執行一次全網增量掃描（官方製品庫新版本、文件站新頁面、新影片、新倉庫），有變化就更新
- 只收**能開啟**的連結；每次更新跑一遍全量連結檢查，失效連結下線或換新網址
- 影片要求確實拍了 A210；專案要求倉庫裡真的有 A210 的裝置樹、分支或 BSP（不是只提一句）
- 收錄不代表背書。官方映像檔之外的第三方建置、授權條款與維護狀態請自行判斷
- 缺漏歡迎提 issue / PR，請註明原始來源、適用板型與造訪日期

[返回語言索引](README.md)
