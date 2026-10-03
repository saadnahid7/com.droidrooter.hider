<div align="center">

# Android ID and Emulator Hider

**Suplanta la identidad del dispositivo. Oculta el root y Xposed. Supera la verificación.**

Un módulo Xposed/LSPosed, de [DroidRooter](https://droidrooter.com).

[![Release](https://img.shields.io/github/v/release/saadnahid7/com.droidrooter.hider?style=for-the-badge&color=teal)](https://github.com/saadnahid7/com.droidrooter.hider/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/saadnahid7/com.droidrooter.hider/total?style=for-the-badge&color=violet)](https://github.com/saadnahid7/com.droidrooter.hider/releases)
[![Android](https://img.shields.io/badge/Android-8%20to%2016-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#compatibilidad)
[![Xposed API](https://img.shields.io/badge/libxposed%20API-102-orange?style=for-the-badge)](https://github.com/libxposed/api)

[![DroidRooter](https://img.shields.io/badge/DroidRooter-droidrooter.com-2F6BFF?style=for-the-badge)](https://droidrooter.com)
[![Telegram](https://img.shields.io/badge/Telegram-@DroidRooter-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/DroidRooter)
[![Facebook](https://img.shields.io/badge/Facebook-DroidRooter-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://www.facebook.com/droidrooter)

**Leer en otros idiomas:** [English](README.md) · [العربية](README.ar.md) · [Deutsch](README.de.md) · [日本語](README.ja.md) · [简体中文](README.zh-hans.md) · [Français](README.fr.md) · [Italiano](README.it.md)

</div>

---

## Por qué Android ID and Emulator Hider

Muchas apps se niegan a funcionar, o se limitan en silencio, en cuanto creen
que el dispositivo es un emulador, está rooteado o corre un framework de
hooks. Este módulo cambia lo que ven esas comprobaciones —tanto en la capa
Java como en la nativa— para que la app se comporte como lo haría en un
teléfono de fábrica sin modificar.

- Elige entre **12 perfiles de dispositivos reales** (Pixel, Galaxy, POCO,
  OnePlus, Redmi, Nothing), cada uno construido a partir de una asignación
  IMEI verificada de GSMA y una huella de compilación de fábrica real, no
  valores inventados.
- Activa o desactiva cada protección de forma independiente, por app, desde
  una sola pantalla.
- Ejecuta **Device Check** para ver, en vivo, exactamente lo que una app de
  verificación leería de tu dispositivo ahora mismo.

El enmascaramiento principal es gratuito, siempre. Una compra única desbloquea
perfiles personalizados, modo seguro y algunos identificadores adicionales —
consulta **Unlock Pro** dentro de la app.

## Qué cubre

| Protección | Qué cambia |
|---|---|
| Identidad del dispositivo | Modelo, marca, fabricante, fingerprint, propiedades de compilación, Android ID, número de serie |
| Rastros de emulador | Propiedades qemu/goldfish, archivos, nombres de drivers del kernel, `/proc/mounts` |
| Procesador | Lista de ABI, `os.arch`, y el string crudo de vendor/modelo en `/proc/cpuinfo` (hosts x86) |
| Gráficos | Fabricante y string de renderizado de la GPU |
| Sensores | Nombres y fabricantes de los sensores |
| Batería | Nivel, estado de salud, estado, capacidad, valores de sysfs |
| Dispositivos de entrada | Nombres de dispositivos, `/proc/bus/input/devices` |
| Radio del teléfono | IMEI, IMSI, operador/país de la SIM, número de línea, versión de banda base |
| Cámara | Número de cámaras y orientación (frontal/trasera), por ID de cámara |
| Ubicación | Respuesta alternativa para apps que consultan la última ubicación conocida y no reciben nada |
| Root | `su`, Magisk, KernelSU y binarios/rutas relacionados; `ro.debuggable`/`ro.secure` |
| Xposed | Rastros de LSPosed/Vector en `/proc/self/maps`, el gestor de paquetes, logcat |

## Requisitos

- Un dispositivo rooteado con un framework compatible con LSPosed que soporte
  la moderna **libxposed API 102**, como [LSPosed](https://github.com/LSPosed/LSPosed)
  o [Vector](https://github.com/JingMatrix/Vector).
- Android 8.0 o superior.

> [!IMPORTANT]
> Este módulo está construido sobre la libxposed API moderna. El Xposed
> clásico y EdXposed no son compatibles.

## Instalación

1. Descarga el último APK desde [Releases](../../releases/latest) e instálalo.
2. Abre tu gestor de Xposed, activa **Android ID and Emulator Hider** y
   añádelo al scope — **necesita estar en su propio scope** para proteger su
   propia pantalla de Device Check, además de cualquier app que quieras
   proteger.
3. Fuerza el cierre y vuelve a abrir cada app que hayas incluido en el scope.

## Uso

1. Abre la app. La tarjeta de estado en la parte superior dice **Protected**
   en cuanto el framework ha enganchado el proceso.
2. Elige un perfil de dispositivo — Pixel 8, Galaxy S24, POCO X3 Pro, y otros
   nueve.
3. Activa o desactiva protecciones individuales en **Protection**.
4. Pulsa **Device Check** para ver exactamente lo que leería una app de
   verificación — propiedades de compilación, fingerprint, CPU, sensores,
   batería— comparado con el perfil activo, en vivo.

## Compatibilidad

| Android | API | Estado |
|---|---|---|
| 16 | 36 | Verificado en dispositivo real |
| 15 | 35 | Verificado en dispositivo real |
| 14 | 34 | Verificado en dispositivo real y emulador |
| 13 | 33 | Verificado en dispositivo real |
| 12 e inferior | 31 e inferior | Soportado (minSdk 26), no verificado de forma independiente |

"Verificado" significa que el módulo se instaló, se incluyó en el scope y se
confirmó activo (los hooks se disparan, sin fallos) en esa versión de Android
durante el desarrollo.

## Preguntas frecuentes

**¿Hace que un dispositivo real parezca un emulador, o un emulador parezca un
dispositivo real?**
Ambas cosas. El enmascaramiento se basa en la identidad, no en el entorno —
cambia lo que reportan las APIs Java/nativas, sin importar lo que realmente
esté corriendo debajo.

**¿Esto evade Play Integrity o SafetyNet?**
No. La atestación por hardware está respaldada por el TEE/StrongBox del
dispositivo y está fuera del alcance de un hook de Xposed en espacio de
usuario — eso necesita un enfoque completamente distinto y dedicado.

**¿Por qué necesito incluir la app en su propio scope?**
Sin eso, el propio proceso de la app nunca se engancha, así que su pantalla
de Device Check mostraría los valores reales de tu dispositivo en lugar de
los del perfil activo — dando una lectura falsa precisamente en la función
pensada para verificar el enmascaramiento.

**¿Puedo usar un perfil que no coincide con el hardware real de mi teléfono
(por ejemplo, un perfil ARM en un emulador x86)?**
Sí — cada perfil enmascara el procesador, así que Build.SUPPORTED_ABIS,
`os.arch` y el string crudo de vendor de `/proc/cpuinfo` cambian todos para
coincidir con el perfil, no con el host.

## Límites

- Cualquier cosa que no pase por una API Java/nativa enganchada —sockets
  crudos, comprobaciones del lado del servidor, atestación por hardware— ve
  el dispositivo real.
- Los cambios se aplican la próxima vez que se inicie una app protegida; una
  app ya en ejecución necesita reiniciarse.
- Este repositorio solo aloja releases. El código fuente es cerrado.

## Aviso legal

Este módulo está pensado para privacidad, pruebas y compatibilidad con tus
propias apps. Eres responsable de cómo lo uses. No lo utilices para romper
los términos de una app, evadir servicios de pago o defraudar a nadie. El
software se proporciona tal cual, sin garantía.

## Agradecimientos

- [libxposed](https://github.com/libxposed) por la API moderna de Xposed y la
  librería de servicio.
- [LSPosed](https://github.com/LSPosed/LSPosed) y
  [Vector](https://github.com/JingMatrix/Vector) por los frameworks sobre los
  que corre.

## Desde DroidRooter

Android ID and Emulator Hider es un proyecto de **DroidRooter**, un pequeño
equipo que construye herramientas para Android rooteado.

- **Sitio web:** [droidrooter.com](https://droidrooter.com)
- **Telegram:** [@DroidRooter](https://t.me/DroidRooter)
- **Facebook:** [facebook.com/droidrooter](https://www.facebook.com/droidrooter)
- **DRVCAM, la cámara virtual de DroidRooter:**
  [droidrooter.com/drvcam](https://www.droidrooter.com/drvcam/) envía tu
  propio video o imágenes a las apps en lugar de la cámara.
- **VirtualNet, el suplantador de red por app de DroidRooter:**
  cambia lo que las apps conocen sobre tu conexión Wi-Fi/datos móviles, código
  abierto.
- **Smali Patcher Reborn:** parchea `services.jar` de tu ROM en el propio
  dispositivo (Magisk/KernelSU/APatch) para ubicación simulada y ventanas
  seguras, Android 10–17 — sucesor de Smali Patcher / SmaliPatcherEx.

Si esta app te resulta útil, sigue a DroidRooter para más.

## Licencia

Propietaria — todos los derechos reservados. Distribución solo en binario; el
código fuente no se publica.
