# Índice de recursos de Zhihe A210 (SODIMM V2 / V3 · barra de cómputo)

[简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [English](README.en.md) · [Русский](README.ru.md) · [日本語](README.ja.md) · [Deutsch](README.de.md) · [Español](README.es.md)

Todo lo que puede encontrarse públicamente sobre el Zhihe Computing A210 (también comercializado como «Archimedes A210») está reunido en esta página: documentación y hojas de datos oficiales, **imágenes oficiales descargables directamente**, guías de grabación por modelo de placa, archivos de diseño de hardware, el estado del kernel y del firmware upstream, proyectos en GitHub y Gitee, y los vídeos de Bilibili y YouTube que realmente muestran esta placa.

Esta página no replica ningún firmware ni documento: solo indica su origen. **Registra enlaces y hechos, no promesas**; antes de grabar, comprueba la revisión de la placa, las notas de la imagen y las sumas de verificación.

> **Primero, aclaremos los nombres: esta placa tiene más alias de lo habitual.**
>
> - **Chip**: Zhihe Computing A210, nombre de la familia de producto «Archimedes» (Archimedes A210), un SoC de IA heterogéneo con cómputo e inferencia integrados.
> - **Formatos de placa**: módulo SODIMM más placa base (**placas base V1 / V2 / V3**), y además un formato aparte de **barra de cómputo A210 (Dongle)**.
> - **Quién dice «Melon Pi / MelonPi»**: la documentación y las hojas de datos oficiales de Zhihe **no** usan ese nombre (oficialmente solo «A210 SODIMM V1/V2/V3»); aparece en los nombres de archivo del árbol de dispositivos de los parches de Linux upstream (`a210-melonpi-v1.dts` / `-v2.dts`), en el título de la página de hardware abierto de XuanTie en Huaqiu («玄铁 MelonPi A210») y en algunos reportajes. Si ves «Melon Pi», se refiere a la misma placa con el nombre que usan el kernel y la comunidad.
> - **No la confundas con la A200**: Zhihe también tiene una plataforma A200, y las imágenes oficiales de Ubuntu son solo para la A200; para la A210 las imágenes oficiales son únicamente Buildroot y Debian de escritorio.

---

## 1. Especificaciones clave

| Elemento | Especificación |
| --- | --- |
| SoC | Zhihe Computing A210 (SoC de IA heterogéneo) |
| CPU | 4× XuanTie C920 + 4× XuanTie C908 (DAMO Academy), RV64GCV (con vectores) |
| Frecuencia | La hoja de datos oficial indica 1.9 GHz; CNX Software informa de hasta 2.3 GHz para el C920 y 1.9 GHz para el C908 (las dos fuentes no coinciden; guíate por tu lote y por la hoja de datos) |
| GPU | Compatible con Vulkan 1.1/1.2/1.3, OpenCL 1.1/1.2/2.0, OpenGL ES 1.1/2.0/3.0/3.1/3.2 (la hoja de datos no indica el modelo; «IMG BXM-4-64» procede de los metadatos de la matriz de soporte de RuyiSDK) |
| NPU | 12 TOPS@INT8, compatible con INT4/INT8/INT16/FP8/FP16/BF16 |
| Memoria | 4 / 8 / 16 GB LPDDR4x de 64 bits, hasta 4266 Mbps |
| Almacenamiento | eMMC 5.1/5.0, NOR/NAND Flash, SD 3.0 |
| Red | 2× puertos Gigabit Ethernet de 10/100/1000 Mbps |
| Pantalla | 1× HDMI 2.0, 1× MIPI DSI de 4 carriles, DP / eDP (limitado por la multiplexación de USB) |
| Cámara | 1× 4 carriles + 1× 2 carriles, o 3× 2 carriles MIPI CSI |
| Expansión | PCIe x4 / x2 + x1, x2 + 2× SATA, 2× x1 + 2× SATA; 2× SPI, 1× QSPI, 7× I²C, 10× UART, 3× PWM de 5 canales, 2× ADC de 1 canal |
| USB | 1× USB 3.1 (DP Alt), 2× USB 2.0 |
| Audio | 3× I2S/PCM de 2 canales, 1× TDM/PCM |
| Alimentación / temperatura | Módulo 5V/5A (mínimo); placa base con entrada de 12V DC; -20 °C ~ 60 °C |
| Dimensiones del módulo | 59.66 mm × 69.94 mm, SODIMM de 260 pines |
| SO oficial | Linux (Debian de escritorio / Buildroot) |

**Sobre RVA23 hay dos versiones**: OMG! Ubuntu afirmó en un artículo de 2025-07 que la A210 admite todas las extensiones obligatorias y opcionales de RVA23; CNX Software lo corrigió después, tanto en los comentarios como en el texto, y sostiene que la A210 es RVA22 y que RVA23 corresponde a la A600 de nueva generación. **No hay conclusión autorizada: no uses esto como base para elegir hardware.**

Fuentes: la «hoja de datos del producto A210» y la «guía del usuario del módulo» oficiales, y la [página de producto de la comunidad de hardware abierto Huaqiu](https://p.eda.cn/d-1389550606774960128) (una reproducción de las mismas tablas).

---

## 2. Documentación oficial (centro de documentación para desarrolladores de Zhihe Computing)

El sitio de documentación es **developer.zhcomputing.com**, actualmente en **2.9.0**, con un archivo **2.8.1** y una edición en inglés en `/en/`. Se renderiza en el cliente, así que `curl` no devuelve el cuerpo: ábrelo en un navegador.

**Punto de entrada**

- [Inicio de la documentación](https://developer.zhcomputing.com/zh/docs/intro) · [English](https://developer.zhcomputing.com/en/docs/intro/)
- [Sección de documentación de la A210](https://developer.zhcomputing.com/zh/docs/A210/) · [English](https://developer.zhcomputing.com/en/docs/A210/)
- [Archivo 2.8.1](https://developer.zhcomputing.com/zh/docs/2.8.1/category/sdk)

**Hoja de datos y grabación (una guía por modelo de placa: si eliges mal, no graba)**

- [Hoja de datos del producto A210 (HTML completo)](https://developer.zhcomputing.com/zh/docs/A210/A210_Datasheet) — características, encapsulado, definición de pines y temporización
- [Guías de grabación de imágenes (índice)](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/)
- [Guía de grabación de la SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V2_Burning_Instruction) — alimentación de 12V DC, puerto de depuración TTL a 115200, puerto de grabación USB-A; mantén pulsada la tecla de grabación y pulsa reinicio para entrar en modo USB; en Windows se usa platform-tools r34.0.5 + usb_driver r13, en Linux android-sdk-platform-tools
- [Guía de grabación de la SODIMM V3](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_SODIMM_V3_Burning_Instruction)
- [Guía de grabación de la barra de cómputo (Dongle)](https://developer.zhcomputing.com/zh/docs/A210/A210_Burning_Instruction/A210_Dongle_Burning_Instruction) — un formato que se pasa por alto con facilidad

**Plataforma de hardware**

- [Guía del usuario del módulo](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/核心板说明) — parámetros clave, dimensiones, definición de los 260 pines
- [Guía del usuario de la placa base SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/BaseBoard-Developer-Guide/A210_SODIMM_V2_baseboard_developer_guide) — conectores, BOOT_SEL, conmutación PCIe RC/EP, UART4 como puerto serie de depuración
- [Esquemático de la placa base SODIMM V2](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Baseboard-Board-diagram/Baseboard_Board_V2) (la V1, la V3 y la barra de cómputo tienen su propia página)
- [Guía de diseño de hardware](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/Hardware-Design-Guide/) — lectura obligada antes de diseñar una placa base propia
- [PINMUX](https://developer.zhcomputing.com/zh/docs/A210/Hardware-Platform/A210-PINMUX) · **descarga directa**: [A210-PINMUX_20260119.xlsx](https://developer.zhcomputing.com/zh/docs/pdf/A210/Hardware-Platform/A210-PINMUX_20260119.xlsx) (unos 39 KB, descarga comprobada)

**SDK**

- [Resumen del SDK](https://developer.zhcomputing.com/zh/docs/category/sdk) · [Inicio rápido (incluye la tabla de imágenes)](https://developer.zhcomputing.com/zh/docs/SDK/Quick-start-guide/Basic_quick_start_guide)
- [Guía de desarrollo con Buildroot](https://developer.zhcomputing.com/zh/docs/SDK/开发环境构建/Buildroot_developer_guide) — desde el entorno zdocker hasta `./build.sh -b buildroot a210`
- [Introducción al TORQ SDK](https://developer.zhcomputing.com/zh/docs/SDK/AI/TORQ%20SDK%E4%BB%8B%E7%BB%8D) — punto de entrada a la NPU de 12 TOPS, con las API de TORQ-Toolkit y TORQ-LLM
- Otras categorías: [inicio rápido](https://developer.zhcomputing.com/zh/docs/category/快速上手) · [entorno de compilación](https://developer.zhcomputing.com/zh/docs/category/开发环境构建) · [multimedia](https://developer.zhcomputing.com/zh/docs/category/多媒体) · [AI](https://developer.zhcomputing.com/zh/docs/category/ai)

**Fabricante y propietario de la IP**

- [Página de producto de la A210 en el sitio de XuanTie](https://www.xrvm.cn/product/board/4565261785988403200) (se renderiza en el cliente; no se puede extraer el cuerpo)
- [Inicio de XuanTie](https://www.xrvm.cn/) · [XuanTie C920](https://www.xrvm.cn/product/xuantie/C920) · [C908](https://www.xrvm.cn/product/xuantie/C908)
- El sitio principal de Zhihe Computing, [www.zhcomputing.com](http://www.zhcomputing.com/), revisado de nuevo el 2026-11-08: **solo funciona por http** (`https://` devuelve 504 siempre y la cadena de certificados está incompleta; el resultado es el mismo en conexión directa y a través de proxy). La serie Archimedes solo lista A200 / A300, la última noticia del centro de noticias es de 2025-07 y no hay página de A210; el sitio en inglés `en.zhcomputing.com` es un marcador de «sitio web próximamente». El centro de documentación de arriba sigue siendo la fuente oficial para A210. Contacto comercial: business@zhcomputing.com

> El enlace «GitHub» del pie del sitio de documentación es un marcador de posición (apunta a `github.com/your-org`), no es un proyecto real: no lo cites.

---

## 3. Imágenes oficiales (descarga directa)

Solo hay dos: **Buildroot** (ligera) y **Debian de escritorio**, ambas con el nombre `a210-evb` y entregadas como paquetes de particiones fastboot. **No hay imagen oficial de Ubuntu** (Ubuntu es solo para la A200).

| Imagen | Versión | Tamaño | Descarga |
| --- | --- | --- | --- |
| Buildroot precompilada | v2.9.0 (actual) | 179.4 MB | [br2image-v2.9.0-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/br2image-v2.9.0-a210_evb.tar.gz) |
| Imagen de escritorio Debian | v2.9.0 (actual) | 738.4 MB | [diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/diskimage_v2.9.0_a210-evb-release_desktop_debian_public.tar.gz) |
| Buildroot precompilada | v2.8.1 (para revertir) | 175.9 MB | [br2image-v2.8.1-a210_evb.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/br2image-v2.8.1-a210_evb.tar.gz) |
| Imagen de escritorio Debian | v2.8.1 (para revertir) | 734.8 MB | [diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz](http://developer.zhcomputing.com/downloads/release/zhihesdk/v2.8.1/diskimage_v2.8.1_a210-evb-release_desktop_debian_public.tar.gz) |

- Al descomprimir se obtienen `emmc-*.img`, `bootzero-rvbl.bin` y `fastboot_images.sh` / `.bat`; entra en modo de grabación y ejecuta el script directamente
- **Índice del repositorio oficial de artefactos** (más completo que la tabla de la documentación): [downloads/release/](http://developer.zhcomputing.com/downloads/release/) — en `zhihesdk` están v2.7.0 / v2.8.0 / v2.8.1 / v2.9.0 y también dos directorios de instantáneas de desarrollo, `develop/` y `develop-test/` (la imagen a210 más reciente allí es del 2026-02-05, anterior a la v2.9.0: no la tomes por una versión nueva), en `npu` están v1.3–v2.1 (ovx-compiler, torq-llm, uca-nn, viplite) y en `tools` hay un contenedor de compilación `ubuntu-24.04-x86_64.v1.7.0.tar.gz` de 1.17 GB
- Si quieres reproducir la instalación con RuyiSDK: [ruyisdk/packages-index PR #208](https://github.com/ruyisdk/packages-index/pull/208) convierte el flujo fastboot, los paquetes de imagen Buildroot y Debian de la 2.8.1 y la tabla de particiones en entradas de ruyi, con mapas de particiones y sumas de verificación para contrastar con las imágenes oficiales

---

## 4. Archivos de diseño de hardware (PDF y esquemáticos de la placa base de código abierto)

[Placa base de código abierto para la XuanTie MelonPi A210 — SODIMM V3](https://p.eda.cn/d-1389550606774960128) (comunidad de hardware abierto Huaqiu, publicada por XuanTie, **OpenAtom OHL 1.0**) ofrece:

- **A210 SODIMM 底板原理图.zip** (2.69 MB)
- **A210 最小系统 原理图设计建议.pdf** (7.80 MB)
- **A210 最小系统 PCB 设计建议.pdf** (15.55 MB)
- **A210 产品规格书.pdf** (399 KB) — la única vía para conseguir la hoja de datos en **PDF** (la oficial solo existe en HTML)
- **A210-PINMUX_20260119.xlsx** (38.89 KB)

Ojo: es la placa base **V3**, una generación distinta de la documentación oficial de la V2. Para descargar hay que registrarse e iniciar sesión en el sitio.

---

## 5. Kernel upstream, firmware y distribuciones

**Linux upstream**

- [[PATCH 00/18] riscv: add initial support for Zhihe A210 and Melon Pi](https://lists.infradead.org/pipermail/linux-riscv/2026-October/101909.html) — el primer soporte en el mainline (UART/clock/reset/pinctrl + DT), validado con los 8 núcleos en marcha en una Melon Pi V2; los nombres de archivo del árbol de dispositivos `a210-melonpi-v1.dts` / `-v2.dts` son el verdadero origen del nombre «Melon Pi»
- [[PATCH RFC 00/18] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-October/102222.html) — la reelaboración del 2026-10-27 (v2 según la numeración del autor): la A210 lleva además un núcleo de gestión E902, y los registros de reloj y reset los gestiona en realidad el firmware SCMI basado en Zephyr que corre en él; esta versión elimina los controladores nativos clk/reset en favor de los protocolos estándar SCMI clock/reset y añade un controlador mailbox de timbre AP→E902; arranca hasta un shell por UART en la Melon Pi V2 con los ocho núcleos. **Ninguna de las dos series está en el mainline a 2026-11-02**; la más reciente es la v3, ver el punto siguiente
- [[PATCH RFC v3 00/17] riscv: add initial Zhihe A210 support using SCMI clocks and resets](https://lists.infradead.org/pipermail/linux-riscv/2026-November/102729.html) — la v3 del 2026-11-02: rebasada sobre v7.4-rc1; se elimina la dependencia de `arm_scmi` de la arquitectura ARM, por lo que también compila en RISC-V; los IDs de SCMI clock/reset pasan de dt-bindings a una cabecera junto al DTS, y el binding de mailbox usa regiones fijas local / remote; en la Melon Pi V2 arranca hasta un shell serie con los ocho núcleos usando la defconfig de riscv. Sigue siendo RFC mientras se resuelve el soporte nativo de SCMI en el firmware de Zhihe

**Kernels y árboles de dispositivos (todavía en las ramas de desarrollo de cada proyecto)**

- [RVCK Linux](https://github.com/RVCK-Project/rvck) — la rama `rvck-6.6` tiene los árboles de dispositivos más completos: [a210.dtsi](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi) · [a210-melon-pi.dts](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts) · [binding del árbol de dispositivos de Zhihe](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml); la búsqueda de commits devuelve 41 commits relacionados con la A210, con GPIO/UART/timer/DMA/sdhci
- [RVCK: issue de seguimiento del soporte de periféricos de la A210](https://github.com/RVCK-Project/rvck/issues/381) · [PR de soporte de periféricos ya fusionado](https://github.com/RVCK-Project/rvck/pull/382)
- [RVCK: PR #437 de soporte USB para la A210](https://github.com/RVCK-Project/rvck/pull/437) — abierto el 2026-10-22 y **sigue open**, pero el autor lo convirtió en **draft** el 2026-11-11: antes se había hecho rebase sobre el `rvck-6.6` actualizado (19 parches, con el segundo GMAC de la Melon Pi, una corrección de pinctrl de UART, GPIO ranges, Zicbop block size y limpieza del device tree); ese mismo día Icenowy señaló tres puntos del device tree en `a210.dtsi` (los nodos con reg solapado deberían volver a syscon o registrar un aux device desde clk_usb; los dos PHY independientes deberían tener cada uno su nodo; la propiedad `syscon` necesita prefijo de fabricante), y la repetición de CI del 11-12 pasa kernel-build y las otras tres comprobaciones. El contenido: dos controladores DWC2 y tres instancias de PHY para USB 2.0, el glue DWC3 y el combo PHY USB 3.1/DP, además del controlador FUSB302 Type-C de la Melon Pi; [el issue #477 de PCIe y SATA](https://github.com/RVCK-Project/rvck/issues/477) también está abierto
- [RevyOS Linux](https://github.com/revyos/linux) — [entrada de mantenimiento de la A210](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d) · [árbol de dispositivos de temperatura y watchdog](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4) · [controlador PWM](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d) · [routing de audio de la Melon Pi V2](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146). Ojo: todos estos commits están en la rama `rv/a210-upstream-local`, no en la rama por defecto
- [RISE Project: riseproject-dev/linux](https://github.com/riseproject-dev/linux) — tiene una rama `alibaba-a210`

**Arranque y firmware**

- [riseproject-dev/u-boot](https://github.com/riseproject-dev/u-boot) — rama `v2024.10-a210`, el árbol incluye `a210.dts`, `a210-soc.dtsi` y `board/zhihe/a200-evb`
- [riseproject-dev/opensbi](https://github.com/riseproject-dev/opensbi) — rama `v1.5-a210`, con `platform/generic/zhihe/a210.c`
- [openeuler-riscv/opensbi-zhihe-a210](https://github.com/openeuler-riscv/opensbi-zhihe-a210) — port de OpenSBI del fabricante
- [revyos/ruyiedk2](https://github.com/revyos/ruyiedk2) — firmware de plataforma EDK2/UEFI; el README indica que admite Melon Pi V1 y V2, y `docs/melonpi.md` documenta el arranque nativo en RAM y el USB Fastboot
- Cadena de arranque SCMI (ramas `a210/scmi-v3`, 2026-11-02): [coreboot](https://github.com/revyos/coreboot/tree/a210/scmi-v3) · [OpenSBI](https://github.com/revyos/opensbi/tree/a210/scmi-v3) · [EDK2](https://github.com/revyos/edk2/tree/a210/scmi-v3) · [RevySR/linux, árbol completo con el resto de periféricos](https://github.com/RevySR/linux/tree/a210/scmi-v3) — acompaña al RFC v3; las ramas anteriores `a210/scmi` siguen ahí y `revyos/ruyiedk2` también tiene `a210/scmi-v3`
- [RevySR/zephyr `xuantie/scmi-v3`](https://github.com/RevySR/zephyr/tree/xuantie/scmi-v3) — firmware servidor de SCMI (Zephyr) sobre el E902; se encarga de la alimentación, el PMIC y los tiempos de CPU DVFS; una segunda rama, `xuantie/vcodec-v3` (2026-11-02), prepara los relojes VP, los resets y los dominios de alimentación del VC9000D y exporta los recursos de códec de vídeo al AP mediante el servidor SCMI
- [RevySR/linux `a210/vcodec-v3`](https://github.com/RevySR/linux/tree/a210/vcodec-v3) — nueva línea de desarrollo del 2026-11-02 para decodificación de vídeo: añade al driver hantro el decodificador VC9000D de la A210 (con VP9) y los nodos correspondientes del árbol de dispositivos
- RevySR/linux tiene más ramas A210 que la de SCMI: [a210/bringup-v7.3](https://github.com/RevySR/linux/tree/a210/bringup-v7.3) (bring-up, 2026-10-22), [a210/scmi-bootchain-v7.3](https://github.com/RevySR/linux/tree/a210/scmi-bootchain-v7.3) (cadena de arranque SCMI, 10-27) y [b4/a210-init](https://github.com/RevySR/linux/tree/b4/a210-init) (la primera serie de parches, 10-21) — elige la que corresponda a lo que quieras verificar

**Capa de distribución**

- [riscv/meta-riscv](https://github.com/riscv/meta-riscv) — la capa RISC-V de OpenEmbedded/Yocto incluye la máquina `zhihe-a210` ("Zhihe Computing Archimedes A210") y `conf/machine/zhihe-a210.conf` existe; el [PR #744](https://github.com/riscv/meta-riscv/pull/744), fusionado el 2026-11-07, cambió el origen del kernel del BSP a la etiqueta `v7.2.12-a210` de `riseproject-dev/linux` (`a210_evb_defconfig`) y añadió `test-zhihe-a210.yml`: compilación en la nube más una prueba de netboot por TFTP en la board farm de OSU-OSL
- [RevySR/rvck-image](https://github.com/RevySR/rvck-image) — construcción de rootfs e imágenes de disco; el README describe el flujo «grabar mediante Melon Pi EDK2 fastboot» (F9 para entrar en Fastboot, `flash emmc0`)
- [riseproject-dev/android_manifest](https://github.com/riseproject-dev/android_manifest) — BSP de RISE Android 17 que cubre la Alibaba A210 EVB, con objetivo de lunch `aosp_a210_evb-trunk_staging-userdebug`
- [riseproject-dev/android_kernel_device](https://github.com/riseproject-dev/android_kernel_device) — los fragmentos de dispositivo Kleaf de ese BSP (`alibaba/a210/`, `zhihe_a210.fragment`)
- [riseproject-dev/android_bootloader_build](https://github.com/riseproject-dev/android_bootloader_build) — repositorio de compilación de la cadena de arranque de RISE; la rama `alibaba-android-17` genera el par U-Boot + OpenSBI para la a210 (verificación AVB desactivada, diseño GPT de Android para la eMMC de 64 GB)
- [riseproject-dev/android_vendor_rise](https://github.com/riseproject-dev/android_vendor_rise) — repositorio de RISE con cadenas de arranque y firmware precompilados (`alibaba/a210/bootloader/`): `u-boot.bin`, `spl-with-fit-rvbl.bin`, `bootzero-rvbl.bin`, `riscv-boot.itb`, `emmc-gpt_primary.img`, `a210.dtb` y el firmware Bluetooth del RTL8822CS; la CI los reconstruye cada tres horas a partir de los repositorios de bootloader de aguas arriba, así que no hace falta compilar un par U-Boot + OpenSBI para la A210 EVB
- [BayLibre/android_device_alibaba_a210](https://github.com/BayLibre/android_device_alibaba_a210) — árbol de dispositivos AOSP mantenido por BayLibre (rama `android-17`, `PRODUCT_SHIPPING_API_LEVEL` 37): el objetivo de lunch es el mismo, `aosp_a210_evb-trunk_staging-userdebug`, pero `TARGET_ARCH_VARIANT := a210`, porque ni el C920 ni el C908 implementan Zvbb y la base riscv64 no compila; U-Boot/OpenSBI y el kernel se incluyen como precompilados y la consola de depuración es `ttyS4` a 115200. Ya trae WiFi/Bluetooth con RTL8822CS, audio por HDMI, las declaraciones Vulkan de PowerVR y un WebView riscv64. Es un árbol Android 17 independiente del BSP de RISE de arriba
- [BayLibre/android_device_alibaba_a210_kernel](https://github.com/BayLibre/android_device_alibaba_a210_kernel) — repositorio del kernel precompilado para ese árbol de dispositivos: en `mainline/` están `Image`, `a210-evb.dtb`, `System.map`, `vmlinux.symvers` y los directorios dlkm, además de las ramas de desarrollo `glaroque/a210-fixes` y `jmasson/a210-fixes-wifi-bt`
- [Matriz de soporte de RuyiSDK: A210 SODIMM V2](https://matrix.ruyisdk.org/zh-CN/boards/A210_SODIMM_V2/) ([directorio del código fuente](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2) · [others.yml](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml)) — Debian y Buildroot aparecen como `wip`; `wip` significa «en curso, sin terminar», no equivale a utilizable
- [ruyisdk/ruyi](https://github.com/ruyisdk/ruyi) — el gestor de paquetes tiene una convención de nombres para el fabricante zhihe, pero **todavía no hay entrada de dispositivo para la A210**; no supongas que instalar ruyi te da imágenes para la A210

---

## 6. Panorama de proyectos en GitHub

El ecosistema de la A210 en GitHub es escaso y se reduce a cuatro líneas: **RVCK** (los árboles de dispositivos más completos), **RevyOS** (commits de kernel + firmware EDK2), **RISE Project** (U-Boot / OpenSBI / BSP de Android) y **meta-riscv** (máquina Yocto). **No existe una organización oficial de Zhihe en GitHub** (`orgs/zhcomputing` devuelve 404); todo el material oficial está en el sitio de documentación.

Lo ya listado en la sección 5 no se repite; el resto:

- [kubuds/A210-Melon-Pi-all-in-one](https://github.com/kubuds/A210-Melon-Pi-all-in-one) — este índice
- [PR #208](https://github.com/ruyisdk/packages-index/pull/208) de `ruyisdk/packages-index` — la estrategia de ruyi para el dispositivo A210 y su grabación
- [riseproject-dev/board-farm](https://github.com/riseproject-dev/board-farm) — el repositorio de gestión de la board farm de RISE: las primeras 20 placas Zhihe A210 (donadas por Alibaba) están en OSU-OSL, en la Oregon State University, con un pool de Labgrid `a210-yocto` en la Phase 1; el repo contiene las configuraciones client/exporter en `boards/zhihe-a210/`, `a210_netboot.yml` (arranque TFTP en memoria, a210-board-01 a 05), `a210_labgrid_uboot.yml` y `yocto-zhihe-a210.yml`, con commits del 2026-11-03 al 11-08

---

## 7. Proyectos en Gitee

Hay muy pocos repositorios de Gitee dirigidos directamente a la A210, y **la API de búsqueda interna de Gitee devuelve vacío para cualquier palabra clave ahora mismo**, así que esta sección **no garantiza ser exhaustiva**:

- [agiros/yolov5_torq_camera](https://gitee.com/agiros/yolov5_torq_camera) — su descripción original dice «pensado principalmente para la placa A210: permite llamar a un modelo yolov5 mediante torq y publicar el resultado del reconocimiento y la imagen como temas de AGIROS». Ojo: el README sigue siendo la plantilla por defecto de Gitee
- [agiros/ur5-demo](https://gitee.com/agiros/ur5-demo) — es el repositorio que se clona con `git clone` en el tutorial de brazo robótico A210 de AGIROS, para hacer captura visual con UR5 sobre A210 + openEuler 24.03; el repositorio en sí no menciona la A210, es un caso de «lo usa realmente un proyecto A210»

> Trampa: buscar «a210» devuelve sobre todo proyectos de la **K210** de Canaan; `gitee.com/zhihe` es una cuenta personal de «知和先生», sin relación con Zhihe Computing.

---

## 8. Vídeos

**Bilibili (solo hay 4 en todo el sitio, y solo uno se llama Melon Pi)**

- [Prueba de la placa de desarrollo Zhihe XuanTie A210 Melon Pi](https://www.bilibili.com/video/BV1wdx969Exj/) · donatello1996 · 2026-11-04 · unas 34 reproducciones — un clip de 21 segundos: dos paneles de matriz de LED muestran temperatura, humedad, presión y estado de gestos, además de una animación de una cara; **la placa nunca aparece en imagen**, así que lo único que indica que es la A210 es el título y las etiquetas (RISC-V, XuanTie, placa de desarrollo). El primer vídeo de Bilibili con Melon Pi en el título
- [Soluciones de robótica inteligente basadas en A210 x AGIROS](https://www.bilibili.com/video/BV12KFKzkELG/) · comunidad open source AGIROS · 2026-02-02 · unas 62 reproducciones — parte 5 del AGIROS Meetup de Pekín; el ponente, Shen Zhuang, es ingeniero sénior de IA en Zhihe Computing Technology (Hangzhou); **el único vídeo hasta ahora en el que un ingeniero en activo de Zhihe habla del A210** (14 min 10 s), sobre la solución y no sobre cifras de benchmark
- [Unboxing de la placa de desarrollo Zhihe Computing Archimedes A210 RISC-V: núcleo XuanTie C920 + NPU con cómputo e inferencia integrados](https://www.bilibili.com/video/BV1fJrnBsENd/) · DSOE1024 · 2026-01-14 · unas 1.7k reproducciones — **el único vídeo de unboxing de esta placa** (2 min 48 s)
- [Llega el Zhihe Computing A210: el caso modélico del ciclo «industria-universidad-investigación» y la A600 a la vista](https://www.bilibili.com/video/BV19R84zsEVH/) · 石榴派-袁德俊 · 2025-07-26 · 428 reproducciones — comentario de las noticias de la cumbre, no una prueba de la placa

**YouTube (solo hay 1, y es un listado de especificaciones más una guía de compra)**

- [Struggling with local AI projects? This RISC-V dev kit might help](https://www.youtube.com/watch?v=yK5x93THqLE) · 스마트직구연구소 — la descripción indica Sipeed ZHIHE A210 RISC-V AI Dev Kit; el contenido es un listado de especificaciones, no una prueba real

**No hay tutoriales, no hay registros de desarrollo, no hay grabación de presentación**. Zhihe Computing no tiene cuenta oficial ni en Bilibili ni en YouTube. Este es el estado real de esta placa hoy, sin adornos.

---

## 9. Tutoriales, prácticas y reportajes en chino

- [AGIROS + RISC-V en la Zhihe A210: pila completa funcionando y verificada en hardware](https://ruyisdk.cn/t/topic/2362) — **el artículo práctico en chino más completo hasta ahora**: grabar openEuler 24.03 LTS (incluida la contraseña de root `openEuler12#$`), red e IP estática, instalación de AGIROS 25.12 en un paso, ur5-moveit-demo, calibración mano-ojo y captura real con un UR5
- [Unboxing de la placa de desarrollo Zhihe Computing A210 (republicación del vídeo)](https://ruyisdk.cn/t/topic/2412) — entrada breve, para ver el aspecto y la disposición de los conectores
- [Placa base de código abierto XuanTie MelonPi A210 SODIMM V3](https://p.eda.cn/d-1389550606774960128) — el artículo más útil del lado del hardware (incluye 22 descripciones de conectores, BOOT_SEL, PCIe RC/EP, UART4)
- Comunidad de desarrolladores de Alibaba Cloud: [enunciado del 2.º concurso nacional CIE de innovación y aplicaciones RISC-V de alto nivel](https://developer.aliyun.com/article/1749897) — el problema 1 es «aplicación de agente de visión en el borde con A210» y exige expresamente basarse en la A210 (NPU de 12 TOPS) y en la imagen oficial de Debian para hacer captura de imagen + YOLOv5/v8 en el dispositivo + diálogo con un modelo grande en la nube. **Si buscas un proyecto para practicar con la A210, basta con seguir este enunciado**
- Artículo largo en Weibo: [XuanTie en la práctica: «poner a funcionar» en líneas de producción, robots y cómputo en el borde](https://weibo.com/ttarticle/x/m/geoshow/id/2309405355143666729355) — cifras medidas poco habituales: MobileNetV2 847 FPS, YOLOv8n 336 FPS, inferencia local de Qwen3-4B a 19 token/s; además, soluciones de AI NAS, puerta de enlace en el borde de 16 canales 1080P, barra de cómputo de 12 TOPS y tarjeta PCIe de 48 TOPS con 4 A210 interconectadas
- [Zhihe Computing te espera en AICC2025](https://mp.weixin.qq.com/s/e11WDCFZoI5CtObrTIFO5g) — el único artículo de la cuenta oficial que menciona la A210; es solo el anuncio de un evento, sin contenido técnico

**Reportajes en inglés**

- CNX Software [Zhihe A210 octa-core RISC-V SoC with 12 TOPS NPU powers SoM-based development board](https://www.cnx-software.com/2026/06/17/zhihe-a210-octa-core-risc-v-soc-with-12-tops-npu-powers-som-based-development-board/) — el reportaje en inglés más completo
- CNX Software [Three high-performance RISC-V processors to watch in H2 2025](https://www.cnx-software.com/2025/07/22/three-high-performance-risc-v-processors-to-watch-in-h2-2025-ultrarisc-ur-dp1000-zizhe-a210-and-spacemit-k3/) — la primera vez que la A210 apareció en el panorama internacional
- OMG! Ubuntu [New RVA23 RISC-V chips are coming sooner than you think](https://www.omgubuntu.co.uk/2025/07/ubuntu-risc-v-rva23-hardware-coming-soon) — ojo: su afirmación sobre RVA23 choca con la corrección de CNX (véase la sección 1)

> Lo que no se pudo incluir: CSDN, Zhihu, `bbs.21ic.com` y `eefocus.com` devuelven 521 / 403 / páginas de captcha desde la red de esta máquina, así que su contenido no se puede verificar y no se ha recogido ningún enlace suyo. El artículo sobre AGIROS de `x-techcon.com` ya da 404 (el mismo contenido está en la entrada de ruyisdk). La ruta de la imagen A210 de openEuler `images.oerv.ac.cn/.../zhihe/a210-dev/` devuelve 404 en la práctica; si quieres usarla, confírmalo por los canales oficiales del SIG RISC-V de openEuler.

---

## 10. Dónde comprarla

- **Tienda empresarial de Kubuds (苦芽科技) en Taobao**: https://item.taobao.com/item.htm?id=1034868327078&skuId=6052940225420 — para ver la ficha del producto hay que iniciar sesión en Taobao; el enlace en sí devuelve 200
- Un tercero en AliExpress (chipboard store) la anuncia como «Sipeed ZHIHE A210», configuración de 8GB/64GB por unos $334 (la página lleva a un muro de inicio de sesión, así que el precio es solo orientativo)
- Zhihe Computing no tiene página pública de venta directa ni de precios

---

## 11. Antes de empezar

1. **Confirma el modelo y la versión**: SODIMM V1 / V2 / V3 o barra de cómputo; la placa base cambia la secuencia de teclas para grabar, la alimentación y los conectores, y **las guías de grabación están separadas por modelo**.
2. **Solo hay dos imágenes** (Buildroot / Debian de escritorio), ambas con el nombre `a210-evb`; no hay Ubuntu oficial. Para revertir, usa el par 2.8.1.
3. **La placa base V2 se alimenta con 12V DC**, el módulo en sí es 5V/5A; el puerto serie de depuración es **UART4**, a 115200.
4. **No conectes la placa base en caliente** y toma precauciones antiestáticas; el modo de arranque se ajusta con las resistencias de pull de BOOT_SEL y el PCIe tiene conmutación RC/EP.
5. `wip` en la matriz de soporte no significa que se pueda usar; si tienes problemas de árbol de dispositivos o de controladores, incluye modelo de placa, imagen y versión de kernel, y el log completo del puerto serie.

---

## 12. Cómo se mantiene este índice

- Cada día a las 13:00 se ejecuta un barrido incremental de toda la web (nuevas versiones en el repositorio oficial de artefactos, nuevas páginas de documentación, nuevos vídeos, nuevos repositorios); si hay cambios, se actualiza
- Solo se recogen enlaces **que abren**; en cada actualización se comprueba la totalidad de los enlaces y los enlaces muertos se retiran o se sustituyen por una dirección nueva
- En los vídeos se exige que realmente se filme una A210; en los proyectos, que el repositorio contenga de verdad árboles de dispositivos, ramas o BSP de la A210 (no solo una mención)
- Aparecer aquí no es un aval. Juzga por tu cuenta las compilaciones de terceros, las licencias y el estado de mantenimiento
- Si falta algo, abre un issue / PR indicando la fuente original, el modelo de placa aplicable y la fecha de consulta

[Volver al índice de idiomas](README.md)
