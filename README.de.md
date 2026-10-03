<div align="center">

# Android ID and Emulator Hider

**Täuscht die Geräteidentität vor. Versteckt Root und Xposed. Besteht die Prüfung.**

Ein Xposed/LSPosed-Modul von [DroidRooter](https://droidrooter.com).

[![Release](https://img.shields.io/github/v/release/saadnahid7/com.droidrooter.hider?style=for-the-badge&color=teal)](https://github.com/saadnahid7/com.droidrooter.hider/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/saadnahid7/com.droidrooter.hider/total?style=for-the-badge&color=violet)](https://github.com/saadnahid7/com.droidrooter.hider/releases)
[![Android](https://img.shields.io/badge/Android-8%20to%2016-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#kompatibilitat)
[![Xposed API](https://img.shields.io/badge/libxposed%20API-102-orange?style=for-the-badge)](https://github.com/libxposed/api)

[![DroidRooter](https://img.shields.io/badge/DroidRooter-droidrooter.com-2F6BFF?style=for-the-badge)](https://droidrooter.com)
[![Telegram](https://img.shields.io/badge/Telegram-@DroidRooter-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/DroidRooter)
[![Facebook](https://img.shields.io/badge/Facebook-DroidRooter-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://www.facebook.com/droidrooter)

**In anderen Sprachen lesen:** [English](README.md) · [Español](README.es.md) · [العربية](README.ar.md) · [日本語](README.ja.md) · [简体中文](README.zh-hans.md) · [Français](README.fr.md) · [Italiano](README.it.md)

</div>

---

## Warum Android ID and Emulator Hider

Viele Apps verweigern den Dienst oder schränken sich still ein, sobald sie
glauben, das Gerät sei ein Emulator, gerootet oder laufe mit einem
Hook-Framework. Dieses Modul ändert, was diese Prüfungen sehen — sowohl auf
Java- als auch auf nativer Ebene —, sodass sich die App so verhält, als liefe
sie auf einem unveränderten Serientelefon.

- Wähle aus **12 echten Geräteprofilen** (Pixel, Galaxy, POCO, OnePlus, Redmi,
  Nothing), jedes basierend auf einer verifizierten GSMA-IMEI-Zuteilung und
  einem echten Werks-Build-Fingerprint — keine erfundenen Werte.
- Schalte jeden Schutz unabhängig, pro App, auf einem einzigen Bildschirm um.
- Führe **Device Check** aus, um live zu sehen, was eine prüfende App gerade
  jetzt von deinem Gerät lesen würde.

Die grundlegende Maskierung ist immer kostenlos. Ein einmaliger Kauf schaltet
individuelle Profile, den Safe Mode und einige zusätzliche Kennungen frei —
siehe **Unlock Pro** in der App.

## Was abgedeckt wird

| Schutz | Was geändert wird |
|---|---|
| Geräteidentität | Modell, Marke, Hersteller, Fingerprint, Build-Eigenschaften, Android-ID, Seriennummer |
| Emulator-Spuren | qemu/goldfish-Eigenschaften, Dateien, Kernel-Treibernamen, `/proc/mounts` |
| Prozessor | ABI-Liste, `os.arch`, und der rohe Hersteller-/Modellstring in `/proc/cpuinfo` (x86-Hosts) |
| Grafik | GPU-Hersteller und Renderer-String |
| Sensoren | Sensornamen und -hersteller |
| Akku | Ladestand, Zustand, Status, Kapazität, sysfs-Werte |
| Eingabegeräte | Gerätenamen, `/proc/bus/input/devices` |
| Telefon-Funkmodul | IMEI, IMSI, SIM-Betreiber/-Land, Rufnummer, Basisbandversion |
| Kamera | Anzahl der Kameras und Ausrichtung (vorne/hinten), pro Kamera-ID |
| Standort | Fallback für Apps, die den letzten bekannten Standort abfragen und nichts zurückbekommen |
| Root | `su`, Magisk, KernelSU und zugehörige Binärdateien/Pfade; `ro.debuggable`/`ro.secure` |
| Xposed | LSPosed/Vector-Spuren in `/proc/self/maps`, Paketmanager, Logcat |

## Voraussetzungen

- Ein gerootetes Gerät mit einem LSPosed-kompatiblen Framework, das die
  moderne **libxposed API 102** unterstützt, wie
  [LSPosed](https://github.com/LSPosed/LSPosed) oder
  [Vector](https://github.com/JingMatrix/Vector).
- Android 8.0 oder neuer.

> [!IMPORTANT]
> Dieses Modul basiert auf der modernen libxposed API. Klassisches Xposed und
> EdXposed werden nicht unterstützt.

## Installation

1. Lade die neueste APK aus [Releases](../../releases/latest) herunter und
   installiere sie.
2. Öffne deinen Xposed-Manager, aktiviere **Android ID and Emulator Hider**
   und füge es dem Scope hinzu — **es muss sich selbst im Scope haben**, um
   seinen eigenen Device-Check-Bildschirm zu schützen, zusätzlich zu jeder App,
   die du schützen möchtest.
3. Erzwinge das Stoppen und öffne jede App im Scope erneut.

## Verwendung

1. Öffne die App. Die Statuskarte oben zeigt **Protected**, sobald das
   Framework den Prozess eingehängt hat.
2. Wähle ein Geräteprofil — Pixel 8, Galaxy S24, POCO X3 Pro und neun weitere.
3. Schalte einzelne Schutzfunktionen unter **Protection** um.
4. Tippe auf **Device Check**, um live genau zu sehen, was eine prüfende App
   lesen würde — Build-Eigenschaften, Fingerprint, CPU, Sensoren, Akku — im
   Vergleich zum aktiven Profil.

## Kompatibilität

| Android | API | Status |
|---|---|---|
| 16 | 36 | Auf echtem Gerät verifiziert |
| 15 | 35 | Auf echtem Gerät verifiziert |
| 14 | 34 | Auf echtem Gerät und Emulator verifiziert |
| 13 | 33 | Auf echtem Gerät verifiziert |
| 12 und darunter | 31 und darunter | Unterstützt (minSdk 26), nicht unabhängig verifiziert |

„Verifiziert" bedeutet, dass das Modul installiert, in den Scope
aufgenommen und als aktiv bestätigt wurde (Hooks greifen, keine Abstürze) —
auf dieser Android-Version während der Entwicklung.

## FAQ

**Lässt das ein echtes Gerät wie einen Emulator aussehen, oder einen
Emulator wie ein echtes Gerät?**
Beides. Die Maskierung basiert auf Identität, nicht auf der Umgebung — sie
ändert, was Java-/native APIs melden, unabhängig davon, was tatsächlich
darunter läuft.

**Umgeht das Play Integrity oder SafetyNet?**
Nein. Die Hardware-Attestierung basiert auf dem TEE/StrongBox des Geräts und
ist für einen Userspace-Xposed-Hook unerreichbar — dafür braucht es einen
komplett eigenen, dedizierten Ansatz.

**Warum muss ich die App in ihren eigenen Scope aufnehmen?**
Ohne das wird der eigene Prozess der App nie eingehängt, sodass ihr Device-
Check-Bildschirm die echten Werte deines Geräts statt die des aktiven
Profils anzeigen würde — und ausgerechnet die Funktion, die die Maskierung
überprüfen soll, eine falsche Ablesung liefert.

**Kann ich ein Profil verwenden, das nicht zur echten Hardware meines
Telefons passt (z. B. ein ARM-Profil auf einem x86-Emulator)?**
Ja — jedes Profil maskiert den Prozessor, sodass Build.SUPPORTED_ABIS,
`os.arch` und der rohe Herstellerstring aus `/proc/cpuinfo` alle zum Profil
wechseln, nicht zum Host.

## Grenzen

- Alles, was nicht über eine eingehängte Java-/native API läuft — rohe
  Sockets, serverseitige Prüfungen, Hardware-Attestierung — sieht das echte
  Gerät.
- Änderungen greifen beim nächsten Start einer geschützten App; eine bereits
  laufende App muss neu gestartet werden.
- Dieses Repository enthält nur Releases. Der Quellcode ist nicht öffentlich.

## Haftungsausschluss

Dieses Modul ist für Privatsphäre, Tests und Kompatibilität mit deinen
eigenen Apps gedacht. Du bist für die Nutzung selbst verantwortlich. Nutze es
nicht, um die Nutzungsbedingungen einer App zu brechen, kostenpflichtige
Dienste zu umgehen oder jemanden zu betrügen. Die Software wird ohne
Gewährleistung bereitgestellt.

## Danksagungen

- [libxposed](https://github.com/libxposed) für die moderne Xposed-API und
  Service-Bibliothek.
- [LSPosed](https://github.com/LSPosed/LSPosed) und
  [Vector](https://github.com/JingMatrix/Vector) für die Frameworks, auf
  denen es läuft.

## Von DroidRooter

Android ID and Emulator Hider ist ein Projekt von **DroidRooter**, einem
kleinen Team, das Werkzeuge für gerootetes Android entwickelt.

- **Website:** [droidrooter.com](https://droidrooter.com)
- **Telegram:** [@DroidRooter](https://t.me/DroidRooter)
- **Facebook:** [facebook.com/droidrooter](https://www.facebook.com/droidrooter)
- **DRVCAM, DroidRooters virtuelle Kamera:**
  [droidrooter.com/drvcam](https://www.droidrooter.com/drvcam/) speist dein
  eigenes Video oder Bilder anstelle der Kamera in Apps ein.
- **VirtualNet, DroidRooters App-weiser Netzwerk-Spoofer:**
  ändert, was Apps über deine WLAN-/Mobilfunkverbindung erfahren, Open
  Source.
- **Smali Patcher Reborn:** patcht die `services.jar` deiner ROM direkt auf
  dem Gerät (Magisk/KernelSU/APatch) für Standort-Simulation und sichere
  Fenster, Android 10–17 — Nachfolger von Smali Patcher / SmaliPatcherEx.

Wenn dir diese App hilft, folge DroidRooter für mehr.

## Lizenz

Proprietär — alle Rechte vorbehalten. Nur Binärdistribution; der Quellcode
wird nicht veröffentlicht.
