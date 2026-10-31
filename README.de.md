# Zhihe A210 Ressourcenübersicht (SODIMM V2 / V3 · Compute-Stick)

[简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [English](README.en.md) · [Русский](README.ru.md) · [日本語](README.ja.md) · [Deutsch](README.de.md) · [Español](README.es.md)

Alles, was sich zum Zhihe Computing A210 (auch als „Archimedes A210" vermarktet) öffentlich finden lässt, ist auf dieser Seite gesammelt: offizielle Dokumentation und Datenblatt, **direkt herunterladbare offizielle Images**, Flash-Anleitungen je Boardvariante, Hardware-Design-Dateien, Fortschritte bei Upstream-Kernel und Firmware, GitHub- und Gitee-Projekte sowie die Bilibili- und YouTube-Videos, die dieses Board tatsächlich zeigen.

Diese Seite spiegelt keine Firmware und keine Dokumente, sie nennt nur die Quelle. **Festgehalten werden Links und Fakten, keine Zusagen** – prüfe vor dem Flashen Board-Revision, Image-Hinweise und Prüfsummen.

> **Erst die Namen sortieren – dieses Board hat mehr Bezeichnungen als üblich.**
>
> - **Chip**: Zhihe Computing A210, Produktfamilie „Archimedes" (Archimedes A210), ein heterogener AI-SoC, der Allzweckrechnung und Inferenz in einem Chip vereint.
> - **Bauformen**: SODIMM-Compute-Modul plus Trägerplatine (**V1 / V2 / V3**, drei Generationen von Trägerplatinen), daneben die Form **A210 Compute-Stick (Dongle)**.
> - **Wer „Melon Pi / MelonPi" sagt**: In der offiziellen Dokumentation und im Datenblatt von Zhihe steht dieser Name **nicht** (offiziell nur „A210 SODIMM V1/V2/V3"); er taucht in den Device-Tree-Dateinamen der Upstream-Linux-Patches auf (`a210-melonpi-v1.dts` / `-v2.dts`), im Titel der XuanTie-Seite im Open-Hardware-Bereich von Huaqiu („XuanTie MelonPi A210") und in einigen Medienberichten. Wer „Melon Pi" liest, meint dasselbe Board unter seinem Kernel- und Community-Namen.
> - **Nicht mit dem A200 verwechseln**: Zhihe hat auch eine A200-Plattform, und die offiziellen Ubuntu-Images gibt es nur für den A200; für den A210 liefert Zhihe offiziell nur zwei Images, Buildroot und Debian Desktop.

---

## 1. Technische Daten

| Punkt | Spezifikation |
| --- | --- |
| SoC | Zhihe Computing A210 (heterogener AI-SoC für Allzweck- und Inferenzrechnung) |
| CPU | 4× XuanTie C920 + 4× XuanTie C908 (DAMO Academy), RV64GCV (mit Vektorerweiterung) |
| Takt | Im offiziellen Datenblatt 1.9 GHz; CNX Software nennt für den C920 bis zu 2.3 GHz und für den C908 1.9 GHz (die beiden Angaben widersprechen sich, maßgeblich sind deine Charge und das Datenblatt) |
| GPU | Vulkan 1.1/1.2/1.3, OpenCL 1.1/1.2/2.0, OpenGL ES 1.1/2.0/3.0/3.1/3.2 (das Datenblatt nennt kein Modell; „IMG BXM-4-64" stammt aus den Metadaten der RuyiSDK-Support-Matrix) |
| NPU | 12 TOPS@INT8, unterstützt INT4/INT8/INT16/FP8/FP16/BF16 |
| Arbeitsspeicher | 4 / 8 / 16 GB 64-Bit LPDDR4x, bis zu 4266 Mbps |
| Speicher | eMMC 5.1/5.0, NOR/NAND-Flash, SD 3.0 |
| Netzwerk | 2× 10/100/1000 Mbps Gigabit-Ethernet |
| Display | 1× HDMI 2.0, 1× 4-Lane-MIPI-DSI, DP / eDP (eingeschränkt durch USB-Multiplexing) |
| Kamera | 1× 4-Lane + 1× 2-Lane oder 3× 2-Lane MIPI CSI |
| Erweiterung | PCIe x4 / x2 + x1, x2 + 2× SATA, 2× x1 + 2× SATA; 2× SPI, 1× QSPI, 7× I²C, 10× UART, 3× 5ch-PWM, 2× 1ch-ADC |
| USB | 1× USB 3.1 (DP Alt), 2× USB 2.0 |
| Audio | 3× 2ch-I2S/PCM, 1× TDM/PCM |
| Stromversorgung / Temperatur | Modul 5V/5A (Minimum); Trägerplatine 12V-DC-Eingang; −20 °C bis 60 °C |
| Modulabmessungen | 59.66 mm × 69.94 mm, 260-Pin-SODIMM |
| Offizielles OS | Linux (Debian Desktop / Buildroot) |

**Zu RVA23 gibt es zwei Aussagen**: OMG! Ubuntu berichtete im Juli 2025, der A210 unterstütze alle verpflichtenden und optionalen RVA23-Erweiterungen; CNX Software hat das später in den Kommentaren und im Text korrigiert und ordnet den A210 als RVA22 ein, RVA23 sei der A600 der nächsten Generation. **Dazu gibt es kein belastbares Ergebnis – nutze es nicht als Grundlage für eine Auswahlentscheidung.**

Quellen: das offizielle „A210-Produktdatenblatt" und das „Benutzerhandbuch für das Compute-Modul", außerdem die [Produktseite in der Huaqiu-Open-Hardware-Community](https://p.eda.cn/d-1389550606774960128) (eine Wiedergabe derselben Spezifikationstabellen).

---

## 2. Offizielle Dokumentation (Dokumentationszentrum für Entwickler von Zhihe Computing)

Die offizielle Doku-Seite ist **developer.zhcomputing.com**, aktuell **2.9.0**, daneben die ältere Version **2.8.1** und eine englische Ausgabe unter `/en/`. Die Seite wird clientseitig gerendert, `curl` bekommt keinen Text – bitte im Browser öffnen.

**Einstieg**

- [Startseite der Dokumentation](https://developer.zhcomputing.com/zh/docs/intro) · [English](https://developer.zhcomputing.com/en/docs/intro/)
- [A210-Dokumentationsverzeichnis](https://developer.zhcomputing.com/zh/docs/A210/) · [English](https://developer.zhcomputing.com/en/docs/A210/)
- [Ältere Version 2.8.1](https://developer.zhcomputing.com/zh/docs/2.8.1/category/sdk)

**Datenblatt und Flashen (nach Boardvariante getrennt, mit der falschen Anleitung schlägt das Flashen fehl)**

- [A210-Produktdatenblatt (vollständiger HTML-Text)](https://developer.zhcomputing.com/zh/docs/A210/A210_Datasheet) – Funktionsmerkmale, Gehäuse, Pinbelegung und Timing
- [Anleitung zum Flashen von Images (Übersicht)](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/)
- [Flash-Anleitung SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V2_Burning_Instruction) – 12V-DC-Versorgung, TTL-Debug-Port mit 115200, USB-A-Flash-Port; Flash-Taste gedrückt halten und Reset auslösen, um in den USB-Modus zu gelangen; unter Windows platform-tools r34.0.5 + usb_driver r13, unter Linux android-sdk-platform-tools
- [Flash-Anleitung SODIMM V3](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V3_Burning_Instruction)
- [Flash-Anleitung Compute-Stick (Dongle)](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_Dongle_Burning_Instruction) – diese Bauform wird leicht übersehen

**Hardware-Plattform**

- [Benutzerhandbuch Compute-Modul](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/核心板说明) – zentrale Parameter, Abmessungen, 260-Pin-Pinbelegung
- [Benutzerhandbuch Trägerplatine SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V2_baseboard_developer_guide) – Schnittstellen, BOOT_SEL, PCIe-Umschaltung RC/EP, UART4 als Debug-Seriellenport
- [Schaltplan der Trägerplatine SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V2) (V1/V3 und der Compute-Stick haben jeweils eigene Seiten)
- [Hardware-Design-Leitfaden](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/) – Pflichtlektüre, bevor du eine eigene Trägerplatine entwickelst
- [PINMUX](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/A210-PINMUX) · **Tabelle direkt herunterladen**: [A210-PINMUX_20260119.xlsx](https://developer.zhcomputing.com/zh/docs/pdf/A210/Hardware-Platform/A210-PINMUX_20260119.xlsx) (ca. 39 KB, Download getestet)

**SDK**

- [SDK-Übersicht](https://developer.zhcomputing.com/zh/docs/category/sdk) · [Schnellstart (mit Tabelle der Images zum Herunterladen)](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/Basic_quick_start_guide)
- [Buildroot-Entwicklungsleitfaden](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/Buildroot_developer_guide) – von der zdocker-Umgebung bis `./build.sh -b buildroot a210`
- [Einführung in das TORQ SDK](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ%20SDK%E4%BB%8B%E7%BB%8D) – der Einstieg in die 12-TOPS-NPU, mit TORQ-Toolkit und TORQ-LLM-API
- Weitere Kategorien: [Schnellstart](https://developer.zhcomputing.com/zh/docs/category/快速上手) · [Build-Umgebung](https://developer.zhcomputing.com/zh/docs/category/开发环境构建) · [Multimedia](https://developer.zhcomputing.com/zh/docs/category/多媒体) · [AI](https://developer.zhcomputing.com/zh/docs/category/ai)

**Hersteller- und IP-Seite**

- [XuanTie-Produktseite zum A210](https://www.xrvm.cn/product/board/4565261785988403200) (clientseitig gerendert, kein Text abrufbar)
- [XuanTie-Startseite](https://www.xrvm.cn/) · [XuanTie C920](https://www.xrvm.cn/product/xuantie/C920) · [C908](https://www.xrvm.cn/product/xuantie/C908)
- Die Hauptseite von Zhihe, `www.zhcomputing.com`, liefert sowohl direkt als auch über einen Proxy 504; die einzige derzeit nutzbare offizielle Website ist das oben genannte Dokumentationszentrum. Geschäftskontakt: business@zhcomputing.com

> Der „GitHub"-Link in der Fußzeile der Doku-Seite ist ein Platzhalter (zeigt auf `github.com/your-org`), kein echtes Projekt – bitte nicht zitieren.

---

## 3. Offizielle Images (direkt herunterladbar)

Es gibt nur zwei: **Buildroot** (leicht) und **Debian Desktop**, beide einheitlich als `a210-evb` benannt, beide als Fastboot-Partitionspaket. **Ein offizielles Ubuntu-Image gibt es nicht** (Ubuntu wird nur für den A200 angeboten).

| Image | Version | Größe | Download |
| --- | --- | --- | --- |
| Buildroot vorkompiliert | v2.9.0 (aktuell) | 179.4 MB | [br2image-v2.9.0-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/br2image-v2.9.0-a210_evb.tar.gz) |
| Debian-Desktop-Image | v2.9.0 (aktuell) | 738.4 MB | [diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz) |
| Buildroot vorkompiliert | v2.8.1 (für Rollback) | 175.9 MB | [br2image-v2.8.1-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/br2image-v2.8.1-a210_evb.tar.gz) |
| Debian-Desktop-Image | v2.8.1 (für Rollback) | 734.8 MB | [diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz) |

- Nach dem Entpacken erhältst du `emmc-*.img`, `bootzero-rvbl.bin` und `fastboot_images.sh` / `.bat`; sobald das Board im Flash-Modus ist, das Skript direkt ausführen
- **Verzeichnisindex des offiziellen Artefakt-Repositories** (vollständiger als die Tabelle in der Doku): [downloads/release/](http://developer.zhcomputing.com/downloads/release/) – unter `zhihesdk` liegen v2.7.0 / v2.8.0 / v2.8.1 / v2.9.0, unter `npu` v1.3–v2.1 (ovx-compiler, torq-llm, uca-nn, viplite), unter `tools` ein 1.17 GB großes Build-Container-Image `ubuntu-24.04-x86_64.v1.7.0.tar.gz`
- Wer die Installation mit dem RuyiSDK nachvollziehen will: [ruyisdk/packages-index PR #208](https://github.com/ruyisdk/packages-index/pull/208) hat den Fastboot-Ablauf, die Buildroot- und Debian-Image-Pakete aus 2.8.1 und die Partitionstabelle als ruyi-Einträge umgesetzt, inklusive Partitionszuordnung und Prüfsummen zum Gegenprüfen

---

## 4. Hardware-Design-Dateien (Open-Source-Trägerplatine als PDF und Schaltplan)

[Open-Source-Trägerplatine für das XuanTie MelonPi A210 – SODIMM V3](https://p.eda.cn/d-1389550606774960128) (Huaqiu-Open-Hardware-Community, veröffentlicht von XuanTie, **OpenAtom OHL 1.0**) bietet:

- **A210 SODIMM 底板原理图.zip** (2.69 MB)
- **A210 最小系统 原理图设计建议.pdf** (7.80 MB)
- **A210 最小系统 PCB 设计建议.pdf** (15.55 MB)
- **A210 产品规格书.pdf** (399 KB) – derzeit der einzige Weg zu einem Datenblatt als **PDF** (offiziell gibt es nur HTML)
- **A210-PINMUX_20260119.xlsx** (38.89 KB)

Achtung: Das ist die **V3-Trägerplatine**, also eine Generation entfernt von der offiziellen V2-Dokumentation. Für den Download ist ein Konto auf der Seite nötig.

---

## 5. Upstream-Kernel, Firmware und Distributionen

**Upstream-Linux-Mainline**

- [[PATCH 00/18] riscv: add initial support for Zhihe A210 and Melon Pi](https://lists.infradead.org/pipermail/linux-riscv/2026-October/101909.html) – die erste Mainline-Unterstützung (UART/Clock/Reset/Pinctrl + DT), auf dem Melon Pi V2 mit allen 8 Kernen validiert; die Device-Tree-Dateinamen `a210-melonpi-v1.dts` / `-v2.dts` sind der eigentliche Ursprung des Namens „Melon Pi"

**Kernel und Device Trees (noch in den Entwicklungszweigen der Anbieter)**

- [RVCK Linux](https://github.com/RVCK-Project/rvck) – im Branch `rvck-6.6` sind die Device Trees am vollständigsten: [a210.dtsi](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi) · [a210-melon-pi.dts](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts) · [Device-Tree-Binding für Zhihe](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml); die Commit-Suche findet 41 A210-bezogene Commits, darunter GPIO/UART/timer/DMA/sdhci
- [RVCK: Issue zur Peripheral-Unterstützung des A210](https://github.com/RVCK-Project/rvck/issues/381) · [gemergter PR zur Peripheral-Unterstützung](https://github.com/RVCK-Project/rvck/pull/382)
- [RevyOS Linux](https://github.com/revyos/linux) – [A210-Maintainer-Eintrag](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d) · [Device Tree für Temperaturregelung und Watchdog](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4) · [PWM-Treiber](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d) · [Audio-Routing auf dem Melon Pi V2](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146). Achtung: Diese Commits liegen nicht auf dem Standard-Branch
- [RISE Project: riseproject-dev/linux](https://github.com/riseproject-dev/linux) – ein Branch `alibaba-a210` ist vorhanden

**Boot und Firmware**

- [riseproject-dev/u-boot](https://github.com/riseproject-dev/u-boot) – Branch `v2024.10-a210`, im Tree liegen `a210.dts`, `a210-soc.dtsi` und `board/zhihe/a200-evb`
- [riseproject-dev/opensbi](https://github.com/riseproject-dev/opensbi) – Branch `v1.5-a210`, enthält `platform/generic/zhihe/a210.c`
- [openeuler-riscv/opensbi-zhihe-a210](https://github.com/openeuler-riscv/opensbi-zhihe-a210) – OpenSBI-Portierung des Herstellers
- [revyos/ruyiedk2](https://github.com/revyos/ruyiedk2) – EDK2/UEFI-Plattformfirmware; das README nennt Unterstützung für Melon Pi V1 und V2, `docs/melonpi.md` beschreibt den nativen RAM-Boot und USB-Fastboot

**Distributionsebene**

- [riscv/meta-riscv](https://github.com/riscv/meta-riscv) – die RISC-V-Schicht für OpenEmbedded/Yocto, in der Machine-Tabelle steht `zhihe-a210` („Zhihe Computing Archimedes A210", OSU-OSL-Mainline-Kernel, TFTP-Netboot), `conf/machine/zhihe-a210.conf` existiert tatsächlich
- [RevySR/rvck-image](https://github.com/RevySR/rvck-image) – Bau von rootfs und Disk-Images; das README beschreibt den Ablauf „über Melon Pi EDK2 fastboot flashen" (F9 für Fastboot, `flash emmc0`)
- [riseproject-dev/android_manifest](https://github.com/riseproject-dev/android_manifest) – RISE-Android-17-BSP für die Alibaba A210 EVB, mit Lunch-Target `aosp_a210_evb-trunk_staging-userdebug`
- [riseproject-dev/android_kernel_device](https://github.com/riseproject-dev/android_kernel_device) – die Kleaf-Gerätefragmente dazu (`alibaba/a210/`, `zhihe_a210.fragment`)
- [RuyiSDK-Support-Matrix: A210 SODIMM V2](https://matrix.ruyisdk.org/zh-CN/boards/A210_SODIMM_V2/) ([Quellverzeichnis](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2) · [others.yml](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml)) – Debian und Buildroot sind beide als `wip` markiert; `wip` heißt „in Arbeit, nicht fertig", nicht „nutzbar"
- [ruyisdk/ruyi](https://github.com/ruyisdk/ruyi) – der Paketmanager hat eine Namenskonvention für den Hersteller zhihe, aber **noch keinen eigenen Geräteeintrag für den A210**; wer ruyi installiert, hat damit noch keine A210-Images

---

## 6. GitHub-Projekte im Überblick

Das GitHub-Ökosystem rund um den A210 ist dünn und lässt sich in vier Linien fassen: **RVCK** (vollständigste Device Trees), **RevyOS** (Kernel-Commits + EDK2-Firmware), **RISE Project** (U-Boot / OpenSBI / Android-BSP) und **meta-riscv** (Yocto-Machine). Eine **offizielle GitHub-Organisation von Zhihe gibt es nicht** (`orgs/zhcomputing` liefert 404), alle offiziellen Unterlagen liegen auf der Dokumentationsseite.

Was in Abschnitt 5 bereits steht, wird hier nicht wiederholt; der Rest:

- [kubuds/A210-Melon-Pi-all-in-one](https://github.com/kubuds/A210-Melon-Pi-all-in-one) – dieses Index-Repository
- [PR #208](https://github.com/ruyisdk/packages-index/pull/208) in `ruyisdk/packages-index` – A210-Gerät und Flash-Strategie auf der ruyi-Seite

---

## 7. Gitee-Projekte

Auf Gitee gibt es nur wenige Repositories, die sich direkt an den A210 richten, und **die Such-API von Gitee liefert derzeit für jedes Stichwort leere Ergebnisse**, daher ist dieser Abschnitt **nicht vollständig**:

- [agiros/yolov5_torq_camera](https://gitee.com/agiros/yolov5_torq_camera) – die Beschreibung lautet im Original „hauptsächlich für das A210-Board, kann über torq ein yolov5-Modell aufrufen und die Erkennungsergebnisse samt Bild als AGIROS-Topic versenden". Achtung: Das README ist noch die Standardvorlage von Gitee
- [agiros/ur5-demo](https://gitee.com/agiros/ur5-demo) – dieses Repository wird im AGIROS-Tutorial zum A210-Roboterarm per `git clone` geholt; dort wird auf A210 + openEuler 24.03 visuelles Greifen mit dem UR5 umgesetzt. Das Repository selbst erwähnt den A210 nicht, es wird „von einem A210-Projekt tatsächlich verwendet"

> Fallstrick: Die Suche nach „a210" trifft massenhaft Projekte zum Canaan **K210**; `gitee.com/zhihe` ist der Privataccount von „Herr Zhihe" und hat mit Zhihe Computing nichts zu tun.

---

## 8. Videos

**Bilibili (auf der ganzen Seite nur 2, und keines trägt „Melon Pi" im Namen)**

- [Zhihe Computing Archimedes A210 RISC-V-Entwicklungsboard im Unboxing – XuanTie-C920-Kern + NPU für Allzweck- und Inferenzrechnung](https://www.bilibili.com/video/BV1fJrnBsENd/) · DSOE1024 · 2026-01-14 · ca. 1.7k Aufrufe – **das derzeit einzige Video, das dieses Board wirklich zeigt** (2 Minuten 48 Sekunden)
- [Der Zhihe Computing A210 ist da, der A600 als Vorzeigefall des Kreislaufs „Industrie, Wissenschaft, Forschung"](https://www.bilibili.com/video/BV19R84zsEVH/) · 石榴派-袁德俊 · 2025-07-26 · 428 Aufrufe – Einordnung der Gipfelkonferenz, kein Praxistest des Boards

**YouTube (nur 1 Video, und es ist eine Aufzählung von Spezifikationen plus Kaufhinweis)**

- [Struggling with local AI projects? This RISC-V dev kit might help](https://www.youtube.com/watch?v=yK5x93THqLE) · 스마트직구연구소 – die Beschreibung nennt das Sipeed ZHIHE A210 RISC-V AI Dev Kit; der Inhalt listet Spezifikationen auf, ohne sie zu testen

**Keine Tutorials, keine Entwicklungsberichte, keine Aufzeichnung einer Produktvorstellung.** Zhihe Computing hat weder auf Bilibili noch auf YouTube einen offiziellen Account. Das ist der derzeit ehrlichste Stand dieses Boards, ohne Beschönigung.

---

## 9. Tutorials, Praxisberichte und Berichterstattung

- [AGIROS + RISC-V auf dem Zhihe A210: Full Stack läuft und ist am Gerät verifiziert](https://ruyisdk.cn/t/topic/2362) – **der derzeit vollständigste chinesische Praxisbericht**: Flashen von openEuler 24.03 LTS (inklusive root-Passwort `openEuler12#$`), Netzwerk und statische IP, Installation von AGIROS 25.12 mit einem Befehl, ur5-moveit-demo, Hand-Auge-Kalibrierung, Greifen mit einem echten UR5
- [Unboxing des Zhihe A210 (Video-Repost)](https://ruyisdk.cn/t/topic/2412) – kurzer Beitrag, zeigt Gehäuse und Anschlusslayout
- [Open-Source-Trägerplatine XuanTie MelonPi A210 SODIMM V3](https://p.eda.cn/d-1389550606774960128) – der für die Hardware nützlichste Beitrag (mit 22 Schnittstellenbeschreibungen, BOOT_SEL, PCIe RC/EP, UART4)
- Alibaba-Cloud-Entwicklercommunity: [Aufgabenstellung des 2. CIE-Wettbewerbs für RISC-V-Innovation und -Anwendung](https://developer.aliyun.com/article/1749897) – Aufgabe 1 ist eine „A210 Edge-Vision-Agent"-Anwendung, ausdrücklich auf Basis des A210 (12 TOPS NPU) und des offiziellen Debian-Images, mit Bildaufnahme + YOLOv5/v8 auf dem Gerät + LLM-Dialog in der Cloud. **Wer ein Übungsprojekt für den A210 sucht, kann genau diese Aufgabe umsetzen**
- Weibo-Langbeitrag: [XuanTie in der Praxis – im Einsatz in Fertigung, Robotik und Edge-Computing](https://weibo.com/ttarticle/x/m/geoshow/id/2309405355143666729355) – seltene Messwerte: MobileNetV2 847 FPS, YOLOv8n 336 FPS, Qwen3-4B lokal mit 19 token/s; außerdem Lösungen wie AI-NAS, ein Edge-Gateway mit 16× 1080P, ein 12-TOPS-Compute-Stick und eine PCIe-Karte mit 48 TOPS aus vier zusammengeschalteten A210
- [Zhihe Computing lädt zur AICC2025](https://mp.weixin.qq.com/s/e11WDCFZoI5CtObrTIFO5g) – der einzige Artikel im WeChat-Kanal, der den A210 erwähnt; reine Veranstaltungsankündigung ohne technischen Inhalt

**Englischsprachige Berichte**

- CNX Software: [Zhihe A210 octa-core RISC-V SoC with 12 TOPS NPU powers SoM-based development board](https://www.cnx-software.com/2026/06/17/zhihe-a210-octa-core-risc-v-soc-with-12-tops-npu-powers-som-based-development-board/) – der vollständigste englischsprachige Bericht
- CNX Software: [Three high-performance RISC-V processors to watch in H2 2025](https://www.cnx-software.com/2025/07/22/three-high-performance-risc-v-processors-to-watch-in-h2-2025-ultrarisc-ur-dp1000-zizhe-a210-and-spacemit-k3/) – hier tauchte der A210 erstmals international auf
- OMG! Ubuntu: [New RVA23 RISC-V chips are coming sooner than you think](https://www.omgubuntu.co.uk/2025/07/ubuntu-risc-v-rva23-hardware-coming-soon) – Achtung: Die RVA23-Aussage dort widerspricht der Korrektur von CNX (siehe Abschnitt 1)

> Nicht aufgenommen: CSDN, Zhihu, `bbs.21ic.com` und `eefocus.com` liefern in diesem Netz 521 / 403 / CAPTCHA-Seiten, der Text ist nicht überprüfbar, deshalb ist kein einziger Link von dort enthalten. Der AGIROS-Beitrag auf `x-techcon.com` ist inzwischen 404 (derselbe Inhalt steht im ruyisdk-Beitrag). Der openEuler-Image-Pfad `images.oerv.ac.cn/.../zhihe/a210-dev/` liefert ebenfalls 404 – dafür bitte den offiziellen Weg über die openEuler RISC-V SIG nutzen.

---

## 10. Bezugsquellen

- Offizieller Taobao-Shop von Sipeed (矽速科技), ¥1899 (Seite liefert im Test 200): https://www.taobao.com/list/item/Vk81VmhvN0d2L05DN3gzZ1Z1akk5dz09.htm
- Ein Drittanbieter auf AliExpress (chipboard store) führt es als „Sipeed ZHIHE A210", Konfiguration 8GB/64GB für etwa $334 (die Seite springt auf eine Login-Wand, der Preis taugt nur als Anhaltspunkt)
- Zhihe Computing selbst veröffentlicht keine Seite für Direktverkauf oder Preisauskunft

---

## 11. Vor dem ersten Start

1. **Boardvariante und Revision prüfen**: SODIMM V1 / V2 / V3 oder Compute-Stick; Trägerplatine, Tastenfolge beim Flashen, Stromversorgung und Schnittstellen unterscheiden sich, **die Flash-Anleitungen sind nach Boardvariante getrennt**.
2. **Es gibt nur zwei Images** (Buildroot / Debian Desktop), beide heißen `a210-evb`; ein offizielles Ubuntu gibt es nicht. Für einen Rollback das Paar 2.8.1 verwenden.
3. **Die Trägerplatine V2 wird mit 12V DC versorgt**, das Compute-Modul selbst mit 5V/5A; der Debug-Port ist **UART4** mit 115200.
4. **Die Trägerplatine nicht im laufenden Betrieb stecken**, vor Arbeiten für ESD-Schutz sorgen; der Boot-Modus wird über Pull-up-/Pull-down-Widerstände an BOOT_SEL eingestellt, PCIe hat eine RC/EP-Umschaltung.
5. `wip` in der Support-Matrix heißt nicht, dass es funktioniert; bei Problemen mit Device Tree oder Treibern bitte Boardvariante, Image- und Kernelversion sowie das vollständige serielle Log mitschicken.

---

## 12. Wie dieser Index gepflegt wird

- Täglich um 13:00 läuft ein inkrementeller Scan über alle Quellen (neue Versionen im offiziellen Artefakt-Repository, neue Doku-Seiten, neue Videos, neue Repositories); bei Änderungen wird diese Datei aktualisiert
- Aufgenommen werden nur **erreichbare** Links; bei jeder Aktualisierung läuft eine vollständige Linkprüfung, tote Links fliegen raus oder werden ersetzt
- Bei Videos muss tatsächlich ein A210 gefilmt sein; bei Projekten müssen im Repository wirklich Device Trees, Branches oder BSPs für den A210 liegen (nicht nur eine beiläufige Erwähnung)
- Aufnahme ist keine Empfehlung. Builds von Drittanbietern außerhalb der offiziellen Images, ihre Lizenz und ihr Wartungsstand sind selbst zu beurteilen
- Fehlendes gern als Issue / PR melden, bitte mit Originalquelle, passender Boardvariante und Datum des Zugriffs

[Zurück zum Sprachindex](README.md)
