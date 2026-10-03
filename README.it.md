<div align="center">

# Android ID and Emulator Hider

**Falsifica l'identità del dispositivo. Nasconde root e Xposed. Supera il controllo.**

Un modulo Xposed/LSPosed, di [DroidRooter](https://droidrooter.com).

[![Release](https://img.shields.io/github/v/release/saadnahid7/com.droidrooter.hider?style=for-the-badge&color=teal)](https://github.com/saadnahid7/com.droidrooter.hider/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/saadnahid7/com.droidrooter.hider/total?style=for-the-badge&color=violet)](https://github.com/saadnahid7/com.droidrooter.hider/releases)
[![Android](https://img.shields.io/badge/Android-8%20to%2016-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#compatibilita)
[![Xposed API](https://img.shields.io/badge/libxposed%20API-102-orange?style=for-the-badge)](https://github.com/libxposed/api)

[![DroidRooter](https://img.shields.io/badge/DroidRooter-droidrooter.com-2F6BFF?style=for-the-badge)](https://droidrooter.com)
[![Telegram](https://img.shields.io/badge/Telegram-@DroidRooter-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/DroidRooter)
[![Facebook](https://img.shields.io/badge/Facebook-DroidRooter-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://www.facebook.com/droidrooter)

**Leggi in altre lingue:** [English](README.md) · [Español](README.es.md) · [العربية](README.ar.md) · [Deutsch](README.de.md) · [日本語](README.ja.md) · [简体中文](README.zh-hans.md) · [Français](README.fr.md)

</div>

---

## Perché Android ID and Emulator Hider

Molte app si rifiutano di funzionare, o si limitano silenziosamente, non
appena pensano che il dispositivo sia un emulatore, rootato o che esegua un
framework di hook. Questo modulo cambia ciò che quei controlli vedono — sia a
livello Java che nativo — così l'app si comporta come farebbe su un telefono
di serie non modificato.

- Scegli tra **12 profili di dispositivi reali** (Pixel, Galaxy, POCO,
  OnePlus, Redmi, Nothing), ciascuno costruito a partire da un'allocazione
  IMEI GSMA verificata e da un fingerprint di build di fabbrica reale — non
  valori inventati.
- Attiva ogni protezione in modo indipendente, per app, da un'unica schermata.
- Esegui **Device Check** per vedere, in tempo reale, esattamente ciò che
  un'app di verifica leggerebbe dal tuo dispositivo in questo momento.

La mascheratura di base è sempre gratuita. Un acquisto unico sblocca profili
personalizzati, safe mode e alcuni identificatori aggiuntivi — vedi **Unlock
Pro** nell'app.

## Cosa copre

| Protezione | Cosa cambia |
|---|---|
| Identità del dispositivo | Modello, marca, produttore, fingerprint, proprietà di build, Android ID, numero di serie |
| Tracce dell'emulatore | Proprietà qemu/goldfish, file, nomi dei driver del kernel, `/proc/mounts` |
| Processore | Elenco ABI, `os.arch`, e la stringa grezza vendor/modello in `/proc/cpuinfo` (host x86) |
| Grafica | Produttore della GPU e stringa di rendering |
| Sensori | Nomi e produttori dei sensori |
| Batteria | Livello, stato di salute, stato, capacità, valori sysfs |
| Dispositivi di input | Nomi dei dispositivi, `/proc/bus/input/devices` |
| Radio del telefono | IMEI, IMSI, operatore/paese SIM, numero di linea, versione banda base |
| Fotocamera | Numero di fotocamere e orientamento (anteriore/posteriore), per ID fotocamera |
| Posizione | Risposta di riserva per le app che richiedono l'ultima posizione nota e non ricevono nulla |
| Root | `su`, Magisk, KernelSU e binari/percorsi correlati; `ro.debuggable`/`ro.secure` |
| Xposed | Tracce LSPosed/Vector in `/proc/self/maps`, package manager, logcat |

## Requisiti

- Un dispositivo rootato con un framework compatibile con LSPosed che
  supporti la moderna **libxposed API 102**, come
  [LSPosed](https://github.com/LSPosed/LSPosed) o
  [Vector](https://github.com/JingMatrix/Vector).
- Android 8.0 o successivo.

> [!IMPORTANT]
> Questo modulo è basato sulla moderna libxposed API. Xposed classico ed
> EdXposed non sono supportati.

## Installazione

1. Scarica l'ultimo APK da [Releases](../../releases/latest) e installalo.
2. Apri il tuo gestore Xposed, attiva **Android ID and Emulator Hider** e
   aggiungilo allo scope — **deve includere se stesso nello scope** per
   proteggere la propria schermata Device Check, oltre a qualsiasi app che
   vuoi proteggere.
3. Forza l'arresto e riapri ogni app inclusa nello scope.

## Utilizzo

1. Apri l'app. La scheda di stato in alto mostra **Protected** non appena il
   framework ha agganciato il processo.
2. Scegli un profilo di dispositivo — Pixel 8, Galaxy S24, POCO X3 Pro e
   altri nove.
3. Attiva o disattiva le singole protezioni in **Protection**.
4. Tocca **Device Check** per vedere esattamente cosa leggerebbe un'app di
   verifica — proprietà di build, fingerprint, CPU, sensori, batteria —
   confrontato con il profilo attivo, in tempo reale.

## Compatibilità

| Android | API | Stato |
|---|---|---|
| 16 | 36 | Verificato su dispositivo reale |
| 15 | 35 | Verificato su dispositivo reale |
| 14 | 34 | Verificato su dispositivo reale ed emulatore |
| 13 | 33 | Verificato su dispositivo reale |
| 12 e inferiori | 31 e inferiori | Supportato (minSdk 26), non verificato in modo indipendente |

"Verificato" significa che il modulo è stato installato, incluso nello scope
e confermato attivo (gli hook scattano, senza crash) su quella versione di
Android durante lo sviluppo.

## FAQ

**Fa sembrare un dispositivo reale un emulatore, o un emulatore un
dispositivo reale?**
Entrambi. La mascheratura è basata sull'identità, non sull'ambiente — cambia
ciò che le API Java/native riportano, indipendentemente da cosa sta
realmente girando sotto.

**Questo bypassa Play Integrity o SafetyNet?**
No. L'attestazione hardware è garantita dal TEE/StrongBox del dispositivo ed
è fuori portata per un hook Xposed in userspace — serve un approccio
separato e dedicato.

**Perché devo includere l'app nel proprio scope?**
Senza, il processo dell'app stessa non viene mai agganciato, quindi la sua
schermata Device Check mostrerebbe i valori reali del tuo dispositivo invece
di quelli del profilo attivo — falsando proprio la funzione pensata per
verificare la mascheratura.

**Posso usare un profilo che non corrisponde all'hardware reale del mio
telefono (ad esempio un profilo ARM su un emulatore x86)?**
Sì — ogni profilo maschera il processore, quindi Build.SUPPORTED_ABIS,
`os.arch` e la stringa grezza del vendor in `/proc/cpuinfo` passano tutti al
profilo, non all'host.

## Limiti

- Tutto ciò che non passa attraverso un'API Java/nativa agganciata — socket
  grezzi, controlli lato server, attestazione hardware — vede il dispositivo
  reale.
- Le modifiche si applicano al prossimo avvio di un'app protetta; un'app già
  in esecuzione deve essere riavviata.
- Questo repository ospita solo le release. Il codice sorgente è chiuso.

## Avvertenza

Questo modulo è pensato per privacy, test e compatibilità con le tue app. Sei
responsabile di come lo usi. Non usarlo per violare i termini di un'app,
aggirare servizi a pagamento o frodare qualcuno. Il software è fornito così
com'è, senza garanzia.

## Ringraziamenti

- [libxposed](https://github.com/libxposed) per la moderna API Xposed e la
  libreria di servizio.
- [LSPosed](https://github.com/LSPosed/LSPosed) e
  [Vector](https://github.com/JingMatrix/Vector) per i framework su cui
  gira.

## Da DroidRooter

Android ID and Emulator Hider è un progetto di **DroidRooter**, un piccolo
team che costruisce strumenti per Android rootato.

- **Sito web:** [droidrooter.com](https://droidrooter.com)
- **Telegram:** [@DroidRooter](https://t.me/DroidRooter)
- **Facebook:** [facebook.com/droidrooter](https://www.facebook.com/droidrooter)
- **DRVCAM, la fotocamera virtuale di DroidRooter:**
  [droidrooter.com/drvcam](https://www.droidrooter.com/drvcam/) invia il tuo
  video o le tue immagini alle app al posto della fotocamera.
- **VirtualNet, lo spoofer di rete per app di DroidRooter:**
  cambia ciò che le app sanno della tua connessione Wi-Fi/dati mobili, open
  source.
- **Smali Patcher Reborn:** applica patch al `services.jar` della tua ROM
  direttamente sul dispositivo (Magisk/KernelSU/APatch) per posizione
  simulata e finestre sicure, Android 10–17 — successore di Smali Patcher /
  SmaliPatcherEx.

Se questa app ti è utile, segui DroidRooter per saperne di più.

## Licenza

Proprietaria — tutti i diritti riservati. Distribuzione solo in formato
binario; il codice sorgente non è pubblicato.
