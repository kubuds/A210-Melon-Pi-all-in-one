# 知合 A210 / Melon Pi 資源彙整

[简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [English](README.en.md) · [Русский](README.ru.md) · [日本語](README.ja.md) · [Deutsch](README.de.md) · [Español](README.es.md)

本文彙整目前可核驗的 A210 開發板公開資料。各頁面可能隨上游更新；連結所指原文是規格、映像檔及支援狀態的最終依據。此清單持續補充，不代表已窮盡網路資源。

## 開發板概覽

[RuyiSDK 開發板支援矩陣](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2)收錄了 **A210 SODIMM V2**，並列出以下資訊：

| 項目 | 支援矩陣所列資訊 |
| --- | --- |
| 廠商 | ZHIHE COMPUTING（知合） |
| SoC | A210 |
| CPU 核心 | XuanTie C920 + XuanTie C908 |
| GPU | IMG BXM-4-64 |
| 記憶體組態 | 4 GB / 8 GB / 16 GB |

以上資訊來自該支援矩陣頁面，不應據此推論其他硬體版本的組態。請以手上開發板的絲印、產品資料及目前版本文件為準。

## 開發板專屬資源

### 硬體資料與系統支援

- [RuyiSDK A210 SODIMM V2 支援矩陣頁面](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2)：開發板條目及專案狀態。
- [硬體與處理器資訊（README）](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/README.md)：處理器、核心、GPU、記憶體及廠商資訊。
- [系統支援狀態（others.yml）](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml)：目前記錄 Debian 和 Buildroot 狀態為 `wip`；狀態可能改變，請查看最新檔案。
- [RuyiSDK 第 075 期雙週報告](https://github.com/ruyisdk/wechat-articles/blob/main/20260901-ruyisdk-biweekly-75.md)：記錄 RuyiSDK 軟體源新增對知合 A210 SODIMM 官方 EVB 系統映像檔的相容支援。此報告不是映像檔下載頁；使用前請核對原始映像檔說明、開發板版本及校驗值。

### Linux 核心與驅動進展

以下是 RevyOS Linux 儲存庫中明確提及 A210 / Melon Pi 的變更，可用來追蹤裝置樹、驅動程式及板級支援。這些是特定開發提交，不代表所有發行版都已支援。

- [A210 平台維護項目及支援檔案範圍](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d)：列出 A210 裝置樹、繫結及驅動程式目錄。
- [A210 溫控與看門狗裝置樹](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4)。
- [PWM 驅動程式支援 A210](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d)：提交說明指出重用 TH1520 驅動程式。
- [Melon Pi V2 音訊走線](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146)。
- [RevyOS Linux 原始碼儲存庫](https://github.com/revyos/linux)：查看目前分支、裝置樹、驅動程式、提交及後續更新。
- [在 RevyOS Linux 中搜尋 A210 程式碼](https://github.com/revyos/linux/search?q=A210&type=code)：依目前儲存庫內容搜尋。
- [RVCK Linux 的 Melon Pi 裝置樹](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts)：板級 Linux 組態，不是完整硬體手冊。
- [RVCK Linux 的 A210 SoC 裝置樹](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi)及[知合裝置樹繫結](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml)：SoC 與相容字串的實作參考。
- [RVCK A210 周邊支援追蹤](https://github.com/RVCK-Project/rvck/issues/381)及[已合併的周邊支援變更](https://github.com/RVCK-Project/rvck/pull/382)：查看 GPIO、計時器、I²C、SPI、DMA 等支援討論與程式碼。該儲存庫屬於另一條 Linux 開發線，不能據此推論 RevyOS 或其他系統已包含相同支援。

## 開始使用前

1. 確認開發板的確切型號、版本及記憶體容量；相同 A210 SoC 不代表所有載板或版本都相同。
2. 先查看支援矩陣及映像檔發布說明，確認適用對象、狀態、開機媒介及校驗值。請勿直接燒錄其他 A210 開發板的映像檔。
3. 閱讀對應映像檔的原始安裝說明，並先備份現有資料。本文未驗證任何特定燒錄指令或映像檔。
4. 遇到裝置樹、驅動程式或開機問題時，請附上開發板版本、映像檔／核心版本、完整記錄及來源連結，再回報給相關專案。

## 資料範圍與貢獻

目前公開且可核驗的 A210 專屬資料，主要來自支援矩陣及 RevyOS Linux 開發記錄。尚未確認的官方產品手冊、原理圖、接腳表、下載網址及社群聯絡方式不在此猜測補寫。歡迎提交遺漏資料；請註明原始來源、適用硬體版本、查閱日期，並盡可能保留校驗和及授權資訊。
