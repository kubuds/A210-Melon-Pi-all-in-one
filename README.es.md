# Guía de recursos de Zhihe A210 / Melon Pi

[简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [English](README.en.md) · [Русский](README.ru.md) · [日本語](README.ja.md) · [Deutsch](README.de.md) · [Español](README.es.md)

Esta guía reúne recursos públicos y verificables sobre la placa de desarrollo A210. Las páginas originales son la referencia para las especificaciones, las imágenes del sistema y el estado del soporte, y pueden cambiar. Este índice se ampliará con el tiempo; no afirma haber encontrado todos los recursos de Internet.

## Descripción de la placa

La [matriz de soporte de placas de RuyiSDK](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2) incluye la **A210 SODIMM V2** con estos datos:

| Elemento | Información de la matriz |
| --- | --- |
| Fabricante | ZHIHE COMPUTING |
| SoC | A210 |
| Núcleos de CPU | XuanTie C920 + XuanTie C908 |
| GPU | IMG BXM-4-64 |
| Configuraciones de memoria | 4 GB / 8 GB / 16 GB |

Estos datos corresponden a esa entrada de la matriz y no deben extrapolarse a otras revisiones de hardware. Comprueba las marcas y la documentación de la placa concreta.

## Recursos específicos de la placa

### Hardware y estado del sistema operativo

- [Matriz de soporte de RuyiSDK para A210 SODIMM V2](https://github.com/ruyisdk/support-matrix/tree/main/A210_SODIMM_V2): ficha de la placa y estado del proyecto.
- [Datos de hardware y procesador (README)](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/README.md): procesador, núcleos, GPU, memoria y fabricante.
- [Estado de los sistemas operativos (others.yml)](https://github.com/ruyisdk/support-matrix/blob/main/A210_SODIMM_V2/others.yml): Debian y Buildroot aparecen actualmente como `wip`; consulta el archivo para ver cambios.
- [Informe quincenal n.º 75 de RuyiSDK](https://github.com/ruyisdk/wechat-articles/blob/main/20260901-ruyisdk-biweekly-75.md): indica que el repositorio de paquetes de RuyiSDK añadió compatibilidad con la imagen oficial del sistema EVB de Zhihe A210 SODIMM. Es un anuncio, no una página de descarga; antes de usar la imagen, comprueba las instrucciones originales, la revisión de la placa y la suma de verificación.

### Desarrollo del kernel Linux y controladores

Estos cambios del repositorio RevyOS Linux mencionan explícitamente A210 / Melon Pi y sirven para seguir el desarrollo del árbol de dispositivos, los controladores y el soporte de la placa. Un commit de desarrollo no implica que todas las distribuciones sean compatibles.

- [Mantenimiento de la plataforma A210 y archivos incluidos](https://github.com/revyos/linux/commit/e214610882a3cced2e158a6824ced2543eb1195d): enumera árboles de dispositivos, bindings y directorios de controladores de A210.
- [Árbol de dispositivos de temperatura y watchdog para A210](https://github.com/revyos/linux/commit/238818df88f8387e07306305462e1b90e7b6b4a4).
- [Compatibilidad del controlador PWM con A210](https://github.com/revyos/linux/commit/dd6ce756803d76e879e9d5cbe6d5f528b8216c2d): la descripción del commit indica que reutiliza el controlador TH1520.
- [Enrutamiento de audio de Melon Pi V2](https://github.com/revyos/linux/commit/84fbce4e2eb80e7b4bbcd24b83b149beee474146).
- [Código fuente de RevyOS Linux](https://github.com/revyos/linux): rama actual, árboles de dispositivos, controladores, commits y trabajo en curso.
- [Buscar código A210 en RevyOS Linux](https://github.com/revyos/linux/search?q=A210&type=code): búsqueda en el contenido actual del repositorio.
- [Árbol de dispositivos de Melon Pi en RVCK Linux](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210-melon-pi.dts): configuración de Linux para la placa, no un manual de hardware completo.
- [Árbol de dispositivos del SoC A210 en RVCK Linux](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/arch/riscv/boot/dts/zhihe/a210.dtsi) y [binding del árbol de dispositivos de Zhihe](https://github.com/RVCK-Project/rvck/blob/rvck-6.6/Documentation/devicetree/bindings/riscv/zhihe.yaml): referencias de implementación del SoC y las cadenas compatible.
- [Incidencia de RVCK sobre periféricos de A210](https://github.com/RVCK-Project/rvck/issues/381) y [cambio combinado de soporte de periféricos](https://github.com/RVCK-Project/rvck/pull/382): debates y código sobre GPIO, temporizadores, I²C, SPI, DMA y otros periféricos. RVCK es una línea de desarrollo de Linux independiente; esto no implica que RevyOS u otros sistemas incluyan el mismo soporte.

## Antes de empezar

1. Identifica el modelo exacto, la revisión de hardware y la memoria de la placa; compartir el SoC A210 no garantiza que las placas base o revisiones sean iguales.
2. Consulta la matriz de soporte y el anuncio de la imagen para verificar la placa de destino, el estado, el medio de arranque y la suma de verificación. No grabes sin confirmar una imagen destinada a otra placa A210.
3. Sigue las instrucciones originales de instalación de la imagen concreta y guarda una copia de los datos existentes. Esta guía no valida comandos de grabación ni archivos de imagen específicos.
4. Al informar de problemas con el árbol de dispositivos, los controladores o el arranque, incluye la revisión de la placa, las versiones de la imagen y del kernel, los registros completos y los enlaces de referencia.

## Alcance y contribuciones

Los recursos públicos específicos de A210 que se pueden verificar actualmente se encuentran principalmente en la matriz de soporte y en el historial de desarrollo de RevyOS Linux. No se inventan manuales oficiales, esquemas, tablas de pines, direcciones de descarga ni contactos comunitarios que no se hayan podido confirmar. Se agradecen las contribuciones: incluye la fuente original, la revisión de hardware aplicable, la fecha de consulta y, si está disponible, la suma de verificación y la licencia.
