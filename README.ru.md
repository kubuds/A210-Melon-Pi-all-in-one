# Zhihe A210: сводный указатель ресурсов (SODIMM V2 / V3 · стик)

[简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [English](README.en.md) · [Русский](README.ru.md) · [日本語](README.ja.md) · [Deutsch](README.de.md) · [Español](README.es.md)

О платформе Zhihe Computing A210 (во внешних материалах — также «Archimedes A210») на этой странице собрано всё, что можно найти в открытом доступе: официальная документация и техническое описание, **официальные образы с прямой загрузкой**, руководства по прошивке для каждого варианта платы, файлы аппаратного проектирования, работа над ядром и прошивками в upstream, проекты на GitHub и Gitee, а также видео на Bilibili и YouTube, где эта плата действительно показана.

Страница не зеркалирует ни прошивки, ни документы — она указывает только на первоисточник. **Здесь фиксируются ссылки и факты, а не обещания** — перед прошивкой сверяйте ревизию платы, примечания к образу и контрольные суммы.

> **Сначала разберёмся с названиями: у этой платы их больше, чем у большинства отладочных плат.**
>
> - **Кристалл**: Zhihe Computing A210, название продуктовой серии — «Archimedes» (Archimedes A210), гетерогенная AI-SoC, совмещающая универсальные вычисления и инференс.
> - **Форм-факторы**: SODIMM-модуль плюс несущая плата (**V1 / V2 / V3** — три поколения несущих), а также отдельный вариант — **A210 в виде стика (Dongle)**.
> - **Кто говорит «Melon Pi / MelonPi»**: в официальной документации и техническом описании Zhihe этого названия **нет** (официально используется только «A210 SODIMM V1/V2/V3»); оно встречается в именах файлов дерева устройств в патчах upstream Linux (`a210-melonpi-v1.dts` / `-v2.dts`), в заголовке страницы XuanTie на площадке открытого железа Huaqiu («XuanTie MelonPi A210») и в части публикаций в прессе. Если вы видите Melon Pi, речь идёт о той же самой плате — так её называют в ядре и в сообществе.
> - **Не путать с A200**: у Zhihe есть также платформа A200, и официальные образы Ubuntu выпущены только для A200; для A210 официально существуют лишь два набора образов — Buildroot и Debian с графической средой.

---

## 1. Ключевые характеристики

| Параметр | Значение |
| --- | --- |
| SoC | Zhihe Computing A210 (гетерогенная AI-SoC, совмещающая вычисления и инференс) |
| CPU | 4× XuanTie C920 + 4× XuanTie C908 (DAMO Academy), RV64GCV (с векторным расширением) |
| Тактовая частота | В официальном техническом описании указано 1.9 GHz; в публикации CNX Software — до 2.3 GHz для C920 и 1.9 GHz для C908 (данные расходятся; ориентируйтесь на свою партию и техническое описание) |
| GPU | Поддержка Vulkan 1.1/1.2/1.3, OpenCL 1.1/1.2/2.0, OpenGL ES 1.1/2.0/3.0/3.1/3.2 (в официальном описании модель не названа; «IMG BXM-4-64» взято из метаданных матрицы поддержки RuyiSDK) |
| NPU | 12 TOPS@INT8, поддержка INT4/INT8/INT16/FP8/FP16/BF16 |
| Память | 4 / 8 / 16 GB, 64-битная LPDDR4x, до 4266 Mbps |
| Накопители | eMMC 5.1/5.0, NOR/NAND Flash, SD 3.0 |
| Сеть | 2× 10/100/1000 Mbps, гигабитные сетевые порты |
| Дисплей | 1× HDMI 2.0, 1× 4-lane MIPI DSI, DP / eDP (с ограничениями из-за мультиплексирования с USB) |
| Камера | 1× 4-lane + 1× 2-lane либо 3× 2-lane MIPI CSI |
| Расширение | PCIe x4 / x2 + x1, x2 + 2× SATA, 2× x1 + 2× SATA; 2× SPI, 1× QSPI, 7× I²C, 10× UART, 3× 5ch PWM, 2× 1ch ADC |
| USB | 1× USB 3.1 (DP Alt), 2× USB 2.0 |
| Аудио | 3× 2ch I2S/PCM, 1× TDM/PCM |
| Питание / температура | Модуль 5V/5A (минимум); несущая плата — вход 12V DC; −20 °C … 60 °C |
| Размеры модуля | 59.66 mm × 69.94 mm, 260-pin SODIMM |
| Официальная ОС | Linux (Debian с графической средой / Buildroot) |

**Относительно RVA23 существуют две версии**: в публикации OMG! Ubuntu от 2025-07 говорится, что A210 поддерживает все обязательные и опциональные расширения RVA23; CNX Software затем исправил это в комментариях и в основном тексте, отнеся A210 к RVA22, а RVA23 — к следующему поколению A600. **Однозначного вывода нет, не используйте это как основание для выбора.**

Источники: официальные документы «Техническое описание продукта A210» и «Руководство пользователя модуля», а также [страница продукта в сообществе открытого железа Huaqiu](https://p.eda.cn/d-1389550606774960128) (перепечатка той же таблицы характеристик).

---

## 2. Официальная документация (центр документации разработчика Zhihe Computing)

Официальный сайт документации — **developer.zhcomputing.com**, текущая версия **2.9.0**, также доступны архивная версия **2.8.1** и английская редакция `/en/`. Сайт рендерится на стороне клиента, поэтому `curl` не возвращает основной текст — открывайте его в браузере.

**Основные точки входа**

- [Главная страница центра документации](https://developer.zhcomputing.com/zh/docs/intro) · [English](https://developer.zhcomputing.com/en/docs/intro/)
- [Раздел документации A210](https://developer.zhcomputing.com/zh/docs/A210/) · [English](https://developer.zhcomputing.com/en/docs/A210/)
- [Архивная версия 2.8.1](https://developer.zhcomputing.com/zh/docs/2.8.1/category/sdk)

**Техническое описание и прошивка (руководства разделены по типу платы: с неверным образом прошивка не пройдёт)**

- [Техническое описание A210 (полный текст в HTML)](https://developer.zhcomputing.com/zh/docs/A210/A210_Datasheet) — функциональные возможности, корпус, назначение выводов и временные диаграммы
- [Руководства по записи образов (оглавление)](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/)
- [Руководство по прошивке SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V2_Burning_Instruction) — питание 12V DC, отладочный порт TTL 115200, порт прошивки USB-A; для перехода в режим USB удерживайте кнопку прошивки и нажмите сброс; в Windows используются platform-tools r34.0.5 и usb_driver r13, в Linux — android-sdk-platform-tools
- [Руководство по прошивке SODIMM V3](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V3_Burning_Instruction)
- [Руководство по прошивке стика (Dongle)](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_Dongle_Burning_Instruction) — этот форм-фактор очень легко упустить из виду

**Аппаратная платформа**

- [Руководство пользователя модуля](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/核心板说明) — ключевые параметры, размеры, назначение выводов 260-pin
- [Руководство пользователя несущей платы SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V2_baseboard_developer_guide) — интерфейсы, BOOT_SEL, переключение PCIe RC/EP, отладочный порт UART4
- [Принципиальная схема несущей платы SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V2) (для V1/V3 и стика есть отдельные страницы)
- [Руководство по проектированию аппаратного обеспечения](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/) — обязательное чтение перед разработкой собственной несущей платы
- [PINMUX](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/A210-PINMUX) · **таблица для прямой загрузки**: [A210-PINMUX_20260119.xlsx](https://developer.zhcomputing.com/zh/docs/pdf/A210/Hardware-Platform/A210-PINMUX_20260119.xlsx) (около 39 KB, загрузка проверена)

**SDK**

- [Обзор SDK](https://developer.zhcomputing.com/zh/docs/category/sdk) · [Быстрый старт (с таблицей образов)](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/Basic_quick_start_guide)
- [Руководство разработчика Buildroot](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/Buildroot_developer_guide) — от окружения zdocker до `./build.sh -b buildroot a210`
- [Знакомство с TORQ SDK](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ%20SDK%E4%BB%8B%E7%BB%8D) — точка входа для NPU 12 TOPS, вместе с TORQ-Toolkit и API TORQ-LLM
- Другие категории: [быстрый старт](https://developer.zhcomputing.com/zh/docs/category/快速上手) · [сборка окружения разработки](https://developer.zhcomputing.com/zh/docs/category/开发环境构建) · [мультимедиа](https://developer.zhcomputing.com/zh/docs/category/多媒体) · [AI](https://developer.zhcomputing.com/zh/docs/category/ai)

**Производитель и владелец IP**

- [Страница продукта A210 на сайте XuanTie](https://www.xrvm.cn/product/board/4565261785988403200) (рендерится на клиенте, основной текст не извлекается)
- [Главная страница XuanTie](https://www.xrvm.cn/) · [XuanTie C920](https://www.xrvm.cn/product/xuantie/C920) · [C908](https://www.xrvm.cn/product/xuantie/C908)
- Основной сайт Zhihe [www.zhcomputing.com](http://www.zhcomputing.com/) — перепроверено 2026-11-08: **работает только по http** (`https://` стабильно отдаёт 504, цепочка сертификатов неполная; результат одинаков при прямом подключении и через прокси). В разделе Archimedes только A200 / A300, последняя новость в разделе новостей датирована 2025-07, страницы A210 нет; английский сайт `en.zhcomputing.com` — заглушка «сайт скоро откроется». Официальные материалы по A210 по-прежнему в центре документации выше. Контакт для деловых вопросов: business@zhcomputing.com

> Ссылка «GitHub» в подвале сайта документации — заглушка (ведёт на `github.com/your-org`), это не реальный проект, ссылаться на неё не следует.

---

## 3. Официальные образы (прямая загрузка)

Образов всего два: **Buildroot** (лёгкий) и **Debian с графической средой**; оба названы `a210-evb` и поставляются как наборы разделов для fastboot. **Официального образа Ubuntu нет** (Ubuntu выпускается только для A200).

| Образ | Версия | Размер | Загрузка |
| --- | --- | --- | --- |
| Предварительно собранный образ Buildroot | v2.9.0 (текущая) | 179.4 MB | [br2image-v2.9.0-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/br2image-v2.9.0-a210_evb.tar.gz) |
| Образ Debian с графической средой | v2.9.0 (текущая) | 738.4 MB | [diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz) |
| Предварительно собранный образ Buildroot | v2.8.1 (для отката) | 175.9 MB | [br2image-v2.8.1-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/br2image-v2.8.1-a210_evb.tar.gz) |
| Образ Debian с графической средой | v2.8.1 (для отката) | 734.8 MB | [diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz) |

- После распаковки получаются `emmc-*.img`, `bootzero-rvbl.bin`, `fastboot_images.sh` / `.bat`; переведите плату в режим прошивки и просто запустите скрипт
- **Индекс официального хранилища артефактов** (полнее таблицы в документации): [downloads/release/](http://developer.zhcomputing.com/downloads/release/) — в `zhihesdk` лежат v2.7.0 / v2.8.0 / v2.8.1 / v2.9.0, а также два каталога снимков разработки — `develop/` и `develop-test/` (самый свежий образ a210 там датирован 2026-02-05 и старше v2.9.0, не путайте его с новой сборкой), в `npu` — v1.3–v2.1 (ovx-compiler, torq-llm, uca-nn, viplite), в `tools` — сборочный контейнер `ubuntu-24.04-x86_64.v1.7.0.tar.gz` размером 1.17 GB
- Если нужно воспроизвести установку средствами RuyiSDK: [ruyisdk/packages-index PR #208](https://github.com/ruyisdk/packages-index/pull/208) превращает процедуру fastboot, наборы образов Buildroot и Debian версии 2.8.1 и таблицу разделов в записи ruyi с картой разделов и контрольными суммами — по ним можно перекрёстно сверить официальные образы

---

## 4. Файлы аппаратного проектирования (PDF и схемы открытой несущей платы)

[Высокопроизводительная отладочная плата XuanTie MelonPi A210 — открытая несущая плата SODIMM V3](https://p.eda.cn/d-1389550606774960128) (сообщество открытого железа Huaqiu, издатель — XuanTie, лицензия **OpenAtom OHL 1.0**) содержит:

- **A210 SODIMM 底板原理图.zip** (2.69 MB)
- **A210 最小系统 原理图设计建议.pdf** (7.80 MB)
- **A210 最小系统 PCB 设计建议.pdf** (15.55 MB)
- **A210 产品规格书.pdf** (399 KB) — единственный на сегодня канал, по которому можно получить техническое описание в **PDF** (официально публикуется только HTML)
- **A210-PINMUX_20260119.xlsx** (38.89 KB)

Учтите, что это несущая плата **V3**, она на одно поколение отличается от официальной документации для V2. Для загрузки требуется регистрация и вход на сайте.

---

## 5. Ядро, прошивки и дистрибутивы из upstream

**Upstream-ядро Linux (mainline)**

- [[PATCH 00/18] riscv: add initial support for Zhihe A210 and Melon Pi](https://lists.infradead.org/pipermail/linux-riscv/2026-October/101909.html) — первая версия поддержки в mainline (UART/clock/reset/pinctrl + DT), проверена на Melon Pi V2 со всеми восемью включёнными ядрами; имена файлов дерева устройств `a210-melonpi-v1.dts` / `-v2.dts` — это и есть настоящий источник названия «Melon Pi»
- [[PATCH RFC 00/18] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-October/102222.html) — переработка от 2026-10-27 (v2 в нумерации автора): в A210 есть ещё управляющее ядро E902, и регистры тактирования и сброса фактически находятся в ведении прошивки SCMI на Zephyr, работающей на нём; в этой версии нативные драйверы clk/reset убраны в пользу стандартных протоколов SCMI clock/reset, добавлен драйвер mailbox-дверного звонка AP→E902; загрузка до shell на UART на Melon Pi V2 со всеми восемью ядрами. **Ни одна из версий по состоянию на 2026-11-02 в mainline не принята**; самая свежая — v3, см. следующий пункт
- [[PATCH RFC v3 00/17] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-November/102729.html) — v3 от 2026-11-02: серия перебазирована на v7.4-rc1; зависимость `arm_scmi` от архитектуры ARM убрана, поэтому она собирается и на RISC-V; идентификаторы SCMI clock/reset перенесены из dt-bindings в заголовок рядом с DTS, а привязка mailbox переведена на фиксированные области local / remote; на Melon Pi V2 с riscv defconfig загружаются все восемь ядер и появляется shell на последовательном порту. Серия остаётся RFC, пока не решён вопрос с нативной поддержкой SCMI в прошивке Zhihe

**Ядра и деревья устройств (пока в ветках разработки отдельных проектов)**

- [RVCK Linux](https://github.com/RVCK-Project/rvck) — в ветке `rvck-6.6` самые полные деревья устройств: [a210.dtsi](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi) · [a210-melon-pi.dts](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts) · [привязки устройств Zhihe](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml); поиск по коммитам даёт 41 коммит, связанный с A210, включая GPIO/UART/timer/DMA/sdhci
- [RVCK: issue с отслеживанием поддержки периферии A210](https://github.com/RVCK-Project/rvck/issues/381) · [влитый PR с поддержкой периферии](https://github.com/RVCK-Project/rvck/pull/382)
- [RVCK: PR #437 с поддержкой USB для A210](https://github.com/RVCK-Project/rvck/pull/437) — открыт 2026-10-22 и **всё ещё open**, но 2026-11-11 автор перевёл его в **draft**: до этого серия была перебазирована на обновлённый `rvck-6.6` (20 патчей, добавлены второй GMAC на Melon Pi, исправление pinctrl для UART, GPIO ranges, Zicbop block size и чистка device tree), в тот же день Icenowy оставил три замечания по `a210.dtsi` (узлы с перекрывающимися reg — вернуть syscon или регистрировать aux device из clk_usb; два независимых PHY должны быть отдельными узлами; имя свойства `syscon` требует префикса производителя), а прогон CI 11-13 прошёл полностью: check-patch, kunit, kernel-build и загрузка в LAVA QEMU со сбором результатов. Содержимое: два контроллера DWC2 и три экземпляра PHY для USB 2.0, DWC3 glue и combo PHY USB 3.1/DP, плюс контроллер FUSB302 Type-C на Melon Pi; [issue #477 про PCIe и SATA](https://github.com/RVCK-Project/rvck/issues/477) тоже открыт
- [RevyOS Linux](https://github.com/revyos/linux) — [запись о сопровождении A210](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d) · [дерево устройств для термоконтроля и сторожевого таймера](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4) · [драйвер PWM](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d) · [разводка аудио на Melon Pi V2](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146). Учтите, что все эти коммиты лежат в ветке `rv/a210-upstream-local`, а не в ветке по умолчанию
- [RISE Project: riseproject-dev/linux](https://github.com/riseproject-dev/linux) — есть ветка `alibaba-a210`

**Загрузчик и прошивки**

- [riseproject-dev/u-boot](https://github.com/riseproject-dev/u-boot) — ветка `v2024.10-a210`, в дереве есть `a210.dts`, `a210-soc.dtsi`, `board/zhihe/a200-evb`
- [riseproject-dev/opensbi](https://github.com/riseproject-dev/opensbi) — ветка `v1.5-a210`, содержит `platform/generic/zhihe/a210.c`
- [openeuler-riscv/opensbi-zhihe-a210](https://github.com/openeuler-riscv/opensbi-zhihe-a210) — вендорский порт OpenSBI
- [revyos/ruyiedk2](https://github.com/revyos/ruyiedk2) — платформенная прошивка EDK2/UEFI; в README указана поддержка Melon Pi V1 и V2, в `docs/melonpi.md` описаны загрузка из ОЗУ напрямую и USB Fastboot
- Загрузочная цепочка SCMI (ветки `a210/scmi-v3`, 2026-11-02): [coreboot](https://github.com/revyos/coreboot/tree/a210/scmi-v3) · [OpenSBI](https://github.com/revyos/opensbi/tree/a210/scmi-v3) · [EDK2](https://github.com/revyos/edk2/tree/a210/scmi-v3) · [RevySR/linux, полное дерево с остальной периферией](https://github.com/RevySR/linux/tree/a210/scmi-v3) — соответствует RFC v3; прежние ветки `a210/scmi` тоже на месте, у `revyos/ruyiedk2` есть ветка `a210/scmi-v3`
- [RevySR/zephyr `xuantie/scmi-v3`](https://github.com/RevySR/zephyr/tree/xuantie/scmi-v3) — серверная прошивка SCMI (Zephyr) на E902, отвечает за питание, PMIC и тайминги CPU DVFS; вторая ветка `xuantie/vcodec-v3` (2026-11-02) готовит для VC9000D тактирование VP, сбросы и домены питания и экспортирует ресурсы видеокодека на AP через сервер SCMI
- [RevySR/linux `a210/vcodec-v3`](https://github.com/RevySR/linux/tree/a210/vcodec-v3) — новая ветка от 2026-11-02 по декодированию видео: в драйвер hantro добавлен декодер VC9000D для A210 (включая VP9) и соответствующие узлы дерева устройств
- У RevySR/linux есть и другие ветки A210, помимо SCMI: [a210/bringup-v7.3](https://github.com/RevySR/linux/tree/a210/bringup-v7.3) (bring-up, 2026-10-22), [a210/scmi-bootchain-v7.3](https://github.com/RevySR/linux/tree/a210/scmi-bootchain-v7.3) (загрузочная цепочка SCMI, 10-27) и [b4/a210-init](https://github.com/RevySR/linux/tree/b4/a210-init) (первая серия патчей, 10-21) — выбирайте по тому, что хотите проверить

**Уровень дистрибутивов**

- [riscv/meta-riscv](https://github.com/riscv/meta-riscv) — слой RISC-V для OpenEmbedded/Yocto, в списке машин есть `zhihe-a210` ("Zhihe Computing Archimedes A210"), файл `conf/machine/zhihe-a210.conf` действительно существует; [PR #744](https://github.com/riscv/meta-riscv/pull/744), влитый 2026-11-07, перевёл источник ядра BSP на тег `v7.2.12-a210` из `riseproject-dev/linux` (`a210_evb_defconfig`) и добавил `test-zhihe-a210.yml`: сборка в облаке плюс проверка TFTP-загрузки на стенде OSU-OSL; [PR #748](https://github.com/riscv/meta-riscv/pull/748), влитый 2026-11-10, расширил фильтры путей этого workflow и перешёл на `readlink -f`
- [RevySR/rvck-image](https://github.com/RevySR/rvck-image) — сборка rootfs и образов диска; в README приведена процедура «прошивка через Melon Pi EDK2 fastboot» (F9 для входа в Fastboot, `flash emmc0`)
- [riseproject-dev/android_manifest](https://github.com/riseproject-dev/android_manifest) — BSP RISE Android 17 с поддержкой Alibaba A210 EVB, цель lunch — `aosp_a210_evb-trunk_staging-userdebug`
- [riseproject-dev/android_kernel_device](https://github.com/riseproject-dev/android_kernel_device) — фрагменты устройств Kleaf для упомянутого BSP (`alibaba/a210/`, `zhihe_a210.fragment`)
- [riseproject-dev/android_bootloader_build](https://github.com/riseproject-dev/android_bootloader_build) — репозиторий сборки загрузочной цепочки RISE; ветка `alibaba-android-17` собирает для a210 пару U-Boot + OpenSBI (проверка AVB отключена, разметка GPT для 64 GB eMMC)
- [riseproject-dev/android_vendor_rise](https://github.com/riseproject-dev/android_vendor_rise) — репозиторий RISE с готовыми загрузочными цепочками и прошивками (`alibaba/a210/bootloader/`): `u-boot.bin`, `spl-with-fit-rvbl.bin`, `bootzero-rvbl.bin`, `riscv-boot.itb`, `emmc-gpt_primary.img`, `a210.dtb` и прошивка Bluetooth RTL8822CS; CI пересобирает их каждые три часа из вышестоящих bootloader-репозиториев, так что пару U-Boot + OpenSBI для A210 EVB можно не собирать самому
- [BayLibre/android_device_alibaba_a210](https://github.com/BayLibre/android_device_alibaba_a210) — дерево устройств AOSP, которое сопровождает BayLibre (ветка `android-17`, `PRODUCT_SHIPPING_API_LEVEL` 37): цель lunch та же, `aosp_a210_evb-trunk_staging-userdebug`, но `TARGET_ARCH_VARIANT := a210`, потому что ни C920, ни C908 не реализуют Zvbb и базовая конфигурация riscv64 не собирается; U-Boot/OpenSBI и ядро положены в дерево как прекомпилированные, отладочная консоль — `ttyS4` на 115200. Уже есть WiFi/Bluetooth на RTL8822CS, HDMI-аудио, объявления Vulkan для PowerVR и riscv64 WebView. Это отдельное дерево Android 17, не тот же BSP RISE, что выше
- [BayLibre/android_device_alibaba_a210_kernel](https://github.com/BayLibre/android_device_alibaba_a210_kernel) — репозиторий прекомпилированного ядра для этого дерева устройств: в `mainline/` лежат `Image`, `a210-evb.dtb`, `System.map`, `vmlinux.symvers` и каталоги dlkm, плюс ветки разработки `glaroque/a210-fixes` и `jmasson/a210-fixes-wifi-bt`
- [Матрица поддержки RuyiSDK: A210 SODIMM V2](https://matrix.ruyisdk.org/zh-CN/boards/A210_SODIMM_V2/) ([каталог исходников](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2) · [others.yml](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml)) — Debian и Buildroot отмечены как `wip`; `wip` означает «в работе, не завершено» и не равно пригодности к использованию
- [ruyisdk/ruyi](https://github.com/ruyisdk/ruyi) — менеджер пакетов, для производителя Zhihe есть соглашение об именовании, но **отдельной записи устройства A210 пока нет**, поэтому установленный ruyi сам по себе не даёт образов для A210

---

## 6. Обзор проектов на GitHub

Экосистема A210 на GitHub очень тонкая и сводится к четырём линиям: **RVCK** (самые полные деревья устройств), **RevyOS** (коммиты в ядро + прошивка EDK2), **RISE Project** (U-Boot / OpenSBI / Android BSP), **meta-riscv** (машина в Yocto). Официальной организации Zhihe на GitHub **нет** (`orgs/zhcomputing` отдаёт 404), все официальные материалы находятся на сайте документации.

Уже перечисленное в разделе 5 здесь не повторяется; остальное:

- [kubuds/A210-Melon-Pi-all-in-one](https://github.com/kubuds/A210-Melon-Pi-all-in-one) — этот репозиторий-указатель
- [PR #208](https://github.com/ruyisdk/packages-index/pull/208) в `ruyisdk/packages-index` — устройство A210 и стратегия прошивки на стороне ruyi
- [riseproject-dev/developer-cloud](https://github.com/riseproject-dev/developer-cloud) (бывший `board-farm`, переименован 2026-11-11) — репозиторий управления RISC-V Developer Cloud от RISE: первые 20 плат Zhihe A210 (подарены Alibaba) стоят в OSU-OSL при Университете штата Орегон, на Phase 1 работает пул Labgrid `a210-yocto`, плюс площадки Scaleway (Франция) и SOPIC (Китай); в репозитории есть конфиги client/exporter и pytest-кейсы в `boards/zhihe-a210/`, а в `.github/workflows/` — четыре конвейера для A210 (`a210_netboot.yml` с TFTP-загрузкой в память для a210-board-01–05, `a210_labgrid_uboot.yml`, `yocto-zhihe-a210.yml` и добавленный 2026-11-11 `a210_telemetry.yml` для недеструктивной телеметрии железа); тогда же в hub появились публикация тегов плат с фильтрацией по тегам/поиску, автоопределение Android-плат через ADB или UART и исправление эха UART на zhihe-a210, мешавшего определению версии ядра

---

## 7. Проекты на Gitee

Репозиториев на Gitee, напрямую посвящённых A210, очень мало, а **поисковый API Gitee в настоящее время возвращает пустой результат по любому запросу**, поэтому раздел **не претендует на полноту**:

- [agiros/yolov5_torq_camera](https://gitee.com/agiros/yolov5_torq_camera) — в описании сказано: «Предназначен в основном для платы A210, позволяет вызывать модель YOLOv5 через torq и публиковать результаты распознавания вместе с изображением в виде топиков AGIROS». Учтите, что README всё ещё представляет собой шаблон Gitee по умолчанию
- [agiros/ur5-demo](https://gitee.com/agiros/ur5-demo) — именно этот репозиторий клонируют в руководстве AGIROS по роботу-манипулятору на A210; на нём выполняют визуальный захват UR5 на A210 + openEuler 24.03. В самом репозитории A210 не упоминается — он «фактически используется проектом A210»

> Подвох: поиск по «a210» в массе своей выдаёт проекты на Canaan **K210**; `gitee.com/zhihe` — личный аккаунт `知和先生`, не имеющий отношения к Zhihe Computing.

---

## 8. Видео

**Bilibili (на всей площадке всего 4 ролика, и только один назван Melon Pi)**

- [Практический тест отладочной платы Zhihe XuanTie A210 Melon Pi](https://www.bilibili.com/video/BV1wdx969Exj/) · donatello1996 · 2026-11-04 · около 34 просмотров — 21-секундный клип: две светодиодные матричные панели показывают температуру, влажность, давление и состояние жестов плюс анимацию лица; **сама плата в кадр не попадает**, поэтому о том, что это A210, можно судить только по названию и тегам (RISC-V, XuanTie, отладочная плата). Первое видео на Bilibili с Melon Pi в названии
- [Решение для интеллектуальной робототехники на базе A210 x AGIROS](https://www.bilibili.com/video/BV12KFKzkELG/) · сообщество AGIROS · 2026-02-02 · около 62 просмотров — часть 5 встречи AGIROS Meetup в Пекине; докладчик Шэнь Чжуан — старший AI-инженер Zhihe Computing Technology (Ханчжоу); **единственное видео, где о A210 рассказывает действующий инженер Zhihe** (14 мин 10 с), и речь в нём о решении, а не о цифрах бенчмарков
- [Распаковка отладочной платы Zhihe Computing Archimedes A210 RISC-V: ядро XuanTie C920 + NPU, совмещающий вычисления и инференс](https://www.bilibili.com/video/BV1fJrnBsENd/) · DSOE1024 · 2026-01-14 · около 1,7 тыс. просмотров — **единственное видео с распаковкой этой платы** (2 мин 48 с)
- [Выход Zhihe Computing A210: эталонный пример замкнутого цикла «наука — производство», на подходе A600](https://www.bilibili.com/video/BV19R84zsEVH/) · 石榴派-袁德俊 · 2025-07-26 · 428 просмотров — разбор новостей с саммита, а не испытания платы

**YouTube (всего один ролик, и это перечень характеристик плюс реклама магазина)**

- [Struggling with local AI projects? This RISC-V dev kit might help](https://www.youtube.com/watch?v=yK5x93THqLE) · 스마트직구연구소 — в описании указан Sipeed ZHIHE A210 RISC-V AI Dev Kit; содержание — перечень характеристик, без практических испытаний

**Ни руководств, ни отчётов о разработке, ни записи презентации.** У Zhihe Computing нет официальных аккаунтов ни на Bilibili, ни на YouTube. Это самое честное описание текущего состояния платы, без прикрас.

---

## 9. Китайские руководства, практические отчёты и публикации

- [AGIROS + RISC-V на Zhihe A210: полный стек работает и проверен на реальном железе](https://ruyisdk.cn/t/topic/2362) — **самый полный китайский практический отчёт на сегодня**: прошивка openEuler 24.03 LTS (включая пароль root `openEuler12#$`), сеть и статический IP, установка AGIROS 25.12 одной командой, ur5-moveit-demo, калибровка «глаз—рука», захват реальным UR5
- [Распаковка платы Zhihe Computing A210 (перепост видео)](https://ruyisdk.cn/t/topic/2412) — короткая публикация: внешний вид и расположение интерфейсов
- [Открытая несущая плата XuanTie MelonPi A210 SODIMM V3](https://p.eda.cn/d-1389550606774960128) — самая полезная публикация по аппаратной части (описание 22 интерфейсов, BOOT_SEL, PCIe RC/EP, UART4)
- Сообщество разработчиков Alibaba Cloud: [описание задачи второго национального конкурса CIE по высокоуровневым инновациям и применению RISC-V](https://developer.aliyun.com/article/1749897) — задача первая, «Приложение edge-визуального агента на A210», прямо требует A210 (NPU 12 TOPS) и официального образа Debian: сбор изображений + YOLOv5/v8 на устройстве + диалог с облачной большой моделью. **Если ищете проект для практики на A210, делайте по этой задаче**
- Длинная публикация в Weibo: [XuanTie на практике: «запуск» на производственных линиях, в роботах и на периферийных вычислениях](https://weibo.com/ttarticle/x/m/geoshow/id/2309405355143666729355) — редкие измеренные цифры: MobileNetV2 847 FPS, YOLOv8n 336 FPS, локальный инференс Qwen3-4B 19 token/s; кроме того, решения AI NAS, шлюз периферийных вычислений на 16 каналов 1080P, стик с производительностью 12 TOPS и карта PCIe на 48 TOPS из четырёх A210
- [Zhihe Computing на AICC2025](https://mp.weixin.qq.com/s/e11WDCFZoI5CtObrTIFO5g) — единственная статья в официальном аккаунте WeChat, где упоминается A210; чистый анонс мероприятия, без технического содержания

**Публикации на английском**

- CNX Software: [Zhihe A210 octa-core RISC-V SoC with 12 TOPS NPU powers SoM-based development board](https://www.cnx-software.com/2026/06/17/zhihe-a210-octa-core-risc-v-soc-with-12-tops-npu-powers-som-based-development-board/) — самая полная публикация на английском
- CNX Software: [Three high-performance RISC-V processors to watch in H2 2025](https://www.cnx-software.com/2025/07/22/three-high-performance-risc-v-processors-to-watch-in-h2-2025-ultrarisc-ur-dp1000-zizhe-a210-and-spacemit-k3/) — A210 впервые попал в поле зрения международной аудитории
- OMG! Ubuntu: [New RVA23 RISC-V chips are coming sooner than you think](https://www.omgubuntu.co.uk/2025/07/ubuntu-risc-v-rva23-hardware-coming-soon) — учтите, что утверждение о RVA23 противоречит исправлению CNX (см. раздел 1)

> Что не вошло: CSDN, Zhihu, `bbs.21ic.com`, `eefocus.com` в сети на этой машине отдают 521 / 403 / страницу с капчей, основной текст проверить нельзя, поэтому не включена ни одна ссылка. Статья про AGIROS на `x-techcon.com` уже отдаёт 404 (тот же материал есть в публикации на ruyisdk). Путь к образу A210 в openEuler `images.oerv.ac.cn/.../zhihe/a210-dev/` при проверке отдаёт 404 — если он нужен, уточняйте через официальные каналы openEuler RISC-V SIG.

---

## 10. Где купить

- **Корпоративный магазин Kubuds (苦芽科技) на Taobao**: https://item.taobao.com/item.htm?id=1034868327078&skuId=6052940225420 — чтобы увидеть карточку товара, нужен вход в аккаунт Taobao; сама ссылка отдаёт 200
- Сторонний продавец на AliExpress (chipboard store) продаёт его как «Sipeed ZHIHE A210», конфигурация 8GB/64GB — около $334 (при открытии требуется вход в аккаунт, поэтому цену можно рассматривать только как ориентир)
- У самого Zhihe Computing нет публичной страницы прямых продаж и страницы с ценами

---

## 11. Что обязательно проверить перед началом

1. **Уточните форм-фактор и ревизию платы**: SODIMM V1 / V2 / V3 или стик; у разных несущих плат отличаются порядок нажатия кнопки прошивки, питание и интерфейсы — **руководства по прошивке разделены по типу платы**.
2. **Образов всего два** (Buildroot / Debian с графической средой), оба названы `a210-evb`; официального Ubuntu нет. Для отката используйте пару версии 2.8.1.
3. **Несущая плата V2 питается от 12V DC**, сам модуль — 5V/5A; отладочный порт — **UART4**, 115200.
4. **Не подключайте несущую плату на горячую**, перед работой примите меры защиты от статического электричества; режим загрузки задаётся подтягивающими резисторами BOOT_SEL, у PCIe есть переключение RC/EP.
5. `wip` в матрице поддержки не означает, что устройство можно использовать; при проблемах с деревом устройств или драйвером указывайте в обращении ревизию платы, версию образа и ядра, полный лог последовательного порта.

---

## 12. Как поддерживается этот указатель

- Каждый день в 13:00 автоматически выполняется полный инкрементальный обход (новые версии артефактов, новые страницы документации, новые видео, новые репозитории); при наличии изменений файл обновляется
- Включаются только ссылки, которые **открываются**; при каждом обновлении выполняется полная проверка ссылок, мёртвые ссылки убираются или заменяются новыми адресами
- От видео требуется, чтобы в нём действительно была снята A210; от проекта — чтобы в репозитории действительно присутствовали дерево устройств, ветка или BSP для A210, а не одно лишь упоминание
- Включение в список не означает рекомендации. Оценивайте сторонние сборки, лицензии и состояние поддержки самостоятельно
- О пропусках и пробелах сообщайте через issue / PR, указывая первоисточник, применимую ревизию платы и дату обращения

[Вернуться к указателю языков](README.md)
