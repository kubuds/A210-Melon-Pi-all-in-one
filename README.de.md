# Ressourcenübersicht für Zhihe A210 / Melon Pi

[简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [English](README.en.md) · [Русский](README.ru.md) · [日本語](README.ja.md) · [Deutsch](README.de.md) · [Español](README.es.md)

Diese Seite sammelt öffentlich zugängliche und überprüfbare Informationen zum A210-Entwicklungsboard. Für technische Daten, Systemabbilder und den Supportstatus sind die verlinkten Originalquellen maßgeblich; sie können sich ändern. Die Übersicht wird fortlaufend ergänzt und erhebt keinen Anspruch auf Vollständigkeit aller Internetquellen.

## Board-Übersicht

Die [RuyiSDK-Supportmatrix für Boards](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2) führt das **A210 SODIMM V2** mit folgenden Angaben:

| Merkmal | Angabe in der Supportmatrix |
| --- | --- |
| Hersteller | ZHIHE COMPUTING |
| SoC | A210 |
| CPU-Kerne | XuanTie C920 + XuanTie C908 |
| GPU | IMG BXM-4-64 |
| Speicherkonfigurationen | 4 GB / 8 GB / 16 GB |

Diese Angaben stammen aus genau diesem Matrixeintrag und gelten nicht zwangsläufig für andere Hardware-Revisionen. Maßgeblich sind die Beschriftung und Dokumentation des konkreten Boards.

## Board-spezifische Ressourcen

### Hardware und Betriebssystemstatus

- [RuyiSDK-Supportmatrix für A210 SODIMM V2](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2): Boardeintrag und Projektstatus.
- [Hardware- und Prozessorangaben (README)](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/README.md): Prozessor, Kerne, GPU, Speicher und Hersteller.
- [Betriebssystemstatus (others.yml)](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml): Debian und Buildroot sind derzeit als `wip` markiert. Den aktuellen Stand bitte in der Datei prüfen.
- [RuyiSDK-Zweiwochenbericht Nr. 75](https://github.com/ruyisdk/wechat-articles/blob/main/20260901-ruyisdk-biweekly-75.md): berichtet, dass das RuyiSDK-Paketrepository Kompatibilität mit dem offiziellen Zhihe-A210-SODIMM-EVB-Systemabbild ergänzt hat. Dies ist eine Ankündigung, keine Downloadseite. Vor der Nutzung Originalhinweise, Board-Revision und Prüfsumme prüfen.

### Linux-Kernel- und Treiberentwicklung

Die folgenden Änderungen im RevyOS-Linux-Repository nennen A210 / Melon Pi ausdrücklich und helfen dabei, Gerätebaum-, Treiber- und Board-Support nachzuverfolgen. Einzelne Entwicklungseinträge bedeuten nicht, dass jede Distribution das Board unterstützt.

- [A210-Plattformbetreuung und unterstützte Dateibereiche](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d): listet A210-Gerätebäume, Bindings und Treiberverzeichnisse.
- [Gerätebaum für Temperaturregelung und Watchdog des A210](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4).
- [PWM-Treiberunterstützung für A210](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d): Laut Commit-Beschreibung wird der TH1520-Treiber wiederverwendet.
- [Audio-Routing des Melon Pi V2](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146).
- [RevyOS-Linux-Quellcode](https://github.com/revyos/linux): aktueller Branch, Gerätebäume, Treiber, Commits und laufende Arbeiten.
- [A210-Code in RevyOS Linux suchen](https://github.com/revyos/linux/search?q=A210&type=code): Suche im aktuellen Repository.
- [Melon-Pi-Gerätebaum in RVCK Linux](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts): Linux-Konfiguration für das Board, kein vollständiges Hardwarehandbuch.
- [A210-SoC-Gerätebaum in RVCK Linux](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi) und [Zhihe-Gerätebaum-Binding](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml): Implementierungsreferenzen für SoC und Compatible-Strings.
- [RVCK-Issue zur A210-Peripherieunterstützung](https://github.com/RVCK-Project/rvck/issues/381) und [zusammengeführte Änderung zur Peripherieunterstützung](https://github.com/RVCK-Project/rvck/pull/382): Diskussion und Code zu GPIO, Timern, I²C, SPI, DMA und weiteren Geräten. RVCK ist eine separate Linux-Entwicklungslinie; daraus folgt nicht, dass RevyOS oder andere Systeme dieselbe Unterstützung enthalten.

## Vor dem ersten Start

1. Exaktes Boardmodell, Hardware-Revision und Speichergröße feststellen. Derselbe A210-SoC bedeutet nicht, dass Trägerplatinen oder Revisionen identisch sind.
2. Supportmatrix und Image-Ankündigung auf Zielboard, Status, Startmedium und Prüfsumme prüfen. Kein Abbild für ein anderes A210-Board ungeprüft flashen.
3. Die Original-Installationsanleitung des jeweiligen Abbilds befolgen und vorhandene Daten sichern. Diese Übersicht bestätigt keine konkreten Flash-Befehle oder Image-Dateien.
4. Bei Problemen mit Gerätebaum, Treibern oder Startvorgang Board-Revision, Image-/Kernel-Version, vollständige Protokolle und Quellen angeben.

## Umfang und Beiträge

Die derzeit überprüfbaren, A210-spezifischen öffentlichen Informationen finden sich hauptsächlich in der Supportmatrix und in der Entwicklungshistorie von RevyOS Linux. Nicht bestätigte Produkthandbücher, Schaltpläne, Pinbelegungen, Download-URLs und Community-Kontakte werden nicht spekulativ ergänzt. Beiträge sind willkommen; bitte Originalquelle, passende Hardware-Revision, Prüfdatum sowie nach Möglichkeit Prüfsummen und Lizenzangaben nennen.
