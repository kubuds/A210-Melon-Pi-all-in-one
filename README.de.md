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
- [Flash-Anleitung SODIMM V1](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V1_Burning_Instruction) – die älteste der vier boardbezogenen Anleitungen, gilt nur für V1-Trägerplatten
- [Flash-Anleitung SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V2_Burning_Instruction) – 12V-DC-Versorgung, TTL-Debug-Port mit 115200, USB-A-Flash-Port; Flash-Taste gedrückt halten und Reset auslösen, um in den USB-Modus zu gelangen; unter Windows platform-tools r34.0.5 + usb_driver r13, unter Linux android-sdk-platform-tools
- [Flash-Anleitung SODIMM V3](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V3_Burning_Instruction)
- [Flash-Anleitung Compute-Stick (Dongle)](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_Dongle_Burning_Instruction) – diese Bauform wird leicht übersehen

**Hardware-Plattform**

- [Benutzerhandbuch Compute-Modul](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/核心板说明) – zentrale Parameter, Abmessungen, 260-Pin-Pinbelegung
- [Benutzerhandbuch Trägerplatine SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V2_baseboard_developer_guide) – Schnittstellen, BOOT_SEL, PCIe-Umschaltung RC/EP, UART4 als Debug-Seriellenport
- Benutzerhandbücher der beiden anderen Trägerplatten: [SODIMM V1](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V1_baseboard_developer_guide) · [SODIMM V3](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V3_baseboard_developer_guide)
- Schaltpläne der Trägerplatten (einer pro Boardvariante, insgesamt vier): [SODIMM V1](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V1) · [SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V2) · [SODIMM V3](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V3) · [Compute-Stick](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Dongle)
- [Hardware-Design-Leitfaden](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/) – Pflichtlektüre, bevor du eine eigene Trägerplatine entwickelst; der Text besteht aus zwei Teilen: [Empfehlungen zum Schaltplan](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/Schematic_Diagram_Design_Suggestions) (Minimalsystem, 24-MHz- und 32,768-kHz-Takt, Reset und Watchdog, BOOT_SEL- und STRAP-Pull-Widerstände, Behandlung von TEST_MODE/DEBUG_MODE) · [PCB-Empfehlungen](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/PCB_Design_Recommendations)
- [PINMUX](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/A210-PINMUX) · **Tabelle direkt herunterladen**: [A210-PINMUX_20260119.xlsx](https://developer.zhcomputing.com/zh/docs/pdf/A210/Hardware-Platform/A210-PINMUX_20260119.xlsx) (ca. 39 KB, Download getestet)

**SDK**

- [SDK-Übersicht](https://developer.zhcomputing.com/zh/docs/category/sdk) · [Schnellstart (mit Tabelle der Images zum Herunterladen)](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/Basic_quick_start_guide) · [Multimedia-Schnellstart](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/Multimedia_quick_start_guide) · [AI-Schnellstart](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/AI_quick_start_guide)
- Build-Umgebung: [Buildroot-Entwicklungsleitfaden](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/Buildroot_developer_guide) – von der zdocker-Umgebung bis `./build.sh -b buildroot a210`; [BSP-Entwicklungsleitfaden](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/BSP_developer_guide) · [Partitionslayout](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/分区介绍)
- Multimedia: [MPI-API-Referenz](https://developer.zhcomputing.com/zh/docs/SDK/多媒体/MPI_API_Reference/)
- [Einführung in das TORQ SDK](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ%20SDK%E4%BB%8B%E7%BB%8D) – der Einstieg in die 12-TOPS-NPU, mit TORQ-Toolkit und TORQ-LLM-API; Referenzhandbücher: [TORQ-Toolkit Python API](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ-Toolkit%20API%E5%8F%82%E8%80%83) · [TORQ C API](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ%20C%20API%E5%8F%82%E8%80%83) · [TORQ-LLM C API](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ-LLM%20C%20API%E5%8F%82%E8%80%83) · [Liste der unterstützten Plattform-Operatoren](https://developer.zhcomputing.com/zh/docs/SDK/AI/Platform_operators_support_list)
- Weitere Kategorien: [Schnellstart](https://developer.zhcomputing.com/zh/docs/category/快速上手) · [Build-Umgebung](https://developer.zhcomputing.com/zh/docs/category/开发环境构建) · [Multimedia](https://developer.zhcomputing.com/zh/docs/category/多媒体) · [AI](https://developer.zhcomputing.com/zh/docs/category/ai)

**Hersteller- und IP-Seite**

- [XuanTie-Produktseite zum A210](https://www.xrvm.cn/product/board/4565261785988403200) (clientseitig gerendert, kein Text abrufbar)
- [XuanTie-Startseite](https://www.xrvm.cn/) · [XuanTie C920](https://www.xrvm.cn/product/xuantie/C920) · [C908](https://www.xrvm.cn/product/xuantie/C908)
- Die Hauptseite von Zhihe, [www.zhcomputing.com](http://www.zhcomputing.com/), am 2026-11-08 erneut geprüft: **nur über http erreichbar** (`https://` liefert durchgehend 504, die Zertifikatskette ist unvollständig; direkt und über Proxy gleiches Ergebnis). Die Reihe Archimedes listet nur A200 / A300, die letzte Meldung im Newscenter stammt von 2025-07, eine A210-Seite gibt es nicht; die englische Seite `en.zhcomputing.com` ist ein Platzhalter („Website kommt bald"). Maßgeblich für A210 bleibt daher das oben genannte Dokumentationszentrum. Geschäftskontakt: business@zhcomputing.com

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
- **Verzeichnisindex des offiziellen Artefakt-Repositories** (vollständiger als die Tabelle in der Doku): [downloads/release/](http://developer.zhcomputing.com/downloads/release/) – unter `zhihesdk` liegen v2.7.0 / v2.8.0 / v2.8.1 / v2.9.0 sowie zwei Entwicklungs-Snapshots, `develop/` und `develop-test/` (das jüngste a210-Image dort ist vom 2026-02-05 und damit älter als v2.9.0 – nicht für einen neueren Build halten), unter `npu` v1.3–v2.1 (ovx-compiler, torq-llm, uca-nn, viplite), unter `tools` ein 1.17 GB großes Build-Container-Image `ubuntu-24.04-x86_64.v1.7.0.tar.gz`
- **Das offizielle Artefakt-Repository lieferte ab 2026-11-13 auf allen Pfaden 503 und ist seit der Prüfung am 2026-11-18 wieder erreichbar**: Verzeichnisindex und alle vier Image-Direktlinks antworten wieder mit 200, `br2image-v2.9.0-a210_evb.tar.gz` mit 188.113.587 Bytes (179,4 MB) und `usb_driver_r13-windows.zip` mit 8.682.039 Bytes, passend zu den angegebenen Größen; während der Störung lieferten dieselben Pfade eine 4,6 MB große JFrog-Platform-Ladeseite
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
- [[PATCH RFC 00/18] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-October/102222.html) – die Überarbeitung vom 2026-10-27 (v2 nach Nummerierung des Autors): Der A210 hat zusätzlich einen Management-Kern E902, und die Clock- und Reset-Register werden tatsächlich von der dort laufenden Zephyr-SCMI-Firmware verwaltet; diese Version entfernt die nativen clk/reset-Treiber zugunsten der Standard-SCMI-Protokolle clock/reset und ergänzt einen AP→E902-Doorbell-Mailbox-Treiber; startet auf dem Melon Pi V2 mit allen acht Kernen bis zur UART-Shell. **Beide Serien sind Stand 2026-11-02 nicht im Mainline**; die neueste ist v3, siehe nächster Punkt
- [[PATCH RFC v3 00/17] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-November/102729.html) – v3 vom 2026-11-02: auf v7.4-rc1 rebasiert; die ARM-Abhängigkeit von `arm_scmi` entfällt, sodass es auch auf RISC-V baut; die SCMI-clock/reset-IDs wandern von dt-bindings in einen Header neben dem DTS, und das mailbox-Binding nutzt feste local-/remote-Regionen; auf dem Melon Pi V2 starten mit der riscv-defconfig alle acht Kerne bis zur seriellen Shell. Bleibt RFC, bis die Firmware von Zhihe SCMI nativ unterstützt. Außerdem nutzen in diesen Bindings die V3-Baseboards dasselbe Compatible wie V2 (`zhihe,a210-melonpi-v2`), es gibt upstream also keinen eigenen v3-Boardnamen, und ein V2-DTB auf V3-Hardware ist erwartetes Verhalten (Conor Dooley hat das Binding geackt). Auf der Review-Seite fehlt nur noch eine Nicht-RFC-Version: sowohl das pinctrl-dt-binding als auch der Treiber haben von Linus Walleij ein LGTM ([102916](https://lists.infradead.org/pipermail/linux-riscv/2026-November/102916.html)), und Conor Dooley schlägt vor, das von SCMI unabhängige pinctrl in eine eigene Serie auszulagern ([103213](https://lists.infradead.org/pipermail/linux-riscv/2026-November/103213.html)).
- [[PATCH v4 00/13] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-November/104545.html) – v4 vom 2026-11-20, **RFC gestrichen und als reguläre Serie gesendet**: nachdem Zhihe SCMI in der Firmware zugestimmt hat, ist der frühere Vorbehalt weg. Die Serie ist auf v7.4-rc3 rebased und nach Review aufgeteilt – die `arm_scmi`-Architekturabhängigkeit geht separat, `vendor-prefixes` und der Pin-Controller wurden eigene Serien (laut Autor beide in linux-next) –, sodass aus 18 nur noch **13 Patches** wurden und die Serie jetzt nur Mailbox, UARTs samt Bindings, DT, defconfig und MAINTAINERS enthält. Ein Melon Pi V2 bootet mit riscv defconfig bis zur seriellen Shell, alle acht CPUs online; das Board-Binding `zhihe,a210-melonpi-v1/v2` trägt weiterhin `Acked-by: Conor Dooley` (v4 05/13). Stand 2026-11-25 nicht in mainline, in patchwork stehen alle 13 Patches weiterhin auf `new`, und nach dem Posting gibt es noch keine Review-Antworten

**Kernel und Device Trees (noch in den Entwicklungszweigen der Anbieter)**

- [RVCK Linux](https://github.com/RVCK-Project/rvck) – im Branch `rvck-6.6` sind die Device Trees am vollständigsten: [a210.dtsi](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi) · [a210-melon-pi.dts](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts) · [Device-Tree-Binding für Zhihe](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml); die Commit-Suche findet 56 A210-bezogene Commits, darunter GPIO/UART/timer/DMA/sdhci
- [RVCK: Issue zur Peripheral-Unterstützung des A210](https://github.com/RVCK-Project/rvck/issues/381) · [gemergter PR zur Peripheral-Unterstützung](https://github.com/RVCK-Project/rvck/pull/382)
- [RVCK: PR #437 zur USB-Unterstützung des A210](https://github.com/RVCK-Project/rvck/pull/437) – am 2026-10-22 eröffnet und **am 2026-11-23 gemergt**; am 2026-11-11 hat der Autor ihn in einen **Draft** umgewandelt, am **11-18** aber wieder auf **ready** gestellt: Zuvor war die Serie auf das aktualisierte `rvck-6.6` rebased worden (20 Patches, darunter der zweite GMAC am Melon Pi, ein UART-pinctrl-Fix, GPIO-Ranges, Zicbop-Blockgröße und Device-Tree-Aufräumarbeiten); am selben Tag nannte Icenowy drei Device-Tree-Punkte zu `a210.dtsi` (Knoten mit überlappendem reg besser wieder über syscon oder ein aus clk_usb registriertes aux device; die beiden unabhängigen PHYs brauchen je einen eigenen Knoten; ein `syscon`-Property braucht ein Herstellerpräfix), und der CI-Lauf vom 11-13 besteht die gesamte Kette (check-patch, kunit, kernel-build sowie LAVA-QEMU-Boot inklusive Ergebnisabholung); danach bat der Autor @unicornx und Icenowy öffentlich um Review, und Icenowy ergänzte am selben Tag zwei weitere Punkte: `clk_usb` sollte nicht in eigene Knoten aufgeteilt werden, sondern den gesamten Registersatz abdecken und syscon aus dem clk-Treiber bereitstellen; die beiden USB2-PHYs können je einen eigenen Knoten bekommen, wobei der Pulldown als DT-Property wie `zhihe,pulldown-mask` ausgedrückt wird; das USB2-PHY auf der DWC3-Seite sollte ein Knoten ohne reg werden oder in den Glue integriert werden, und der Property-Name sollte beschreibend sein, etwa `zhihe,usb-syscon` (nur `syscon` ist nicht zulässig). Der Head-Commit ist jetzt `4990a7ac`. **Stand 2026-11-18**: Der Autor hat die Serie nach den Anmerkungen neu geordnet und rebased und den PR von Draft auf ready zurückgestellt; die PR-Beschreibung hält die endgültige Lösung fest — die beiden DWC2-PHYs haben je einen eigenen Registerblock, die Pulldown-Bits beschreibt `zhihe,pulldown-mask`; das USB2-PHY auf DWC3-Seite teilt sich MMIO mit dem USB-Clock-Controller, deshalb registriert der clk-Treiber die regmap im syscon und das PHY holt sie über den Phandle `zhihe,usb-syscon`, statt ein `reg` zu beschreiben, das den Clock-Knoten überlappt. Es bleiben 20 Patches, 24 Dateien, +2296/−257; Icenowy antwortete am selben Tag mit LGTM, alle vier CI-Prüfungen (check-patch, kunit, kernel-build, LAVA QEMU) liefen durch, und unicornx hat Build und Boot auf QEMU/virt und Pioneerbox getestet — **am 11-23 in `rvck-6.6` gemergt** (Merge-Commit `f8351c85`): `a210.dtsi` enthält jetzt den Knoten `zhihe,a210-dwc3-usb2-phy` (Register über `zhihe,usb-syscon`) und den USB3-PHY, `a210-melon-pi.dts` die vbus-Regler für `usb2_0`/`usb2_1` und den Type-C-Rollenschalter für `usb3`. Inhalt: zwei DWC2-Controller und drei USB-2.0-PHY-Instanzen, der DWC3-Glue und das USB-3.1/DP-Combo-PHY sowie der FUSB302-Type-C-Controller des Melon Pi; [Issue #477 zu PCIe und SATA](https://github.com/RVCK-Project/rvck/issues/477) ist ebenfalls offen
- [RevyOS Linux](https://github.com/revyos/linux) – der Standard-Branch `revyos/7.3.y` wird seit dem 11-21 an vier Tagen hintereinander täglich komplett umgeschrieben, **aktueller Head ist [`9c93e241`](https://github.com/revyos/linux/commit/9c93e241b3) (2026-11-24)**: Der Stand vom 11-24 trägt die Upstream-Patches im Standard-Branch: [`FROMGIT: pinctrl: zhihe: add A210 support`](https://github.com/revyos/linux/commit/0e533424) (als FROMGIT markiert, also schon im pinctrl-Subsystem-Baum), [`FROMLIST: mailbox: add Zhihe A210 AP to E902 mailbox driver`](https://github.com/revyos/linux/commit/d5ce9954), [`FROMLIST: dt-bindings: riscv: add Melon Pi V1 and V2`](https://github.com/revyos/linux/commit/12dde5ea) und [`FROMLIST: riscv: dts: zhihe: add Melon Pi V1 and V2`](https://github.com/revyos/linux/commit/ed2dc077) (dazu A210 core / UARTs / module memory Device-Tree-Patches aus derselben Runde); in mainline ist davon weiterhin nichts: `drivers/pinctrl/zhihe` und `arch/riscv/boot/dts/zhihe` gibt es in torvalds/linux nicht. Der A210-defconfig-Commit ist jetzt [`REVYOS: config: enable Zhihe A210 support`](https://github.com/revyos/linux/commit/a774c69b95): er aktiviert `CONFIG_ARCH_ZHIHE`, `CONFIG_PINCTRL_ZHIHE_A210` und `CONFIG_ZHIHE_A210_MBOX`, hebt `ARM_SCMI_PROTOCOL` und `COMMON_CLK_SCMI` von `=m` auf `=y` und ergänzt `ARM_SCMI_PERF_DOMAIN=m`, `ARM_SCMI_POWER_DOMAIN=m` und `RESET_SCMI=m` — A210 holt Takt und Resets beide über SCMI, die ersten beiden müssen also eingebaut sein. Durch das Umschreiben sind die früher notierten `62df2f69` und `96b82eb6` aus dem Standard-Branch gefallen (`62df2f69` ist vom aktuellen Head divergiert: 339 ahead / 334 behind); [A210-Maintainer-Eintrag](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d) · [Device Tree für Temperaturregelung und Watchdog](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4) · [PWM-Treiber](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d) · [Audio-Routing auf dem Melon Pi V2](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146) liegen weiterhin nur auf `rv/a210-upstream-local`
- [RISE Project: riseproject-dev/linux](https://github.com/riseproject-dev/linux) – ein Branch `alibaba-a210` ist vorhanden

**Boot und Firmware**

- [riseproject-dev/u-boot](https://github.com/riseproject-dev/u-boot) – Branch `v2024.10-a210`, im Tree liegen `a210.dts`, `a210-soc.dtsi` und `board/zhihe/a200-evb`; außerdem gibt es einen [`fix/a210-sdhci-1v8-phy`](https://github.com/riseproject-dev/u-boot/tree/fix/a210-sdhci-1v8-phy)-Branch, dessen Commit vom 2026-11-17 `zhihe_sdhci` den passenden PHY für fest 1,8 V betriebene eMMC wählen lässt
- [riseproject-dev/opensbi](https://github.com/riseproject-dev/opensbi) – Branch `v1.5-a210`, enthält `platform/generic/zhihe/a210.c`
- [openeuler-riscv/opensbi-zhihe-a210](https://github.com/openeuler-riscv/opensbi-zhihe-a210) – OpenSBI-Portierung des Herstellers
- [revyos/ruyiedk2](https://github.com/revyos/ruyiedk2) – EDK2/UEFI-Plattformfirmware; das README nennt Unterstützung für Melon Pi V1 und V2, `docs/melonpi.md` beschreibt den nativen RAM-Boot und USB-Fastboot
- [openeuler-riscv/bootloader-build · zhihe-a210](https://github.com/openeuler-riscv/bootloader-build/tree/master/zhihe-a210) – Verzeichnis fertiger Boot-Firmware der openEuler-RISC-V-SIG: `binman-emmc_boot-loader.img` (wird in die eMMC-Partition BOOT1 geschrieben), `bootzero-rvbl.bin` und `binman-spl-with-fit-rvbl.bin` (die beiden Fastboot-Nutzlasten) sowie `a210-opensbi.dtb`; das README beschreibt den Fastboot-Einstieg über K1+K2, die zwei `fastboot flash ram` und das Schreiben von `mmc0boot0`, danach `env set fdtfile zhihe/a210-dev.dtb` und `env save` über die serielle Konsole. So wird ein openEuler-24.03-LTS-Image auf die A210 gebracht.
- SCMI-Bootkette (Branches `a210/scmi-v3`, 2026-11-02): [coreboot](https://github.com/revyos/coreboot/tree/a210/scmi-v3) · [OpenSBI](https://github.com/revyos/opensbi/tree/a210/scmi-v3) · [EDK2](https://github.com/revyos/edk2/tree/a210/scmi-v3) · [RevySR/linux, vollständiger Tree mit der übrigen Peripherie](https://github.com/RevySR/linux/tree/a210/scmi-v3) – passend zum RFC v3; die früheren `a210/scmi`-Branches existieren weiter, `revyos/ruyiedk2` hat ebenfalls `a210/scmi-v3`; der Tree zur v4-Serie ist [RevySR/linux `a210/scmi-v4`](https://github.com/RevySR/linux/tree/a210/scmi-v4) (2026-11-18, mit CPU-DVFS über SCMI Performance und den übrigen Peripheriegeräten), die Branchnamen der Bootketten-Repos bleiben gleich
- [RevySR/zephyr `xuantie/scmi-v3`](https://github.com/RevySR/zephyr/tree/xuantie/scmi-v3) – die SCMI-Server-Firmware (Zephyr) auf dem E902; sie verantwortet Stromversorgung, PMIC und das Timing der CPU-DVFS; ein zweiter Branch `xuantie/vcodec-v3` (2026-11-02) legt VP-Takte, Resets und Power-Domains für den VC9000D an und exportiert die Video-Codec-Ressourcen über den SCMI-Server an den AP
- [RevySR/linux `a210/vcodec-v3`](https://github.com/RevySR/linux/tree/a210/vcodec-v3) – neue Entwicklungslinie vom 2026-11-02 für Videodekodierung: Der hantro-Treiber erhält den VC9000D-Decoder des A210 (inklusive VP9) und die passenden Gerätebaum-Knoten
- RevySR/linux hat mehr A210-Branches als nur den SCMI-Zweig: [a210/bringup-v7.3](https://github.com/RevySR/linux/tree/a210/bringup-v7.3) (Bring-up, 2026-10-22), [a210/scmi-bootchain-v7.3](https://github.com/RevySR/linux/tree/a210/scmi-bootchain-v7.3) (SCMI-Bootkette, 10-27) und [b4/a210-init](https://github.com/RevySR/linux/tree/b4/a210-init) (die erste Patch-Serie, 10-21) – je nachdem, was Sie prüfen wollen

**Distributionsebene**

- [riscv/meta-riscv](https://github.com/riscv/meta-riscv) – die RISC-V-Schicht für OpenEmbedded/Yocto, in der Machine-Tabelle steht `zhihe-a210` („Zhihe Computing Archimedes A210"), `conf/machine/zhihe-a210.conf` existiert; [PR #744](https://github.com/riscv/meta-riscv/pull/744), am 2026-11-07 gemergt, stellt die Kernel-Quelle des BSP auf den Tag `v7.2.12-a210` von `riseproject-dev/linux` um (`a210_evb_defconfig`) und ergänzt `test-zhihe-a210.yml`: Cloud-Build plus TFTP-Netboot-Test auf der OSU-OSL-Boardfarm; [PR #748](https://github.com/riscv/meta-riscv/pull/748), am 2026-11-10 gemergt, erweitert die Pfadfilter dieses Workflows und stellt auf `readlink -f` um
- [git.osuosl.org/osuosl/zhihe-a210-kernel](https://git.osuosl.org/osuosl/zhihe-a210-kernel) — eigener A210-Kernelbaum von OSU-OSL, 11 Branches (`osl/a210-mainline`, `osl/a210-6.6.x-lts` und versionsweise Backups); Tag `v7.2.12-osl-a210` (2026-10-23, markiert den OpenSBI-Bereich als `no-map`) ist genau der Kernel, auf den die TFTP-Netboot-Anleitung von meta-riscv verweist; daneben v2.9.0 / v2.8.1 / v2.8.0 / v2.7.0 und Vendor 2.6.0-rc0
- [openRuyi-BSP-RPM/zhihe-a210](https://git.openruyi.cn/openRuyi-BSP-RPM/zhihe-a210) — openRuyis RPM-Spec-Repo für das A210-BSP (4 Commits, letzter am 2026-08-21): Pakete `firmware-zhihe-a210`, `linux-zhihe-a210-vendor-6.6` und `linux-zhihe-a210-vendor-6.6-rogue`; in derselben Gruppe liegen `rvck`, `spacemit-k1` und `spacemit-k3`
- irradium-3.8-Images `zhihe_a210` — Varianten core und xfce, wobei am **2026-11-21 ein frischer Satz neu gebaut** wurde: core 6.6.0 (1,55 GB), core 7.2.15 (1,64 GB) und xfce 6.6.0 (2,88 GB), dazu ein verbliebenes core-Image 6.6.157 vom 09-21 (1,50 GB): [Spiegelverzeichnis](http://ubuntu-releases.acc.umu.se/mirror/irradium.org/images/zhihe_a210/) (das offizielle `dl.irradium.org` antwortet für diesen Baum mit 403, und die offizielle Boards-Seite listet A210 nicht — als Community-Build behandeln); im Unterverzeichnis `kernel/` liegen drei Paketsätze nach Kernel — `kernel-a210#6.6.0` / `#6.6.157` / `#7.2.15`, jeweils mit kernel (387 MB / 371 MB / 505 MB), kernel-firmware (je rund 1,0 GB) und kernel-source (rund 285 MB); der 7.2.15-Satz ist am 11-21 dazugekommen, ein Kernelwechsel braucht also kein komplettes Neuflashen; die Boot-Archive sind weiterhin `boot-20260908.tar.xz` und `boot-20260921.tar.xz`. Die README beschreibt den Bootloader-Flash per fastboot und die U-Boot-Variablen (`/EFI/irradium/grubriscv64.efi` und `/dtb/zhihe/a210-dev.dtb`)
- **FreeBSD-Bring-up (2026-10-30)**: [RevySR/freebsd-src `a210/bringup`](https://github.com/RevySR/freebsd-src/tree/a210/bringup) — ein Nicht-Linux-Portierversuch für den A210: **48 Commits** auf FreeBSD main (Basis ist der Commit vom 10-29), darunter `riscv: Add Zhihe A210 support`, ein PCIe-Host-Controller-Treiber samt E16-PCIe/SATA-PHY, HS400 ES in `sdhci_zhihe`, dwc3 im Dual-Role-Betrieb und buffer DMA in dwc_otg, eine FDT-Anbindung für ig4 plus tca64xx-PMIC, eqos-Korrekturen und `clk: Add a GPIO gated clock driver`, dazu SCMI / mmio_sram / FDT AHCI aktiviert; alles endet am 10-30, es ist reines Bring-up — weder upstream noch fertige Images
- **NixOS-Bring-up (Drittanbieter, 2026-11-20)**: [NixOS bring-up on an Alibaba RISC-V board](https://feyor.sh/blog/nixos-bringup-on-an-alibaba-riscv-board/) – George Huebner hat eine A210 zum NixOS-Buildserver gemacht; das ist der bislang ausführlichste Drittanbieter-Bericht zu einer Distribution auf diesem Board. Für die Cross-Kompilierung genügt `crossSystem.system = "riscv64-linux"`; bei über tausend Paketen traten nur zwei Fehler auf, keiner davon RISC-V-spezifisch (`rust-bindgen` griff zum falschen clang, bei `ministream` fehlte die Cross-Konfiguration), während das Linken schwerer Pakete wie Clang und GFortran über 9 GB pro Prozess brauchte und die Parallelität gedrosselt werden musste. Der Boot folgt der Vendor-Kette U-Boot FSBL → OpenSBI → U-Boot SSBL → Linux; die eigentliche Falle war ein mit `-march=rv64gv` gebautes OpenSBI, dessen Vektorbefehl `vsetivli` eine Illegal-Instruction-Ausnahme auslöste, weil der Vektorkontext in `mstatus` nicht aktiviert war — ein Neubau mit `-march=generic` half. Danach verstummte UART bei `clk: Disabling unused clocks`; mit `clk_ignore_unused` (die Vendor-cmdline macht es genauso) ging es bis in den Userspace. Die GPU ist eine PowerVR BXM-4-64, die upstream in `drm/imagination` und Mesa bereits unterstützt wird; der Autor portierte den Treiber aus 6.18 auf den Vendor-Kernel 6.6 und erreichte 2445 Punkte in vkmark 2025.01, HDMI, Audio, WLAN/Bluetooth und Ethernet wurden geprüft. Zwei Umgebungsfallen sind ebenfalls notiert: macOS erkennt das Board im Fastboot-Modus nicht, und ein floatender `vRef` am Black Magic Probe killt die UART-Ausgabe.
- [RevySR/rvck-image](https://github.com/RevySR/rvck-image) – Bau von rootfs und Disk-Images; das README beschreibt den Ablauf „über Melon Pi EDK2 fastboot flashen" (F9 für Fastboot, `flash emmc0`)
- [riseproject-dev/android_manifest](https://github.com/riseproject-dev/android_manifest) – RISE-Android-17-BSP für die Alibaba A210 EVB, mit Lunch-Target `aosp_a210_evb-trunk_staging-userdebug`; das [Release android-17-v1.0](https://github.com/riseproject-dev/android_manifest/releases/tag/android-17-v1.0) vom 2026-10-14 liefert zusätzlich ein fertiges `rise-android-17-v1.0-a210-evb.tar.gz` (1,24 GB) samt `SHA256SUMS`, im selben Tag auch ein K3-Pico-ITX-Image — Kernel android-mainline 7.1, Grafik über upstream `drm/imagination` und Mesa; die Nightly-Pipeline wurde **am 2026-11-20 komplett neu geschrieben** (Commit `195084be`, `ci: publish nightly pre-releases and releases`): neu sind `.github/scripts/release.py` (367 Zeilen) und `package-android.sh`, [nightly.yml](https://github.com/riseproject-dev/android_manifest/blob/android-17/.github/workflows/nightly.yml) wurde auf 258 Zeilen umgeschrieben (jede Nacht 01:23 UTC, Build nur wenn sich das gepinnte Manifest ändert, erst K3, dann a210, die letzten sieben Pre-Releases bleiben), dazu `release.yml` und [release-tags.yml](https://github.com/riseproject-dev/android_manifest/blob/android-17/.github/workflows/release-tags.yml) – letzteres taggt bei einem veröffentlichten Final-Release jedes im Manifest genannte riseproject-dev-Repo mit dem Release-Tag, sofern der Commit auf dem Branch liegt. Damals hat der Umbau die alten Nightlies tatsächlich gelöscht (die Tags `android-17-nightly-20261119` / `-20261120` / `-20261121` lieferten zeitweise alle 404, auf der [Releases-Seite](https://github.com/riseproject-dev/android_manifest/releases) stand nur noch `android-17-v1.0`), doch die umgebaute Pipeline lief **am 2026-11-21 zum ersten Mal durch**: der Nightly-Lauf um 08:22 UTC war erfolgreich und um 11:46 erschien das Pre-Release [android-17-nightly-20261121](https://github.com/riseproject-dev/android_manifest/releases/tag/android-17-nightly-20261121) mit `rise-android-17-nightly-20261121-a210-evb.tar.gz` (1,24 GB) und einem K3-Pico-ITX-Build, dazu `default.xml` (jedes Projekt auf den gebauten Commit gepinnt) und `SHA256SUMS`; `release-tags.yml` wird bei einem Nightly-Tag wie vorgesehen übersprungen. In den Release Notes steht, dass nichts auf Hardware getestet wurde. Zitiere immer den neuesten Eintrag der Releases-Seite statt eines konkreten Tags.
- [riseproject-dev/android_kernel_device](https://github.com/riseproject-dev/android_kernel_device) – die Kleaf-Gerätefragmente dazu (`alibaba/a210/`, `zhihe_a210.fragment`)
- [riseproject-dev/android_bootloader_build](https://github.com/riseproject-dev/android_bootloader_build) – das Build-Repository für die Boot-Kette von RISE; der Branch `alibaba-android-17` erzeugt das U-Boot-plus-OpenSBI-Paar für a210 (AVB-Prüfung aus, Android-GPT-Layout für die 64 GB eMMC)
- [riseproject-dev/android_vendor_rise](https://github.com/riseproject-dev/android_vendor_rise) – das Repository von RISE für vorgebaute Boot-Ketten und Firmware (`alibaba/a210/bootloader/`): `u-boot.bin`, `spl-with-fit-rvbl.bin`, `bootzero-rvbl.bin`, `riscv-boot.itb`, `emmc-gpt_primary.img`, `a210.dtb` und die Bluetooth-Firmware für den RTL8822CS; die CI baut sie alle drei Stunden aus den vorgelagerten Bootloader-Repositories neu, ein fertiges U-Boot-plus-OpenSBI-Paar für das A210 EVB muss also nicht selbst gebaut werden
- [BayLibre/android_device_alibaba_a210](https://github.com/BayLibre/android_device_alibaba_a210) – ein von BayLibre gepflegter AOSP-Device-Tree (Branch `android-17`, `PRODUCT_SHIPPING_API_LEVEL` 37): das Lunch-Target ist dasselbe, `aosp_a210_evb-trunk_staging-userdebug`, aber `TARGET_ARCH_VARIANT := a210`, weil weder C920 noch C908 Zvbb implementieren und die riscv64-Basis nicht baut; U-Boot/OpenSBI und der Kernel liegen als Prebuilts im Tree, die Debug-Konsole ist `ttyS4` mit 115200. Enthalten sind bereits WiFi/Bluetooth über RTL8822CS, HDMI-Audio, die Vulkan-Deklarationen für PowerVR und ein riscv64-WebView. Das ist ein eigener Android-17-Tree, nicht der RISE-BSP oben
- [BayLibre/android_device_alibaba_a210_kernel](https://github.com/BayLibre/android_device_alibaba_a210_kernel) – das Prebuilt-Kernel-Repository zu diesem Device-Tree: in `mainline/` liegen `Image`, `a210-evb.dtb`, `System.map`, `vmlinux.symvers` und die dlkm-Verzeichnisse, dazu die Entwicklungsbranches `glaroque/a210-fixes` und `jmasson/a210-fixes-wifi-bt`
- [RuyiSDK-Support-Matrix: A210 SODIMM V2](https://matrix.ruyisdk.org/zh-CN/boards/A210_SODIMM_V2/) ([Quellverzeichnis](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2) · [others.yml](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml)) – Debian und Buildroot sind beide als `wip` markiert; `wip` heißt „in Arbeit, nicht fertig", nicht „nutzbar"
- [ruyisdk/ruyi](https://github.com/ruyisdk/ruyi) – der Paketmanager hat **inzwischen einen Geräteeintrag für den A210** (`entities/device/zhihe-a210-sodimm.toml` mit den Varianten V2 / V3, mit [PR #208](https://github.com/ruyisdk/packages-index/pull/208) am 2026-08-27 gemergt); die Board-Image-Pakete `zhihe-br2image-a210-evb` und `zhihe-diskimage-a210-evb-debian` reichen nur bis **2.8.1** (2.9.0 ist noch nicht paketiert) und kommen mit der Provisioning-Strategie `zhihe-a210-v1` samt Partitionsplan — ruyi erkennt die Platine also und kann die 2.8.1-Images nach Partitionstabelle flashen, für 2.9.0 bleibt der offizielle Artefakt-Server zuständig

---

## 6. GitHub-Projekte im Überblick

Das GitHub-Ökosystem rund um den A210 ist dünn und lässt sich in vier Linien fassen: **RVCK** (vollständigste Device Trees), **RevyOS** (Kernel-Commits + EDK2-Firmware), **RISE Project** (U-Boot / OpenSBI / Android-BSP) und **meta-riscv** (Yocto-Machine). Eine **offizielle GitHub-Organisation von Zhihe gibt es nicht** (`orgs/zhcomputing` liefert 404), alle offiziellen Unterlagen liegen auf der Dokumentationsseite.

Was in Abschnitt 5 bereits steht, wird hier nicht wiederholt; der Rest:

- [kubuds/A210-Melon-Pi-all-in-one](https://github.com/kubuds/A210-Melon-Pi-all-in-one) – dieses Index-Repository
- [PR #208](https://github.com/ruyisdk/packages-index/pull/208) in `ruyisdk/packages-index` – A210-Gerät und Flash-Strategie auf der ruyi-Seite
- [riseproject-dev/developer-cloud](https://github.com/riseproject-dev/developer-cloud) (früher `board-farm`, umbenannt am 2026-11-11) – das Verwaltungs-Repo der RISE RISC-V Developer Cloud: die ersten 20 Zhihe-A210-Boards (von Alibaba gespendet) stehen im OSU-OSL der Oregon State University, in Phase 1 mit einem Labgrid-Pool `a210-yocto`, dazu Standorte bei Scaleway (Frankreich) und SOPIC (China); im Repo liegen client/exporter-Konfigurationen und pytest-Fälle unter `boards/zhihe-a210/` sowie vier A210-Pipelines unter `.github/workflows/` (`a210_netboot.yml` für TFTP-In-Memory-Boot von a210-board-01 bis 05, `a210_labgrid_uboot.yml`, `yocto-zhihe-a210.yml` und das am 2026-11-11 ergänzte `a210_telemetry.yml` für zerstörungsfreie Hardware-Telemetrie); die Hub-Seite erhielt zudem Board-Tag-Veröffentlichung mit Tag-/Suchfilter, Android-Erkennung über ADB oder UART und einen Fix für UART-Echo auf zhihe-a210, das die Kernel-Versionserkennung störte; am 2026-11-13 wurde [PR #5](https://github.com/riseproject-dev/developer-cloud/pull/5) (**am 2026-11-20 geschlossen, nicht gemergt**; beide Dokumente fehlen in `main`) eröffnet, der zwei Statusdokumente ergänzt: `docs/status/current_status.md` beschreibt die A210-Flotte im OSU-OSL (`a210-1` bis `a210-5`), die Aufbau-Meilensteine von Shelf 1 mit `a210-s1-b01` bis `b10`, das BayLibre-Copilot- und Relay-Hat-DFU-Design für Shelf 2, die dreistufige x86-Host-Topologie (Chef-Cookbooks `osl-labgrid` und `proj-rise`) sowie die beiden CI-Pools `pool=a210-yocto` und `pool=a210-android`; `docs/status/2026_weekly_progress.md` ist ein rückwärts chronologisches Sync-Log; am 2026-11-14 wurden die Yocto-Netboot-Tests von der selbstgebauten pyserial-UART-Auswertung und den `===CI_PROBE_START===`-Markern auf Labgrids native UBootDriver und ShellDriver umgestellt, ergänzt um eine `ZhiheA210TftpBootStrategy` (`boards/zhihe-a210/strategy.py`, `helpers.py`, wobei `client.yaml` SerialDriver / UBootDriver / ShellDriver verbindet und die Tests auf `test_uname_a` / `test_smp_cores` / `test_opensbi_reserved_memory` zusammenschrumpfen), siehe [Commit c7d058e](https://github.com/riseproject-dev/developer-cloud/commit/c7d058e8a6dd53a180c9fbd741d3032c460bc8be) von Puneetha Ramachandra (Google). Die Commits vom 2026-11-17 bis 11-18 haben auch AOSP an Labgrid angebunden: neuer Hardware-CI-Workflow für AOSP (`ci(a210-aosp)`, `runs-on` nennt die Runner-Gruppe Developer-Cloud-HW explizit) und eine Labgrid-AOSP-UDP-Fastboot-Strategie; die AOSP-Tests lesen `/proc/mounts`, um den Boot zu erkennen, lockern den Kernel-Versionspräfix, laden vor dem Neustart bei Bedarf das bereitgelegte `zhihe_wdt.ko`, und die `SHA256SUMS`-Auswertung verträgt ein `./`-Präfix; auf der Hub-Seite ist `serial_port` auf `/dev/serial/by-path/` festgelegt, und die Serienerkennung kennt die `u-boot#`-Eingabeaufforderung; am 11-18 kamen Labgrid-Export, Treiber und Smoke-Test für ADB über USB-C dazu (Commit `ef4e93e0`).

---

## 7. Gitee-Projekte

Auf Gitee gibt es nur wenige Repositories, die sich direkt an den A210 richten, und **die Such-API von Gitee liefert derzeit für jedes Stichwort leere Ergebnisse**, daher ist dieser Abschnitt **nicht vollständig**:

- [agiros/yolov5_torq_camera](https://gitee.com/agiros/yolov5_torq_camera) – die Beschreibung lautet im Original „hauptsächlich für das A210-Board, kann über torq ein yolov5-Modell aufrufen und die Erkennungsergebnisse samt Bild als AGIROS-Topic versenden". Achtung: Das README ist noch die Standardvorlage von Gitee
- [agiros/ur5-demo](https://gitee.com/agiros/ur5-demo) – dieses Repository wird im AGIROS-Tutorial zum A210-Roboterarm per `git clone` geholt; dort wird auf A210 + openEuler 24.03 visuelles Greifen mit dem UR5 umgesetzt. Das Repository selbst erwähnt den A210 nicht, es wird „von einem A210-Projekt tatsächlich verwendet"

> Fallstrick: Die Suche nach „a210" trifft massenhaft Projekte zum Canaan **K210**; `gitee.com/zhihe` ist der Privataccount von „Herr Zhihe" und hat mit Zhihe Computing nichts zu tun.

---

## 8. Videos

**Bilibili (auf der ganzen Seite nur 4, und nur eines trägt „Melon Pi" im Namen)**

- [Praxisversuch mit dem Zhihe XuanTie A210 Melon Pi Entwicklungsboard](https://www.bilibili.com/video/BV1wdx969Exj/) · donatello1996 · 2026-11-04 · ca. 34 Aufrufe – ein 21-Sekunden-Clip: zwei LED-Matrixanzeigen zeigen Temperatur, Luftfeuchte, Luftdruck und Gestenstatus sowie eine Gesichtsanimation; **das Board selbst ist nie im Bild**, dass es sich um den A210 handelt, lässt sich nur am Titel und an den Tags (RISC-V, XuanTie, Entwicklungsboard) ablesen. Das erste Bilibili-Video mit „Melon Pi" im Titel
- [Robotik-Lösungen auf Basis von A210 x AGIROS](https://www.bilibili.com/video/BV12KFKzkELG/) · AGIROS-Open-Source-Community · 2026-02-02 · ca. 62 Aufrufe – Teil 5 des AGIROS Meetup in Peking; Referent Shen Zhuang ist Senior-AI-Ingenieur bei Zhihe Computing Technology (Hangzhou); **das bislang einzige Video, in dem ein aktiver Zhihe-Ingenieur über den A210 spricht** (14 Minuten 10 Sekunden), und es geht um die Lösung, nicht um Benchmark-Zahlen
- [Zhihe Computing Archimedes A210 RISC-V-Entwicklungsboard im Unboxing – XuanTie-C920-Kern + NPU für Allzweck- und Inferenzrechnung](https://www.bilibili.com/video/BV1fJrnBsENd/) · DSOE1024 · 2026-01-14 · ca. 1.7k Aufrufe – **das derzeit einzige Unboxing-Video dieses Boards** (2 Minuten 48 Sekunden)
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

- **Kubuds (苦芽科技) Unternehmensshop auf Taobao**: https://item.taobao.com/item.htm?id=1034868327078&skuId=6052940225420 — für die Artikeldetails ist ein Taobao-Login nötig, der Link selbst liefert 200
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
