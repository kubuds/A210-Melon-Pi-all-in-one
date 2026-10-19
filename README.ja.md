# Zhihe A210 / Melon Pi リソースガイド

[简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [English](README.en.md) · [Русский](README.ru.md) · [日本語](README.ja.md) · [Deutsch](README.de.md) · [Español](README.es.md)

このページでは、A210 開発ボードに関する公開情報のうち、出典を確認できるものをまとめています。仕様、OS イメージ、サポート状況は更新されるため、リンク先の一次情報を確認してください。継続的に追加する索引であり、インターネット上のすべての情報を網羅したという意味ではありません。

## ボード概要

[RuyiSDK ボードサポートマトリックス](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2)には **A210 SODIMM V2** が掲載され、次の情報が記載されています。

| 項目 | サポートマトリックスの記載 |
| --- | --- |
| メーカー | ZHIHE COMPUTING |
| SoC | A210 |
| CPU コア | XuanTie C920 + XuanTie C908 |
| GPU | IMG BXM-4-64 |
| メモリ構成 | 4 GB / 8 GB / 16 GB |

これらは該当するマトリックス項目の情報です。他のハードウェアリビジョンにも当てはまるとは限りません。実機の刻印とその版の資料を確認してください。

## ボード固有のリソース

### ハードウェア情報と OS の状況

- [RuyiSDK A210 SODIMM V2 サポートマトリックス](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2)：ボード情報とプロジェクトの状況。
- [ハードウェアとプロセッサ情報（README）](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/README.md)：プロセッサ、コア、GPU、メモリ、メーカー。
- [OS のサポート状況（others.yml）](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml)：現在、Debian と Buildroot は `wip` と記載されています。最新のファイルで状況を確認してください。
- [RuyiSDK 第 75 期隔週レポート](https://github.com/ruyisdk/wechat-articles/blob/main/20260901-ruyisdk-biweekly-75.md)：RuyiSDK パッケージリポジトリが Zhihe A210 SODIMM 公式 EVB システムイメージへの対応を追加したと記載しています。これは告知であり、イメージのダウンロードページではありません。使用前に元の説明、ボードの版、チェックサムを確認してください。

### Linux カーネルとドライバーの開発状況

以下は RevyOS Linux の変更のうち、A210 / Melon Pi に明示的に言及しているものです。デバイスツリー、ドライバー、ボードサポートの追跡に利用できます。個々の開発コミットは、すべてのディストリビューションでのサポートを意味しません。

- [A210 プラットフォームのメンテナンス情報と対象ファイル](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d)：A210 のデバイスツリー、バインディング、ドライバーのディレクトリを列挙。
- [A210 温度制御とウォッチドッグのデバイスツリー](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4)。
- [PWM ドライバーの A210 対応](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d)：コミット説明では TH1520 ドライバーを再利用するとされています。
- [Melon Pi V2 のオーディオ配線](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146)。
- [RevyOS Linux ソースリポジトリ](https://github.com/revyos/linux)：現在のブランチ、デバイスツリー、ドライバー、コミット、進行中の作業。
- [RevyOS Linux の A210 コード検索](https://github.com/revyos/linux/search?q=A210&type=code)：現在のリポジトリ内を検索。
- [RVCK Linux の Melon Pi デバイスツリー](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts)：ボード向け Linux 設定であり、完全なハードウェアマニュアルではありません。
- [RVCK Linux の A210 SoC デバイスツリー](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi)と[Zhihe デバイスツリーバインディング](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml)：SoC と compatible 文字列の実装資料。
- [RVCK の A210 周辺機器サポート issue](https://github.com/RVCK-Project/rvck/issues/381)と[マージ済みの周辺機器サポート変更](https://github.com/RVCK-Project/rvck/pull/382)：GPIO、タイマー、I²C、SPI、DMA などの議論とコードを参照できます。RVCK は別の Linux 開発系列です。RevyOS や他のシステムに同じサポートが含まれることを示すものではありません。

## 利用を始める前に

1. 正確なボード型番、ハードウェアリビジョン、メモリ容量を確認してください。同じ A210 SoC でも、キャリアボードやリビジョンが同一とは限りません。
2. サポートマトリックスとイメージ公開情報で対象ボード、サポート状況、起動メディア、チェックサムを確認してください。別の A210 ボード用イメージを確認せずに書き込まないでください。
3. 対象イメージの一次インストール手順に従い、既存データをバックアップしてください。このガイドでは特定の書き込みコマンドやイメージファイルを検証していません。
4. デバイスツリー、ドライバー、起動に関する問題を報告する際は、ボードの版、イメージ／カーネルのバージョン、完全なログ、参照リンクを添えてください。

## 対象範囲と貢献

現在確認できる A210 固有の公開資料は、主にサポートマトリックスと RevyOS Linux の開発履歴です。未確認の公式マニュアル、回路図、ピン配置、ダウンロード URL、コミュニティ連絡先は推測で掲載していません。資料の追加時は、一次情報、対象ハードウェアリビジョン、確認日、可能であればチェックサムとライセンス情報を記載してください。
