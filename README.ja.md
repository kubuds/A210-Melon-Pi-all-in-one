# 知合計算 A210 リソース総覧（SODIMM V2 / V3・計算スティック）

[简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [English](README.en.md) · [Русский](README.ru.md) · [日本語](README.ja.md) · [Deutsch](README.de.md) · [Español](README.es.md)

知合計算 A210（対外的には「阿基米德 A210」とも呼ばれます）について公開されているリソースをこの 1 ページに集めました。内容は、公式ドキュメントとデータシート、**そのままダウンロードできる公式イメージ**、ボード形状別の書き込みガイド、ハードウェア設計ファイル、アップストリームのカーネルとファームウェアの進捗、GitHub と Gitee のプロジェクト、そして実際にこのボードを使っている Bilibili と YouTube の動画です。

本ページはファームウェアやドキュメントの本体をミラーせず、出典へのリンクのみを載せています。**記録しているのはリンクと事実であり、利用を約束するものではありません** —— 書き込みの前に、ボードのリビジョン、イメージの説明、チェックサムを必ず確認してください。

> **まず名前を整理しましょう。このボードは一般的な開発ボードより呼び名が混乱しています。**
>
> - **チップ**：知合計算 A210、製品シリーズ名は「Archimedes」（阿基米德 A210）。汎用演算と推論を一体化したヘテロジニアス AI SoC です。
> - **ボード形態**：SODIMM コアモジュール + キャリアボード（**V1 / V2 / V3** の 3 世代）、さらに **A210 計算スティック（Dongle）** という形態があります。
> - **「Melon Pi / MelonPi」と呼んでいるのは誰か**：知合計算の公式ドキュメントとデータシートに**この名前はありません**（公式表記は「A210 SODIMM V1/V2/V3」のみ）。この名前は、アップストリーム Linux パッチのデバイスツリーファイル名（`a210-melonpi-v1.dts` / `-v2.dts`）、XuanTie の華秋オープンハードウェアページのタイトル（「玄鉄 MelonPi A210」）、一部の報道で使われています。Melon Pi と書かれていれば、同じボードのカーネル／コミュニティでの呼び名です。
> - **A200 と混同しないこと**：知合計算には A200 プラットフォームもあり、公式 Ubuntu イメージは A200 用のみです。A210 の公式イメージは Buildroot と Debian デスクトップの 2 種類だけです。

---

## 1. 主な仕様

| 項目 | 仕様 |
| --- | --- |
| SoC | 知合計算 A210（汎用演算と推論を一体化したヘテロジニアス AI SoC） |
| CPU | 4× Alibaba DAMO Academy XuanTie C920 + 4× XuanTie C908、RV64GCV（ベクトル拡張付き） |
| クロック | 公式データシートは 1.9 GHz、CNX Software の報道は C920 が最大 2.3 GHz、C908 が 1.9 GHz（両者で数値が一致していません。お手元のロットとデータシートを優先してください） |
| GPU | Vulkan 1.1/1.2/1.3、OpenCL 1.1/1.2/2.0、OpenGL ES 1.1/2.0/3.0/3.1/3.2 に対応（公式データシートに型番の記載はなく、「IMG BXM-4-64」は RuyiSDK サポートマトリックスのメタデータによるもの） |
| NPU | 12 TOPS@INT8、INT4/INT8/INT16/FP8/FP16/BF16 に対応 |
| メモリ | 4 / 8 / 16 GB 64-bit LPDDR4x、最大 4266 Mbps |
| ストレージ | eMMC 5.1/5.0、NOR/NAND Flash、SD 3.0 |
| ネットワーク | 10/100/1000 Mbps ギガビット Ethernet ×2 |
| ディスプレイ | HDMI 2.0 ×1、4-lane MIPI DSI ×1、DP / eDP（USB との多重化により制限あり） |
| カメラ | 4-lane ×1 + 2-lane ×1、または 2-lane MIPI CSI ×3 |
| 拡張 | PCIe x4 / x2 + x1、x2 + SATA ×2、x1 ×2 + SATA ×2。SPI ×2、QSPI ×1、I²C ×7、UART ×10、5ch PWM ×3、1ch ADC ×2 |
| USB | USB 3.1 ×1（DP Alt）、USB 2.0 ×2 |
| オーディオ | 2ch I2S/PCM ×3、TDM/PCM ×1 |
| 給電 / 温度 | コアモジュール 5V/5A（最小）、キャリアボード 12V DC 入力、-20 °C ~ 60 °C |
| コアモジュール寸法 | 59.66 mm × 69.94 mm、260-pin SODIMM |
| 公式 OS | Linux（Debian デスクトップ / Buildroot） |

**RVA23 については 2 つの説があります**：OMG! Ubuntu は 2025-07 の記事で、A210 が RVA23 の必須拡張と任意拡張をすべてサポートすると報じました。これに対して CNX Software は後日、コメント欄と本文で訂正し、A210 は RVA22 であり、RVA23 は次世代の A600 だとしています。**これについて権威ある結論はなく、選定の根拠にしないでください。**

データの出典：公式「A210 製品仕様書」と「コアモジュールユーザーガイド」、および[華秋オープンハードウェアコミュニティの製品ページ](https://p.eda.cn/d-1389550606774960128)（同じ仕様表の転載）。

---

## 2. 公式ドキュメント（知合計算 開発者ドキュメントセンター）

公式ドキュメントサイトは **developer.zhcomputing.com** で、現在は **2.9.0**、ほかに **2.8.1** の履歴版と `/en/` の英語版があります。このサイトはフロントエンドでレンダリングされるため `curl` では本文を取得できません。ブラウザで開いてください。

**総合入口**

- [ドキュメントセンター ホーム](https://developer.zhcomputing.com/zh/docs/intro) · [English](https://developer.zhcomputing.com/en/docs/intro/)
- [A210 ドキュメント目次](https://developer.zhcomputing.com/zh/docs/A210/) · [English](https://developer.zhcomputing.com/en/docs/A210/)
- [2.8.1 履歴版](https://developer.zhcomputing.com/zh/docs/2.8.1/category/sdk)

**データシートと書き込み（ボード形状別に分冊。間違えると書き込めません）**

- [A210 製品仕様書（HTML 全文）](https://developer.zhcomputing.com/zh/docs/A210/A210_Datasheet) —— 機能仕様、パッケージ、ピン定義、タイミング
- [イメージ書き込みガイド（索引）](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/)
- [SODIMM V2 書き込みガイド](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V2_Burning_Instruction) —— 12V DC 給電、TTL 115200 デバッグポート、USB-A 書き込みポート。書き込みキーを押しながらリセットで USB モードへ。Windows は platform-tools r34.0.5 + usb_driver r13、Linux は android-sdk-platform-tools を使用します
- [SODIMM V3 書き込みガイド](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V3_Burning_Instruction)
- [計算スティック（Dongle）書き込みガイド](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_Dongle_Burning_Instruction) —— この形態は見落とされがちです

**ハードウェアプラットフォーム**

- [コアモジュールユーザーガイド](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/核心板说明) —— 主要パラメータ、寸法、260-pin ピン定義
- [SODIMM V2 キャリアボードユーザーガイド](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V2_baseboard_developer_guide) —— インターフェース、BOOT_SEL、PCIe RC/EP の切り替え、UART4 デバッグシリアル
- [SODIMM V2 キャリアボード回路図](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V2)（V1/V3 と計算スティックにはそれぞれ独立したページがあります）
- [ハードウェア設計ガイド](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/) —— 自社設計のキャリアボードを作る前に必読
- [PINMUX](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/A210-PINMUX) · **表を直接ダウンロード**：[A210-PINMUX_20260119.xlsx](https://developer.zhcomputing.com/zh/docs/pdf/A210/Hardware-Platform/A210-PINMUX_20260119.xlsx)（約 39 KB、実測でダウンロード可能）

**SDK**

- [SDK 概要](https://developer.zhcomputing.com/zh/docs/category/sdk) · [クイックスタート（イメージのダウンロード表あり）](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/Basic_quick_start_guide)
- [Buildroot 開発ガイド](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/Buildroot_developer_guide) —— zdocker 環境から `./build.sh -b buildroot a210` まで
- [TORQ SDK の紹介](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ%20SDK%E4%BB%8B%E7%BB%8D) —— 12 TOPS NPU の入り口。TORQ-Toolkit と TORQ-LLM API を併用します
- その他のカテゴリ：[クイックスタート](https://developer.zhcomputing.com/zh/docs/category/快速上手) · [開発環境の構築](https://developer.zhcomputing.com/zh/docs/category/开发环境构建) · [マルチメディア](https://developer.zhcomputing.com/zh/docs/category/多媒体) · [AI](https://developer.zhcomputing.com/zh/docs/category/ai)

**ベンダーとボードメーカー**

- [XuanTie 公式サイト A210 製品ページ](https://www.xrvm.cn/product/board/4565261785988403200)（フロントエンドレンダリングのため本文は取得できません）
- [XuanTie 公式サイト ホーム](https://www.xrvm.cn/) · [XuanTie C920](https://www.xrvm.cn/product/xuantie/C920) · [C908](https://www.xrvm.cn/product/xuantie/C908)
- 知合計算のメインサイト `www.zhcomputing.com` は、直結・プロキシ経由とも実測で 504 です。現在使える唯一の公式サイトは上記のドキュメントセンターだけです。ビジネスに関するお問い合わせは business@zhcomputing.com まで。

> ドキュメントサイトのフッターにある「GitHub」リンクはプレースホルダー（`github.com/your-org` を指しています）で、実在のプロジェクトではありません。引用しないでください。

---

## 3. 公式イメージ（直接ダウンロード可能）

2 種類だけです：**Buildroot**（軽量）と **Debian デスクトップ**。いずれも `a210-evb` という名前で、fastboot のパーティションパッケージを使います。**公式 Ubuntu イメージはありません**（Ubuntu は A200 用のみ）。

| イメージ | バージョン | サイズ | ダウンロード |
| --- | --- | --- | --- |
| Buildroot プリビルドイメージ | v2.9.0（現行） | 179.4 MB | [br2image-v2.9.0-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/br2image-v2.9.0-a210_evb.tar.gz) |
| Debian デスクトップイメージ | v2.9.0（現行） | 738.4 MB | [diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz) |
| Buildroot プリビルドイメージ | v2.8.1（ロールバック用） | 175.9 MB | [br2image-v2.8.1-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/br2image-v2.8.1-a210_evb.tar.gz) |
| Debian デスクトップイメージ | v2.8.1（ロールバック用） | 734.8 MB | [diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz) |

- 展開すると `emmc-*.img`、`bootzero-rvbl.bin`、`fastboot_images.sh` / `.bat` が得られます。書き込みモードに入ってからスクリプトをそのまま実行してください
- **公式アーティファクトリポジトリのディレクトリ索引**（ドキュメントの表より網羅的）：[downloads/release/](http://developer.zhcomputing.com/downloads/release/) —— `zhihesdk` 以下に v2.7.0 / v2.8.0 / v2.8.1 / v2.9.0、`npu` 以下に v1.3–v2.1（ovx-compiler、torq-llm、uca-nn、viplite）、`tools` 以下に 1.17 GB の `ubuntu-24.04-x86_64.v1.7.0.tar.gz` ビルドコンテナがあります
- RuyiSDK でインストールを再現したい場合：[ruyisdk/packages-index PR #208](https://github.com/ruyisdk/packages-index/pull/208) が fastboot の手順、2.8.1 の Buildroot と Debian のイメージパッケージ、パーティションテーブルを ruyi のエントリにしており、パーティションマップとチェックサムが含まれているので突き合わせに使えます

---

## 4. ハードウェア設計ファイル（オープンソースキャリアボードの PDF と回路図）

[XuanTie MelonPi A210 高性能開発ボード —— SODIMM V3 オープンソースキャリアボード](https://p.eda.cn/d-1389550606774960128)（華秋オープンハードウェアコミュニティ、公開者 XuanTie 玄鉄、**OpenAtom OHL 1.0**）では以下が提供されています：

- **A210 SODIMM 底板原理图.zip**（2.69 MB）
- **A210 最小系统 原理图设计建议.pdf**（7.80 MB）
- **A210 最小系统 PCB 设计建议.pdf**（15.55 MB）
- **A210 产品规格书.pdf**（399 KB）—— 現在 **PDF 版**の仕様書を入手できる唯一の経路です（公式は HTML のみ）
- **A210-PINMUX_20260119.xlsx**（38.89 KB）

これは **V3 キャリアボード**であり、公式の V2 ドキュメントとは 1 世代分の差異がある点に注意してください。ダウンロードにはサイト内での登録とログインが必要です。

---

## 5. アップストリームのカーネル、ファームウェア、ディストリビューション

**アップストリーム Linux メインライン**

- [[PATCH 00/18] riscv: add initial support for Zhihe A210 and Melon Pi](https://lists.infradead.org/pipermail/linux-riscv/2026-October/101909.html) —— 初版のメインライン対応（UART/clock/reset/pinctrl + DT）。Melon Pi V2 上で 8 コアすべてを有効にして検証済みです。デバイスツリーファイル名 `a210-melonpi-v1.dts` / `-v2.dts` こそが「Melon Pi」という名前の本当の出所です
- [[PATCH RFC 00/18] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-October/102222.html) —— 2026-10-27 の作り直し版（作者の番号では v2）です。A210 には E902 管理コアも載っており、クロックとリセットのレジスタは実際にはそこで動く Zephyr の SCMI ファームウェアが管理しています。この版はネイティブの clk/reset ドライバーを削除して標準の SCMI clock/reset プロトコルに切り替え、AP→E902 のドアベル mailbox ドライバーを追加しました。Melon Pi V2 で 8 コアを有効にして UART シェルまで起動しています。ネイティブドライバーの版（上の項目）もこの版も、**2026-11-02 時点でもメインラインに入っていません**。最新の v3 は下の項目です
- [[PATCH RFC v3 00/17] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-November/102729.html) —— 2026-11-02 の v3 です。v7.4-rc1 にリベースし、`arm_scmi` の ARM アーキテクチャ依存を外して RISC-V でもビルドできるようにしました。SCMI clock/reset ID は dt-bindings から DTS 隣のヘッダーへ移し、mailbox バインディングは固定の local / remote リージョンに変更しています。Melon Pi V2 では riscv defconfig で 8 コアを有効にしてシリアルシェルまで起動します。知合のファームウェアが SCMI をネイティブにサポートするのを待つため、まだ RFC のままです

**カーネルとデバイスツリー（各社の開発ライン上にあるもの）**

- [RVCK Linux](https://github.com/RVCK-Project/rvck) —— `rvck-6.6` ブランチのデバイスツリーが最も充実しています：[a210.dtsi](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi) · [a210-melon-pi.dts](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts) · [知合デバイスツリーバインディング](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml)。コミット検索では A210 関連のコミットが 41 件あり、GPIO/UART/timer/DMA/sdhci を含みます
- [RVCK：A210 周辺機器サポートの追跡 issue](https://github.com/RVCK-Project/rvck/issues/381) · [マージ済みの周辺機器サポート PR](https://github.com/RVCK-Project/rvck/pull/382)
- [RevyOS Linux](https://github.com/revyos/linux) —— [A210 メンテナンス項目](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d) · [温度管理とウォッチドッグのデバイスツリー](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4) · [PWM ドライバー](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d) · [Melon Pi V2 のオーディオ配線](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146)。これらのコミットはデフォルトブランチにはありません
- [RISE Project：riseproject-dev/linux](https://github.com/riseproject-dev/linux) —— `alibaba-a210` ブランチが存在します

**ブートとファームウェア**

- [riseproject-dev/u-boot](https://github.com/riseproject-dev/u-boot) —— `v2024.10-a210` ブランチ。ツリー内に `a210.dts`、`a210-soc.dtsi`、`board/zhihe/a200-evb` があります
- [riseproject-dev/opensbi](https://github.com/riseproject-dev/opensbi) —— `v1.5-a210` ブランチ。`platform/generic/zhihe/a210.c` を含みます
- [openeuler-riscv/opensbi-zhihe-a210](https://github.com/openeuler-riscv/opensbi-zhihe-a210) —— OpenSBI のベンダーポート
- [revyos/ruyiedk2](https://github.com/revyos/ruyiedk2) —— EDK2/UEFI プラットフォームファームウェア。README に Melon Pi V1 と V2 への対応が明記されており、`docs/melonpi.md` にネイティブ RAM ブートと USB Fastboot が記録されています
- SCMI ブートチェーン（`a210/scmi-v3` ブランチ、2026-11-02）：[coreboot](https://github.com/revyos/coreboot/tree/a210/scmi-v3) · [OpenSBI](https://github.com/revyos/opensbi/tree/a210/scmi-v3) · [EDK2](https://github.com/revyos/edk2/tree/a210/scmi-v3) · [RevySR/linux 残りの周辺機器を含む完全なツリー](https://github.com/RevySR/linux/tree/a210/scmi-v3) —— v3 RFC と対になる構成です。以前の `a210/scmi` ブランチも残っており、`revyos/ruyiedk2` にも `a210/scmi-v3` があります
- [RevySR/zephyr `xuantie/scmi-v3`](https://github.com/RevySR/zephyr/tree/xuantie/scmi-v3) —— E902 上で動く SCMI サーバーファームウェア（Zephyr）で、電源、PMIC、CPU DVFS のタイミングを担当します。もう 1 本の `xuantie/vcodec-v3`（2026-11-02）は VC9000D 用に VP クロック、リセット、電源ドメインを用意し、SCMI サーバー経由でビデオコーデックのリソースを AP に公開します
- [RevySR/linux `a210/vcodec-v3`](https://github.com/RevySR/linux/tree/a210/vcodec-v3) —— 2026-11-02 に追加されたビデオデコードの開発ラインです。hantro ドライバーに A210 の VC9000D デコーダー（VP9 対応）を追加し、対応するデバイスツリーノードも入れています
- RevySR/linux の A210 ブランチは SCMI だけではありません。[a210/bringup-v7.3](https://github.com/RevySR/linux/tree/a210/bringup-v7.3)（2026-10-22 の bring-up）、[a210/scmi-bootchain-v7.3](https://github.com/RevySR/linux/tree/a210/scmi-bootchain-v7.3)（10-27 の SCMI ブートチェーン）、[b4/a210-init](https://github.com/RevySR/linux/tree/b4/a210-init)（10-21 の最初のパッチ系列）の 3 本があり、検証したい範囲で選べます

**ディストリビューション層**

- [riscv/meta-riscv](https://github.com/riscv/meta-riscv) —— OpenEmbedded/Yocto の RISC-V レイヤー。マシン表に `zhihe-a210`（"Zhihe Computing Archimedes A210"、OSU-OSL メインラインカーネル、TFTP netboot）があり、`conf/machine/zhihe-a210.conf` は実際に存在します
- [RevySR/rvck-image](https://github.com/RevySR/rvck-image) —— rootfs／ディスクイメージのビルド。README に「Melon Pi の EDK2 fastboot 経由で書き込む」手順があります（F9 で Fastboot、`flash emmc0`）
- [riseproject-dev/android_manifest](https://github.com/riseproject-dev/android_manifest) —— RISE Android 17 BSP。Alibaba A210 EVB を対象とし、lunch ターゲット `aosp_a210_evb-trunk_staging-userdebug` を記載しています
- [riseproject-dev/android_kernel_device](https://github.com/riseproject-dev/android_kernel_device) —— 上記の Kleaf デバイスフラグメント（`alibaba/a210/`、`zhihe_a210.fragment`）
- [RuyiSDK サポートマトリックス：A210 SODIMM V2](https://matrix.ruyisdk.org/zh-CN/boards/A210_SODIMM_V2/)（[ソースディレクトリ](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2) · [others.yml](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml)）—— Debian と Buildroot はいずれも `wip` と表示されています。`wip` は「作業中で未完成」の意味であり、使えるという意味ではありません
- [ruyisdk/ruyi](https://github.com/ruyisdk/ruyi) —— パッケージマネージャー。zhihe ベンダーの命名規則はありますが、**A210 専用のデバイスエントリはまだありません**。ruyi を入れたからといって A210 のイメージが手に入るわけではありません

---

## 6. GitHub プロジェクト一覧

A210 の GitHub エコシステムは薄く、4 つの系統に整理できます：**RVCK**（デバイスツリーが最も充実）、**RevyOS**（カーネルコミット + EDK2 ファームウェア）、**RISE Project**（U-Boot / OpenSBI / Android BSP）、**meta-riscv**（Yocto マシン）。GitHub に**知合計算の公式組織はありません**（`orgs/zhcomputing` は 404）。公式資料はすべてドキュメントサイトにあります。

第 5 節にすでに挙げたものは繰り返しません。その他は以下のとおりです：

- [kubuds/A210-Melon-Pi-all-in-one](https://github.com/kubuds/A210-Melon-Pi-all-in-one) —— 本インデックスのリポジトリ
- `ruyisdk/packages-index` の [PR #208](https://github.com/ruyisdk/packages-index/pull/208) —— ruyi 側の A210 デバイスと書き込みポリシー

---

## 7. Gitee プロジェクト

Gitee で A210 に直接対応するリポジトリはごく少数で、しかも **Gitee のサイト内検索 API は現在どのキーワードでも空を返します**。そのためこの節は**網羅を保証しません**：

- [agiros/yolov5_torq_camera](https://gitee.com/agiros/yolov5_torq_camera) —— 説明の原文は「主要用于 A210 单板，可以通过 torq 调用 yolov5 模型，并将识别的结果和画面发送为 AGIROS 话题」。なお README は Gitee のデフォルトテンプレートのままです
- [agiros/ur5-demo](https://gitee.com/agiros/ur5-demo) —— AGIROS の A210 ロボットアームのチュートリアルで `git clone` しているのがこのリポジトリです。A210 + openEuler 24.03 上で UR5 のビジュアル把持を行います。リポジトリ自体は A210 に言及しておらず、「A210 のプロジェクトで実際に使われている」という位置づけです

> 注意：「a210」で検索すると嘉楠 **K210** のプロジェクトが大量にヒットします。`gitee.com/zhihe` は「知和先生」という個人アカウントで、知合計算とは無関係です。

---

## 8. 動画

**Bilibili（サイト全体で 3 本のみ、しかも Melon Pi という名前を含むものは 1 本もありません）**

- [A210 x AGIROS による知能ロボットソリューション](https://www.bilibili.com/video/BV12KFKzkELG/) · AGIROS オープンソースコミュニティ · 2026-02-02 · 約 62 再生 —— AGIROS Meetup 北京站の Part5 で、登壇した申壮氏は知合計算技術（杭州）のシニア AI エンジニアです。**知合計算の現役エンジニアが A210 を語る唯一の動画**（14 分 10 秒）で、内容はソリューションの説明でありスコアの話ではありません
- [知合計算 Archimedes A210 RISC-V 開発ボード開梱 XuanTie C920 コア + NPU 通推一体](https://www.bilibili.com/video/BV1fJrnBsENd/) · DSOE1024 · 2026-01-14 · 約 1.7k 再生 —— **現在このボードを開梱する唯一の動画**（2 分 48 秒）
- [知合計算 A210 登場、「産学研」クローズドループの模範例、A600 の登場が近い](https://www.bilibili.com/video/BV19R84zsEVH/) · 石榴派-袁德俊 · 2025-07-26 · 428 再生 —— サミットの情報解説であり、ボードの実機検証ではありません

**YouTube（1 本のみ、しかも仕様の列挙 + 購入ガイド）**

- [Struggling with local AI projects? This RISC-V dev kit might help](https://www.youtube.com/watch?v=yK5x93THqLE) · 스마트직구연구소 —— 説明には Sipeed ZHIHE A210 RISC-V AI Dev Kit と明記されており、内容は仕様の列挙で実機検証はありません

**チュートリアルも、開発記録も、発表会の録画もありません**。知合計算は Bilibili にも YouTube にも公式アカウントを持っていません。これがこのボードの現状で、飾り立てはしません。

---

## 9. 中国語のチュートリアル、実践、報道

- [AGIROS + RISC-V 知合 A210 の全スタックを貫通させ実機で検証](https://ruyisdk.cn/t/topic/2362) —— **現在もっとも完成度の高い中国語の実践記事**：openEuler 24.03 LTS の書き込み（root パスワード `openEuler12#$` を含む）、ネットワークと静的 IP、AGIROS 25.12 のワンクリックインストール、ur5-moveit-demo、ハンドアイキャリブレーション、実機 UR5 での把持まで
- [知合計算 A210 開発ボード開梱（動画転載）](https://ruyisdk.cn/t/topic/2412) —— 短い投稿です。外観とインターフェースの配置を確認できます
- [XuanTie MelonPi A210 SODIMM V3 オープンソースキャリアボード](https://p.eda.cn/d-1389550606774960128) —— ハードウェア面で最も実用的な 1 本（22 個のインターフェース説明、BOOT_SEL、PCIe RC/EP、UART4 を含む）
- Alibaba Cloud 開発者コミュニティ [第 2 回 CIE 全国 RISC-V 高水準イノベーション・応用コンテストの課題説明](https://developer.aliyun.com/article/1749897) —— 課題 1「A210 エッジビジョン Agent アプリケーション」は、A210（12 TOPS NPU）と公式 Debian イメージを使い、画像取得 + 端末側 YOLOv5/v8 + クラウドの大規模モデルとの対話を実装することを明確に求めています。**A210 で練習用プロジェクトを探すなら、この課題に沿って作ればよいでしょう**
- Weibo の長文 [XuanTie・実践：生産ライン、ロボット、エッジ演算で「動かす」](https://weibo.com/ttarticle/x/m/geoshow/id/2309405355143666729355) —— 貴重な実測値：MobileNetV2 847 FPS、YOLOv8n 336 FPS、Qwen3-4B のローカル推論 19 token/s。ほかに AI NAS、16 系統 1080P エッジゲートウェイ、12 TOPS 計算スティック、A210 を 4 個相互接続した 48 TOPS PCIe カードなどの構成
- [知合計算、AICC2025 でお会いしましょう](https://mp.weixin.qq.com/s/e11WDCFZoI5CtObrTIFO5g) —— 公式アカウントで A210 に触れている唯一の記事ですが、内容はイベント告知のみで技術的な記述はありません

**英語の報道**

- CNX Software [Zhihe A210 octa-core RISC-V SoC with 12 TOPS NPU powers SoM-based development board](https://www.cnx-software.com/2026/06/17/zhihe-a210-octa-core-risc-v-soc-with-12-tops-npu-powers-som-based-development-board/) —— 最も完成度の高い英語報道
- CNX Software [Three high-performance RISC-V processors to watch in H2 2025](https://www.cnx-software.com/2025/07/22/three-high-performance-risc-v-processors-to-watch-in-h2-2025-ultrarisc-ur-dp1000-zizhe-a210-and-spacemit-k3/) —— A210 が初めて国際的に注目された記事
- OMG! Ubuntu [New RVA23 RISC-V chips are coming sooner than you think](https://www.omgubuntu.co.uk/2025/07/ubuntu-risc-v-rva23-hardware-coming-soon) —— RVA23 に関する記述が CNX の訂正と矛盾している点に注意してください（第 1 節参照）

> 取得できなかったもの：CSDN、知乎、`bbs.21ic.com`、`eefocus.com` は本機のネットワークでは 521 / 403 / キャプチャページが返り、本文を検証できないため 1 件も収録していません。`x-techcon.com` の AGIROS 記事はすでに 404 です（同じ内容は ruyisdk の記事にあります）。openEuler の A210 イメージパス `images.oerv.ac.cn/.../zhihe/a210-dev/` は実測で 404 でした。利用する場合は openEuler RISC-V SIG の公式チャネルで確認してください。

---

## 10. 購入先

- **苦芽科技（Kubuds）の Taobao 企業店**：https://item.taobao.com/item.htm?id=1034868327078&skuId=6052940225420 —— 商品詳細の表示には Taobao へのログインが必要です（リンク自体は 200 を返します）
- AliExpress の第三者（chipboard store）は「Sipeed ZHIHE A210」と表記し、8GB/64GB 構成で約 $334（ページはログイン画面に遷移するため、価格は参考程度に）
- 知合計算自身は公開の直販ページも見積ページも持っていません

---

## 11. 始める前に必ず確認すること

1. **ボード形状とリビジョンの確認**：SODIMM V1 / V2 / V3 か計算スティックか。キャリアボードが違えば、書き込みキーのタイミング、給電、インターフェースもすべて異なります。**書き込みガイドはボード形状別に分冊されています**。
2. **イメージは 2 種類だけ**（Buildroot / Debian デスクトップ）で、いずれも `a210-evb` という名前です。公式に Ubuntu はありません。ロールバックするなら 2.8.1 の 2 本を使ってください。
3. **V2 キャリアボードは 12V DC 給電**、コアモジュール自体は 5V/5A です。デバッグシリアルは **UART4** で 115200 です。
4. **キャリアボードの活線挿抜はしないでください**。作業前に静電気対策を行ってください。起動モードは BOOT_SEL のプルアップ／プルダウン抵抗で決まり、PCIe には RC/EP の切り替えがあります。
5. サポートマトリックスの `wip` は使えるという意味ではありません。デバイスツリーやドライバーの問題を報告する際は、ボード形状、イメージとカーネルのバージョン、完全なシリアルログを添えてください。

---

## 12. この索引の運用について

- 毎日 13:00 にウェブ全体の増分スキャンを自動実行します（公式アーティファクトリポジトリの新バージョン、ドキュメントサイトの新ページ、新しい動画、新しいリポジトリ）。変化があれば更新します
- **開ける**リンクだけを収録します。更新のたびに全リンクのチェックを実行し、リンク切れは削除するか新しいアドレスに差し替えます
- 動画は実際に A210 を撮影していることを条件とします。プロジェクトは、リポジトリに A210 のデバイスツリー、ブランチ、BSP が実際に存在すること（一言触れているだけでは不可）を条件とします
- 掲載は推奨を意味しません。公式イメージ以外のサードパーティビルド、ライセンス、メンテナンス状況はご自身で判断してください
- 抜けや誤りがあれば issue / PR を歓迎します。その際は元の出典、対象のボード形状、アクセス日を明記してください

[言語インデックスに戻る](README.md)
