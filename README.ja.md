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
- [SODIMM V1 書き込みガイド](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V1_Burning_Instruction) —— 4 冊あるボード別ガイドのうち最も古い世代で、V1 キャリアボード専用です
- [SODIMM V2 書き込みガイド](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V2_Burning_Instruction) —— 12V DC 給電、TTL 115200 デバッグポート、USB-A 書き込みポート。書き込みキーを押しながらリセットで USB モードへ。Windows は platform-tools r34.0.5 + usb_driver r13、Linux は android-sdk-platform-tools を使用します
- [SODIMM V3 書き込みガイド](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V3_Burning_Instruction)
- [計算スティック（Dongle）書き込みガイド](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_Dongle_Burning_Instruction) —— この形態は見落とされがちです

**ハードウェアプラットフォーム**

- [コアモジュールユーザーガイド](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/核心板说明) —— 主要パラメータ、寸法、260-pin ピン定義
- [SODIMM V2 キャリアボードユーザーガイド](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V2_baseboard_developer_guide) —— インターフェース、BOOT_SEL、PCIe RC/EP の切り替え、UART4 デバッグシリアル
- 残り二世代のキャリアボードユーザーガイド：[SODIMM V1](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V1_baseboard_developer_guide) · [SODIMM V3](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V3_baseboard_developer_guide)
- キャリアボード回路図（ボード別に 4 冊）：[SODIMM V1](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V1) · [SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V2) · [SODIMM V3](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V3) · [計算スティック](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Dongle)
- [ハードウェア設計ガイド](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/) —— 自社設計のキャリアボードを作る前に必読。本文は二冊構成です：[回路図設計の推奨事項](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/Schematic_Diagram_Design_Suggestions)（最小システム、24 MHz と 32.768 kHz のクロック、リセットとウォッチドッグ、BOOT_SEL と STRAP の上下プル、TEST_MODE/DEBUG_MODE の扱い）· [PCB 設計の推奨事項](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/PCB_Design_Recommendations)
- [PINMUX](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/A210-PINMUX) · **表を直接ダウンロード**：[A210-PINMUX_20260119.xlsx](https://developer.zhcomputing.com/zh/docs/pdf/A210/Hardware-Platform/A210-PINMUX_20260119.xlsx)（約 39 KB、実測でダウンロード可能）

**SDK**

- [SDK 概要](https://developer.zhcomputing.com/zh/docs/category/sdk) · [クイックスタート（イメージのダウンロード表あり）](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/Basic_quick_start_guide) · [マルチメディアクイックスタート](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/Multimedia_quick_start_guide) · [AI クイックスタート](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/AI_quick_start_guide)
- 開発環境：[Buildroot 開発ガイド](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/Buildroot_developer_guide) —— zdocker 環境から `./build.sh -b buildroot a210` まで；[BSP 開発ガイド](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/BSP_developer_guide) · [パーティション構成](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/分区介绍)
- マルチメディア：[MPI API リファレンス](https://developer.zhcomputing.com/zh/docs/SDK/多媒体/MPI_API_Reference/)
- [TORQ SDK の紹介](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ%20SDK%E4%BB%8B%E7%BB%8D) —— 12 TOPS NPU の入り口。TORQ-Toolkit と TORQ-LLM API を併用します。リファレンス：[TORQ-Toolkit Python API](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ-Toolkit%20API%E5%8F%82%E8%80%83) · [TORQ C API](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ%20C%20API%E5%8F%82%E8%80%83) · [TORQ-LLM C API](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ-LLM%20C%20API%E5%8F%82%E8%80%83) · [プラットフォーム演算子サポート一覧](https://developer.zhcomputing.com/zh/docs/SDK/AI/Platform_operators_support_list)
- その他のカテゴリ：[クイックスタート](https://developer.zhcomputing.com/zh/docs/category/快速上手) · [開発環境の構築](https://developer.zhcomputing.com/zh/docs/category/开发环境构建) · [マルチメディア](https://developer.zhcomputing.com/zh/docs/category/多媒体) · [AI](https://developer.zhcomputing.com/zh/docs/category/ai)

**ベンダーとボードメーカー**

- [XuanTie 公式サイト A210 製品ページ](https://www.xrvm.cn/product/board/4565261785988403200)（フロントエンドレンダリングのため本文は取得できません）
- [XuanTie 公式サイト ホーム](https://www.xrvm.cn/) · [XuanTie C920](https://www.xrvm.cn/product/xuantie/C920) · [C908](https://www.xrvm.cn/product/xuantie/C908)
- 知合計算のメインサイト [www.zhcomputing.com](http://www.zhcomputing.com/) —— 2026-11-08 に再確認：**http のみ**（`https://` は毎回 504 で証明書チェーンも不完全、直結・プロキシ経由とも同じ）。「Archimedes」シリーズのページは A200 / A300 のみ、ニュースセンターの最新記事は 2025-07 で止まっており、A210 のページはありません。英語版 `en.zhcomputing.com` は「サイト公開準備中」のプレースホルダーです —— A210 の公式資料は引き続き上記のドキュメントセンターが基準です。ビジネスに関するお問い合わせは business@zhcomputing.com まで。

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
- **公式アーティファクトリポジトリのディレクトリ索引**（ドキュメントの表より網羅的）：[downloads/release/](http://developer.zhcomputing.com/downloads/release/) —— `zhihesdk` 以下に v2.7.0 / v2.8.0 / v2.8.1 / v2.9.0、加えて `develop/` と `develop-test/` という開発スナップショットのディレクトリ（a210 イメージの最新は 2026-02-05 で v2.9.0 より古いので、新しい版と間違えないこと）、`npu` 以下に v1.3–v2.1（ovx-compiler、torq-llm、uca-nn、viplite）、`tools` 以下に 1.17 GB の `ubuntu-24.04-x86_64.v1.7.0.tar.gz` ビルドコンテナがあります
- **公式アーティファクトリポジトリは 2026-11-13 から全パスで 503 でしたが、2026-11-18 の再確認で復旧**：ディレクトリ索引も上の 4 本のイメージ直リンクも再び 200 を返し、`br2image-v2.9.0-a210_evb.tar.gz` は 188,113,587 バイト（179.4 MB）、`usb_driver_r13-windows.zip` は 8,682,039 バイトで、表に記したサイズと一致します。停止中は同じパスが 4.6 MB の JFrog Platform 読み込みページを返していました
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
- [[PATCH RFC v3 00/17] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-November/102729.html) —— 2026-11-02 の v3 です。v7.4-rc1 にリベースし、`arm_scmi` の ARM アーキテクチャ依存を外して RISC-V でもビルドできるようにしました。SCMI clock/reset ID は dt-bindings から DTS 隣のヘッダーへ移し、mailbox バインディングは固定の local / remote リージョンに変更しています。Melon Pi V2 では riscv defconfig で 8 コアを有効にしてシリアルシェルまで起動します。知合のファームウェアが SCMI をネイティブにサポートするのを待つため、まだ RFC のままです。なお、このバインディングでは V3 底板が V2 の compatible（`zhihe,a210-melonpi-v2`）をそのまま使うため、上流に v3 という板名はなく、V3 実機に V2 の DTB を使うのは想定どおりの動作です（このバインディングは Conor Dooley が ack）。 レビュー側は非 RFC 版待ちだけで、pinctrl の dt-binding とドライバの 2 本はいずれも Linus Walleij から LGTM を得ています（[102916](https://lists.infradead.org/pipermail/linux-riscv/2026-November/102916.html)）。Conor Dooley は SCMI と無関係な pinctrl をこのシリーズから切り出して単独で出すよう提案しています（[103213](https://lists.infradead.org/pipermail/linux-riscv/2026-November/103213.html)）。
- [[PATCH v4 00/13] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-November/104545.html) —— 2026-11-20 の v4 で、**RFC を外して通常のシリーズとして投稿**されました。知合がファームウェアで SCMI を使うことに合意したため、以前の留保は解消しています。v7.4-rc3 へ rebase し、レビュー指摘に従って分割——`arm_scmi` のアーキテクチャ依存は別投稿、`vendor-prefixes` と pin controller は独立シリーズ（pinctrl 側は確認済みで、`drivers/pinctrl/pinctrl-zhihe-a210.c` は [linux-next ツリー](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/tree/drivers/pinctrl/pinctrl-zhihe-a210.c) で読めます。一方 `Documentation/devicetree/bindings/riscv/zhihe.yaml` と mailbox ドライバーはまだ next に入っていません）——した結果、パッチは 18 本から **13 本**に減り、本シリーズは mailbox、UART とそのバインディング、DT、defconfig、MAINTAINERS のみになりました。Melon Pi V2 は riscv defconfig で 8 コアすべてオンラインのままシリアルシェルまで起動します。ボードのバインディング `zhihe,a210-melonpi-v1/v2` には引き続き `Acked-by: Conor Dooley` が付いています（v4 05/13）。2026-11-27 時点でメインライン未収録、patchwork ではこの 13 本がすべて `new` のままで、投稿後のレビュー返信はまだありません

**カーネルとデバイスツリー（各社の開発ライン上にあるもの）**

- [RVCK Linux](https://github.com/RVCK-Project/rvck) —— `rvck-6.6` ブランチのデバイスツリーが最も充実しています：[a210.dtsi](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi) · [a210-melon-pi.dts](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts) · [知合デバイスツリーバインディング](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml)。コミット検索では A210 関連のコミットが 56 件あり、GPIO/UART/timer/DMA/sdhci を含みます
- [RVCK：A210 周辺機器サポートの追跡 issue](https://github.com/RVCK-Project/rvck/issues/381) · [マージ済みの周辺機器サポート PR](https://github.com/RVCK-Project/rvck/pull/382)
- [RVCK：A210 USB サポート PR #437](https://github.com/RVCK-Project/rvck/pull/437) —— 2026-10-22 に作成、**2026-11-23 にマージ済み**です。2026-11-11 に **draft** へ変更されましたが、**11-18 に ready へ戻りました**。それ以前に更新された `rvck-6.6` へ rebase 済みで（20 パッチ、Melon Pi の 2 系統目 GMAC、UART pinctrl の修正、GPIO ranges、Zicbop block size、デバイスツリーの整理を追加）、同日 Icenowy が `a210.dtsi` にデバイスツリーの指摘を 3 点（reg が重複するノードは syscon に戻すか clk_usb から aux device を登録する、独立した 2 つの PHY はそれぞれ別ノードにする、`syscon` というプロパティ名にはベンダープレフィックスが必要）を出しました。11-13 の CI では check-patch、kunit、kernel-build、LAVA QEMU 起動と結果回収まで全工程が通過し、その後作者が @unicornx と Icenowy に公開でレビューを依頼、Icenowy が同日さらに 2 点を追加しました。`clk_usb` はノードを分割せず、レジスタ空間全体を 1 ノードで覆って clk ドライバから syscon を提供する形にする、2 つの USB2 PHY はそれぞれ別ノードにしてプルダウンを `zhihe,pulldown-mask` のような DT プロパティにする、DWC3 側の USB2 PHY は reg のないノードにするか glue に統合する、プロパティ名は `zhihe,usb-syscon` のように説明的な名前にする（`syscon` だけでは不可）という内容です。head コミットは現在 `4990a7ac` です。**2026-11-18 の収束**：作者は上記の指摘に沿って並べ直して rebase し、PR を draft から ready に戻しました。PR 本文には最終的な設計が明記されています——2 つの DWC2 PHY はそれぞれ独立したレジスタブロックを持ち、プルダウンは `zhihe,pulldown-mask` で記述する。DWC3 側の USB2 PHY は USB clock controller と MMIO を共有するため、clk ドライバが regmap を syscon に登録し、PHY は `zhihe,usb-syscon` phandle 経由で受け取る（clock ノードと重複する `reg` は書かない）。20 パッチ・24 ファイル +2296/−257 は変わらず、Icenowy が同日 LGTM を返し、CI 4 項目（check-patch、kunit、kernel-build、LAVA QEMU）もすべて通過、unicornx が QEMU/virt と Pioneerbox でビルドと起動を実測して通過しており、**11-23 に `rvck-6.6` へマージされました**（merge commit `f8351c85`）。マージ後は `a210.dtsi` に `zhihe,a210-dwc3-usb2-phy`（`zhihe,usb-syscon` 経由でレジスタを取得）と USB3 PHY ノードが入り、`a210-melon-pi.dts` には `usb2_0`/`usb2_1` の vbus 電源と `usb3` の Type-C ロールスイッチが入っています。中身は USB 2.0 の DWC2 コントローラ 2 個と PHY 3 個、USB 3.1 の DWC3 glue と USB3.1/DP combo PHY、Melon Pi 側の FUSB302 Type-C コントローラです。[PCIe と SATA 対応の issue #477](https://github.com/RVCK-Project/rvck/issues/477) も open のままです
- [RevyOS Linux](https://github.com/revyos/linux) —— デフォルトブランチ `revyos/7.3.y` は 11-21 以降 6 日連続で毎日まるごと書き換えられており、**現在の先頭は [`5146b3be65`](https://github.com/revyos/linux/commit/5146b3be65)（2026-11-26）**です。11-26 版でも A210 のパッチはデフォルトブランチに入っていますが、SHA はまたすべて入れ替わりました：[`FROMGIT: pinctrl: zhihe: add A210 support`](https://github.com/revyos/linux/commit/e406fddfea)（FROMGIT 表記、すでに pinctrl サブシステムツリーに入っている）、[`FROMLIST: mailbox: add Zhihe A210 AP to E902 mailbox driver`](https://github.com/revyos/linux/commit/389596931e)、[`FROMLIST: dt-bindings: riscv: add Melon Pi V1 and V2`](https://github.com/revyos/linux/commit/ea8db9b877)、[`FROMLIST: riscv: dts: zhihe: add Melon Pi V1 and V2`](https://github.com/revyos/linux/commit/3397bd2dab)（同じバッチに A210 core / UARTs / module memory のデバイスツリーパッチもあります）。メインラインはまだ未収録で、`drivers/pinctrl/zhihe` と `arch/riscv/boot/dts/zhihe` は torvalds/linux に存在しません（別シリーズとして切り出された pinctrl は linux-next に入っています。前の項目を参照）。defconfig は今回 2 つのコミットに分かれ、先に [`REVYOS: config: enable ARM SCMI support`](https://github.com/revyos/linux/commit/d8d23c2d37)（`ARM_SCMI_PROTOCOL=m`、`PINCTRL_SCMI=m`、`ARM_SCMI_CPUFREQ=m`）、次に [`REVYOS: config: enable Zhihe A210 support`](https://github.com/revyos/linux/commit/46829d1c67) です：`CONFIG_ARCH_ZHIHE`、`CONFIG_PINCTRL_ZHIHE_A210`、`CONFIG_ZHIHE_A210_MBOX` を有効にし、`ARM_SCMI_PROTOCOL` と `COMMON_CLK_SCMI` を `=m` から `=y` に引き上げ、さらに `ARM_SCMI_PERF_DOMAIN=m`、`ARM_SCMI_POWER_DOMAIN=m`、`RESET_SCMI=m` を追加しています。A210 のクロックとリセットはどちらも SCMI 経由なので、最初の 2 項目は組み込み必須です。今回の書き換えで以前記録した `62df2f69` と `96b82eb6` はデフォルトブランチから外れました（`62df2f69` は現在の先頭と diverged。11-24 に記録した `0e533424`、`d5ce9954`、`12dde5ea`、`ed2dc077`、`a774c69b95`、さらに 11-25 版の 4 本と `9e1b1ac150` も同様にデフォルトブランチから外れており、いずれも diverged です）。[A210 メンテナンス項目](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d) · [温度管理とウォッチドッグのデバイスツリー](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4) · [PWM ドライバー](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d) · [Melon Pi V2 のオーディオ配線](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146) の 4 件は依然として `rv/a210-upstream-local` ブランチのみにあります
- [RISE Project：riseproject-dev/linux](https://github.com/riseproject-dev/linux) —— `alibaba-a210` ブランチが存在します

**ブートとファームウェア**

- [riseproject-dev/u-boot](https://github.com/riseproject-dev/u-boot) —— `v2024.10-a210` ブランチ。ツリー内に `a210.dts`、`a210-soc.dtsi`、`board/zhihe/a200-evb` があります；[`fix/a210-sdhci-1v8-phy`](https://github.com/riseproject-dev/u-boot/tree/fix/a210-sdhci-1v8-phy) ブランチもあり、2026-11-17 のコミットで `zhihe_sdhci` が固定 1.8V の eMMC に適した PHY を選ぶようになります
- [riseproject-dev/opensbi](https://github.com/riseproject-dev/opensbi) —— `v1.5-a210` ブランチ。`platform/generic/zhihe/a210.c` を含みます
- [openeuler-riscv/opensbi-zhihe-a210](https://github.com/openeuler-riscv/opensbi-zhihe-a210) —— OpenSBI のベンダーポート
- [revyos/ruyiedk2](https://github.com/revyos/ruyiedk2) —— EDK2/UEFI プラットフォームファームウェア。README に Melon Pi V1 と V2 への対応が明記されており、`docs/melonpi.md` にネイティブ RAM ブートと USB Fastboot が記録されています
- [openeuler-riscv/bootloader-build · zhihe-a210](https://github.com/openeuler-riscv/bootloader-build/tree/master/zhihe-a210) —— openEuler RISC-V SIG によるビルド済み起動ファームウェアのディレクトリ：`binman-emmc_boot-loader.img`（eMMC の BOOT1 へ書き込み）、`bootzero-rvbl.bin` と `binman-spl-with-fit-rvbl.bin`（Fastboot 用の 2 段ペイロード）、さらに `a210-opensbi.dtb`。README には K1+K2 で Fastboot に入る手順、`fastboot flash ram` を 2 回実行してから `mmc0boot0` を書く順序、最後にシリアルで `env set fdtfile zhihe/a210-dev.dtb` と `env save` を実行する手順が載っています。openEuler 24.03 LTS の A210 イメージを焼くときはこの手順に従ってください
- SCMI ブートチェーン（`a210/scmi-v3` ブランチ、2026-11-02）：[coreboot](https://github.com/revyos/coreboot/tree/a210/scmi-v3) · [OpenSBI](https://github.com/revyos/opensbi/tree/a210/scmi-v3) · [EDK2](https://github.com/revyos/edk2/tree/a210/scmi-v3) · [RevySR/linux 残りの周辺機器を含む完全なツリー](https://github.com/RevySR/linux/tree/a210/scmi-v3) —— v3 RFC と対になる構成です。以前の `a210/scmi` ブランチも残っており、`revyos/ruyiedk2` にも `a210/scmi-v3` があります；v4 シリーズに対応するツリーは [RevySR/linux `a210/scmi-v4`](https://github.com/RevySR/linux/tree/a210/scmi-v4)（2026-11-18、SCMI Performance による CPU DVFS と残りの周辺機器を含む）で、ブートチェーン各リポジトリのブランチ名は変わっていません
- [RevySR/zephyr `xuantie/scmi-v3`](https://github.com/RevySR/zephyr/tree/xuantie/scmi-v3) —— E902 上で動く SCMI サーバーファームウェア（Zephyr）で、電源、PMIC、CPU DVFS のタイミングを担当します。もう 1 本の `xuantie/vcodec-v3`（2026-11-02）は VC9000D 用に VP クロック、リセット、電源ドメインを用意し、SCMI サーバー経由でビデオコーデックのリソースを AP に公開します
- [RevySR/linux `a210/vcodec-v3`](https://github.com/RevySR/linux/tree/a210/vcodec-v3) —— 2026-11-02 に追加されたビデオデコードの開発ラインです。hantro ドライバーに A210 の VC9000D デコーダー（VP9 対応）を追加し、対応するデバイスツリーノードも入れています
- RevySR/linux の A210 ブランチは SCMI だけではありません。[a210/bringup-v7.3](https://github.com/RevySR/linux/tree/a210/bringup-v7.3)（2026-10-22 の bring-up）、[a210/scmi-bootchain-v7.3](https://github.com/RevySR/linux/tree/a210/scmi-bootchain-v7.3)（10-27 の SCMI ブートチェーン）、[b4/a210-init](https://github.com/RevySR/linux/tree/b4/a210-init)（10-21 の最初のパッチ系列）の 3 本があり、検証したい範囲で選べます

**ディストリビューション層**

- [riscv/meta-riscv](https://github.com/riscv/meta-riscv) —— OpenEmbedded/Yocto の RISC-V レイヤー。マシン表に `zhihe-a210`（"Zhihe Computing Archimedes A210"）があり、`conf/machine/zhihe-a210.conf` は実際に存在します。2026-11-07 にマージされた [PR #744](https://github.com/riscv/meta-riscv/pull/744) で BSP カーネルの取得元が `riseproject-dev/linux` の `v7.2.12-a210` タグ（`a210_evb_defconfig`）に切り替わり、`test-zhihe-a210.yml`（クラウドビルド + OSU-OSL ボードファームでの TFTP ネットブート実測）が追加されました。2026-11-10 にマージされた [PR #748](https://github.com/riscv/meta-riscv/pull/748) が、このワークフローのトリガーパスの絞り込みを広げ `readlink -f` に切り替えました
- [git.osuosl.org/osuosl/zhihe-a210-kernel](https://git.osuosl.org/osuosl/zhihe-a210-kernel) —— オレゴン州立大学 OSU-OSL の A210 カーネルツリー（ブランチ 11 本：`osl/a210-mainline`、`osl/a210-6.6.x-lts`、版ごとのバックアップ）。タグ `v7.2.12-osl-a210`（2026-10-23、OpenSBI 用メモリ領域を `no-map` で予約）は meta-riscv の TFTP ネットブート手順が指定するカーネルそのもので、ほかに v2.9.0 / v2.8.1 / v2.8.0 / v2.7.0 とベンダ版 2.6.0-rc0 があります
- [openRuyi-BSP-RPM/zhihe-a210](https://git.openruyi.cn/openRuyi-BSP-RPM/zhihe-a210) —— openRuyi の A210 BSP RPM spec リポジトリ（コミット 4 件、最終 2026-08-21）。`firmware-zhihe-a210`、`linux-zhihe-a210-vendor-6.6`、`linux-zhihe-a210-vendor-6.6-rogue` の 3 パッケージで、同じグループに `rvck`、`spacemit-k1`、`spacemit-k3` もあります
- irradium 3.8 の `zhihe_a210` イメージ —— core と xfce の 2 種類で、**2026-11-21 に作り直されたロット**があります: core 6.6.0（1.55 GB）、core 7.2.15（1.64 GB）、xfce 6.6.0（2.88 GB）、加えて 09-21 ビルドの core 6.6.157（1.50 GB）が残っています: [ミラー先のディレクトリ](http://ubuntu-releases.acc.umu.se/mirror/irradium.org/images/zhihe_a210/)（公式 `dl.irradium.org` はこのツリーに 403 を返し、公式 boards ページにも A210 の記載がないため、コミュニティビルドとして扱ってください）。同じディレクトリの `kernel/` にはカーネル別に 3 セットのパッケージがあり、`kernel-a210#6.6.0` / `#6.6.157` / `#7.2.15` のそれぞれに kernel（387 MB / 371 MB / 505 MB）、kernel-firmware（各約 1.0 GB）、kernel-source（約 285 MB）が入っています。7.2.15 のセットは 11-21 に追加されたもので、カーネルを差し替えるのにディスク全体を焼き直す必要はありません。boot 用の tarball は依然として `boot-20260908.tar.xz` と `boot-20260921.tar.xz` のままです。README には A210 の fastboot によるブートローダ書き込みと u-boot 変数（`/EFI/irradium/grubriscv64.efi` と `/dtb/zhihe/a210-dev.dtb`）が載っています
- **FreeBSD の移植線（2026-10-30）**: [RevySR/freebsd-src `a210/bringup`](https://github.com/RevySR/freebsd-src/tree/a210/bringup) —— A210 における非 Linux 系の移植の試みで、FreeBSD main（土台は 10-29 のコミット）に **48 個のコミット**を積んでいます: `riscv: Add Zhihe A210 support` のほか、PCIe ホストコントローラのドライバと E16 PCIe/SATA PHY、`sdhci_zhihe` の HS400 ES、デュアルロールの dwc3 と dwc_otg の buffer DMA、ig4 の FDT 接続と tca64xx PMIC、eqos の修正、`clk: Add a GPIO gated clock driver`、さらに SCMI / mmio_sram / FDT AHCI の有効化。すべて 10-30 で止まっており、bring-up の段階で、上流にも入っておらず完成したイメージもありません
- **NixOS bring-up（サードパーティ、2026-11-20）**：[NixOS bring-up on an Alibaba RISC-V board](https://feyor.sh/blog/nixos-bringup-on-an-alibaba-riscv-board/) —— George Huebner が A210 を NixOS のビルドサーバに仕立てた記録で、現時点で最も詳しいサードパーティ製ディストリビューションの実録です。クロスコンパイルは `crossSystem.system = "riscv64-linux"` だけで済み、1000 を超えるパッケージで衝突したのは RISC-V 固有ではない 2 件だけ（`rust-bindgen` が誤った clang を選ぶ、`ministream` のクロス設定漏れ）、一方 Clang や GFortran のような重いパッケージはリンク時に 1 プロセスあたり 9 GB 超のメモリを使うため並列度を落として夜間に回しています。起動はベンダの U-Boot FSBL → OpenSBI → U-Boot SSBL → Linux という流れで、本当の罠は OpenSBI を `-march=rv64gv` でビルドした結果、`mstatus` のベクタコンテキストが無効なまま `vsetivli` を実行して不正命令トラップになった点で、`-march=generic` に変えて解決しています。カーネル起動後は `clk: Disabling unused clocks` で UART が止まるため `clk_ignore_unused` を追加（ベンダの cmdline も同じ）してユーザー空間へ到達。GPU は PowerVR BXM-4-64 で、上流の `drm/imagination` と Mesa が既に対応しており、6.18 のドライバをベンダの 6.6 カーネルへ移植してvkmark 2025.01 で 2445 を記録、HDMI、音声、Wi-Fi/Bluetooth、Ethernet も確認済みです。ほかに macOS が Fastboot モードの基板を認識しない、Black Magic Probe の `vRef` 浮きで UART 出力が消えるという 2 つの環境罠も書かれています
- [RevySR/rvck-image](https://github.com/RevySR/rvck-image) —— rootfs／ディスクイメージのビルド。README に「Melon Pi の EDK2 fastboot 経由で書き込む」手順があります（F9 で Fastboot、`flash emmc0`）
- [riseproject-dev/android_manifest](https://github.com/riseproject-dev/android_manifest) —— RISE Android 17 BSP。Alibaba A210 EVB を対象とし、lunch ターゲット `aosp_a210_evb-trunk_staging-userdebug` を記載しています。2026-10-14 の [android-17-v1.0 リリース](https://github.com/riseproject-dev/android_manifest/releases/tag/android-17-v1.0) はビルド済みの `rise-android-17-v1.0-a210-evb.tar.gz`（1.24 GB）と `SHA256SUMS` を公開し、同じタグに K3 Pico-ITX 版もあります。カーネルは android-mainline 7.1、グラフィックスは上流 `drm/imagination` と Mesa です。夜間ビルドのパイプラインは **2026-11-20 に全面的に書き直されました**（コミット `195084be`、`ci: publish nightly pre-releases and releases`）。`.github/scripts/release.py`（367 行）と `package-android.sh` を新設し、[nightly.yml](https://github.com/riseproject-dev/android_manifest/blob/android-17/.github/workflows/nightly.yml) は 258 行に書き直し（毎晩 01:23 UTC、固定 manifest が前回と変わったときだけビルド、K3 の次に a210、pre-release は直近 7 件を保持）、さらに `release.yml` と [release-tags.yml](https://github.com/riseproject-dev/android_manifest/blob/android-17/.github/workflows/release-tags.yml) を追加——後者は正式リリースの公開時に、そのコミットがブランチ上にあることを条件として、manifest に載る riseproject-dev の各リポジトリへ同名タグを打ちます。この書き直しで当時は旧夜間パッケージがすべて消え（`android-17-nightly-20261119` / `-20261120` / `-20261121` の 3 タグは一時すべて 404、[releases ページ](https://github.com/riseproject-dev/android_manifest/releases) に残るのは `android-17-v1.0` のみ）、書き直し後のパイプラインは **2026-11-21 に初めて完走**しました：08:22 UTC の nightly が成功し、11:46 に pre-release [android-17-nightly-20261121](https://github.com/riseproject-dev/android_manifest/releases/tag/android-17-nightly-20261121) を公開、`rise-android-17-nightly-20261121-a210-evb.tar.gz`（1.24 GB）と K3 Pico-ITX 版、各プロジェクトをビルド時のコミットに固定した `default.xml`、`SHA256SUMS` が付きます。`release-tags.yml` は夜間タグでは設計どおりスキップ。リリースノートにはハードウェア未検証と明記されています。引用するときはタグを固定せず、その時点の releases ページの最新版を見てください
- [riseproject-dev/android_kernel_device](https://github.com/riseproject-dev/android_kernel_device) —— 上記の Kleaf デバイスフラグメント（`alibaba/a210/`、`zhihe_a210.fragment`）
- [riseproject-dev/android_bootloader_build](https://github.com/riseproject-dev/android_bootloader_build) —— RISE のブートチェーン構築リポジトリ。`alibaba-android-17` ブランチが a210 用の U-Boot + OpenSBI を生成します（AVB 検証は無効、64 GB eMMC 向けの Android GPT レイアウト）
- [riseproject-dev/android_vendor_rise](https://github.com/riseproject-dev/android_vendor_rise) —— RISE のプリビルド起動チェーンとファームウェアのリポジトリ（`alibaba/a210/bootloader/`）。`u-boot.bin`、`spl-with-fit-rvbl.bin`、`bootzero-rvbl.bin`、`riscv-boot.itb`、`emmc-gpt_primary.img`、`a210.dtb` と RTL8822CS の Bluetooth ファームウェアを収め、CI が 3 時間ごとに上流の bootloader リポジトリから再ビルドします。A210 EVB 用の U-Boot + OpenSBI を自分でビルドせずに使いたいときに
- [BayLibre/android_device_alibaba_a210](https://github.com/BayLibre/android_device_alibaba_a210) —— BayLibre が保守する AOSP デバイスツリー（`android-17` ブランチ、`PRODUCT_SHIPPING_API_LEVEL` 37）。lunch ターゲットは同じ `aosp_a210_evb-trunk_staging-userdebug` ですが、`TARGET_ARCH_VARIANT := a210` です（C920 も C908 も Zvbb を持たないため riscv64 ベースラインではビルドできません）。U-Boot/OpenSBI とカーネルはプリビルドとしてツリーに置かれ、デバッグコンソールは `ttyS4` 115200。RTL8822CS の WiFi/Bluetooth、HDMI オーディオ、PowerVR の Vulkan 宣言、riscv64 WebView も入っています。上記 RISE のものとは独立した Android 17 ツリーです
- [BayLibre/android_device_alibaba_a210_kernel](https://github.com/BayLibre/android_device_alibaba_a210_kernel) —— そのデバイスツリー用のカーネルプリビルドリポジトリ。`mainline/` に `Image`、`a210-evb.dtb`、`System.map`、`vmlinux.symvers` と dlkm ディレクトリがあり、開発ブランチ `glaroque/a210-fixes` と `jmasson/a210-fixes-wifi-bt` もあります
- [RuyiSDK サポートマトリックス：A210 SODIMM V2](https://matrix.ruyisdk.org/zh-CN/boards/A210_SODIMM_V2/)（[ソースディレクトリ](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2) · [others.yml](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml)）—— Debian と Buildroot はいずれも `wip` と表示されています。`wip` は「作業中で未完成」の意味であり、使えるという意味ではありません
- [ruyisdk/ruyi](https://github.com/ruyisdk/ruyi) —— パッケージマネージャーで、**A210 のデバイスエントリがすでにあります**（`entities/device/zhihe-a210-sodimm.toml`、V2 / V3 の 2 つの variant 付き。[PR #208](https://github.com/ruyisdk/packages-index/pull/208) として 2026-08-27 にマージ）。ボードイメージのパッケージ `zhihe-br2image-a210-evb` と `zhihe-diskimage-a210-evb-debian` はいずれも **2.8.1** までしかなく（2.9.0 は未パッケージ）、`zhihe-a210-v1` の書き込みストラテジとパーティションマップが付いています。つまり ruyi はこのボードを認識し、パーティションテーブルどおりに 2.8.1 のイメージを書き込めますが、2.9.0 が必要なら公式の配布サーバーを使うことになります

---

## 6. GitHub プロジェクト一覧

A210 の GitHub エコシステムは薄く、4 つの系統に整理できます：**RVCK**（デバイスツリーが最も充実）、**RevyOS**（カーネルコミット + EDK2 ファームウェア）、**RISE Project**（U-Boot / OpenSBI / Android BSP）、**meta-riscv**（Yocto マシン）。GitHub に**知合計算の公式組織はありません**（`orgs/zhcomputing` は 404）。公式資料はすべてドキュメントサイトにあります。

第 5 節にすでに挙げたものは繰り返しません。その他は以下のとおりです：

- [kubuds/A210-Melon-Pi-all-in-one](https://github.com/kubuds/A210-Melon-Pi-all-in-one) —— 本インデックスのリポジトリ
- `ruyisdk/packages-index` の [PR #208](https://github.com/ruyisdk/packages-index/pull/208) —— ruyi 側の A210 デバイスと書き込みポリシー
- [riseproject-dev/developer-cloud](https://github.com/riseproject-dev/developer-cloud)（旧 `board-farm`、2026-11-11 に改名）—— RISE の RISC-V Developer Cloud 管理リポジトリ。Alibaba から寄贈された知合 A210 20 枚がオレゴン州立大学の OSU-OSL に置かれ、Phase 1 では Labgrid の `a210-yocto` プールを運用、ほかに Scaleway（フランス）と SOPIC（中国）の拠点があります。`boards/zhihe-a210/` の client/exporter 設定と pytest ケース、`.github/workflows/` 下の A210 向け 4 本のパイプライン（`a210_netboot.yml` の TFTP メモリブート a210-board-01〜05、`a210_labgrid_uboot.yml`、`yocto-zhihe-a210.yml`、2026-11-11 追加の `a210_telemetry.yml` 非破壊ハードウェアテレメトリ）があり、同時期に hub 側でボードタグの公開とタグ/検索フィルタ、ADB または UART による Android ボード自動判別、zhihe-a210 の UART エコーがカーネルバージョン判定を妨げる問題の修正が入りました；2026-11-13 には [PR #5](https://github.com/riseproject-dev/developer-cloud/pull/5)（**2026-11-20 にクローズ、未マージ**。`main` にこの 2 本はありません）が作られ、状態文書 2 本が追加されました。`docs/status/current_status.md` は OSU-OSL の A210 ボード群（`a210-1`〜`a210-5`）、Shelf 1 の `a210-s1-b01`〜`b10` の組み上げ進捗、Shelf 2 の BayLibre Copilot と Relay Hat DFU 設計、3 層の x86 ホスト構成（`osl-labgrid` と `proj-rise` の Chef cookbook）、`pool=a210-yocto` と `pool=a210-android` の 2 つの CI プールを記載し、`docs/status/2026_weekly_progress.md` は週単位の逆時系列の同期記録です；2026-11-14 には Yocto netboot テストを自作の pyserial シリアル解析と `===CI_PROBE_START===` センチネルから Labgrid 標準の UBootDriver + ShellDriver へ移行し、`ZhiheA210TftpBootStrategy`（`boards/zhihe-a210/strategy.py`、`helpers.py`、`client.yaml` で SerialDriver / UBootDriver / ShellDriver を接続し、テストは `test_uname_a` / `test_smp_cores` / `test_opensbi_reserved_memory` に集約）を追加しました。詳細は [コミット c7d058e](https://github.com/riseproject-dev/developer-cloud/commit/c7d058e8a6dd53a180c9fbd741d3032c460bc8be)（Google の Puneetha Ramachandra による）。2026-11-17 から 11-18 の一連のコミットで AOSP も Labgrid に接続されました：AOSP ハードウェア CI ワークフロー（`ci(a210-aosp)`、`runs-on` で Developer-Cloud-HW ランナーグループを明示）と Labgrid AOSP UDP fastboot 戦略を追加し、AOSP のテストは `/proc/mounts` を読んで起動を判定、カーネルバージョンの接頭辞一致を緩和、再起動前に必要ならステージ済みの `zhihe_wdt.ko` を読み込むよう変更、`SHA256SUMS` の解析は `./` 接頭辞に対応。hub 側では `serial_port` を `/dev/serial/by-path/` に固定し、シリアル探索で `u-boot#` プロンプトを認識。11-18 には USB-C ADB の Labgrid export・driver・スモークテストも追加（コミット `ef4e93e0`）。11-25 には AOSP の夜間書き込みが日常運用に組み込まれました：`fb5cdf5c` が夜間書き込みのスケジュール（新しい `android-17-nightly` が出たら毎日ハードウェア検証を実行）を追加し、書き込み時に bootloader と GPT パーティションには触れず、`fastboot continue` で復帰し、`vendor_boot` から `zhihe_wdt` が読み込まれていることを確認します。`0e2a09c1` は Android シェル起動後に `ttyS4` のカーネル printk を止め、root でウォッチドッグを読みます。`02450deb` は GKI カーネルで `CONFIG_WATCHDOG_SYSFS` が無効な場合に `zhihe-wdt` のプラットフォームバインドと `/dev/watchdog*` を確認します。`5d716bad` は `repository_dispatch` で `pool` と `expected_kernel_prefix`（既定 `7.1`）を渡せるようにしました。ボード受け入れポリシーも策定済みです：`boards/compliance-requirements.md` は [PR #2](https://github.com/riseproject-dev/developer-cloud/pull/2) で **2026-11-26 にマージ**され、[PR #3](https://github.com/riseproject-dev/developer-cloud/pull/3)（A210 のボード仕様・ソースミラー概要・受け入れチェックリスト）はまだ open です

---

## 7. Gitee プロジェクト

Gitee で A210 に直接対応するリポジトリはごく少数で、しかも **Gitee のサイト内検索 API は現在どのキーワードでも空を返します**。そのためこの節は**網羅を保証しません**：

- [agiros/yolov5_torq_camera](https://gitee.com/agiros/yolov5_torq_camera) —— 説明の原文は「主要用于 A210 单板，可以通过 torq 调用 yolov5 模型，并将识别的结果和画面发送为 AGIROS 话题」。なお README は Gitee のデフォルトテンプレートのままです
- [agiros/ur5-demo](https://gitee.com/agiros/ur5-demo) —— AGIROS の A210 ロボットアームのチュートリアルで `git clone` しているのがこのリポジトリです。A210 + openEuler 24.03 上で UR5 のビジュアル把持を行います。リポジトリ自体は A210 に言及しておらず、「A210 のプロジェクトで実際に使われている」という位置づけです

> 注意：「a210」で検索すると嘉楠 **K210** のプロジェクトが大量にヒットします。`gitee.com/zhihe` は「知和先生」という個人アカウントで、知合計算とは無関係です。

---

## 8. 動画

**Bilibili（サイト全体で 4 本のみ、うち Melon Pi という名前を含むのは 1 本だけです）**

- [知合 XuanTie A210 Melon Pi 開発ボード試用](https://www.bilibili.com/video/BV1wdx969Exj/) · donatello1996 · 2026-11-04 · 約 34 再生 —— 21 秒のドットマトリクス表示のクリップです。2 枚のパネルに温度・湿度・気圧の値とジェスチャー状態、さらに表情アニメーションが表示されますが、**ボード本体は一切映っていません**。A210 であると判断できるのはタイトルとタグ（RISC-V、XuanTie、開発ボード）だけです。Bilibili でタイトルに Melon Pi を含む最初の動画です
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
- [XuanTie A210 Melon Pi Field Report: I2C Worked, Everything Else Fought Back](https://open-riscv.com/forum/blog/xuantie-a210-melon-pi-field-report-gpio-spi-hdmi-uvc) —— 2026-11-05 の英語長文で、21ic の「ちょっと残念だった」試用記（同じ donatello1996、第 8 節の動画）を英語に整理したもの：2 か月の試用で使えたのは I2C（`/dev/i2c-7` に BME680 / QMC5883L / PAJ7620）と UART8 の 32 バイト固定長フレームだけで、HDMI（`modetest` が出力デバイスを見つけない）、GPIO（`gpiod` がエラー）、QSPI（`spidev` ノードなし）、USB UVC のキャプチャはすべて失敗し、最終的に早期返品；末尾で各症状を切り分け手順に対応づけ、これはチップ能力ではなく BSP の成熟度の問題だと述べています。署名は「RISC-V AI Assistant」で、機械支援による二次的な整理です
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
