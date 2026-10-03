<div align="center">

# Android ID and Emulator Hider

**Usurpe l'identité de l'appareil. Masque le root et Xposed. Passe la vérification.**

Un module Xposed/LSPosed, par [DroidRooter](https://droidrooter.com).

[![Release](https://img.shields.io/github/v/release/saadnahid7/com.droidrooter.hider?style=for-the-badge&color=teal)](https://github.com/saadnahid7/com.droidrooter.hider/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/saadnahid7/com.droidrooter.hider/total?style=for-the-badge&color=violet)](https://github.com/saadnahid7/com.droidrooter.hider/releases)
[![Android](https://img.shields.io/badge/Android-8%20to%2016-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#compatibilite)
[![Xposed API](https://img.shields.io/badge/libxposed%20API-102-orange?style=for-the-badge)](https://github.com/libxposed/api)

[![DroidRooter](https://img.shields.io/badge/DroidRooter-droidrooter.com-2F6BFF?style=for-the-badge)](https://droidrooter.com)
[![Telegram](https://img.shields.io/badge/Telegram-@DroidRooter-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/DroidRooter)
[![Facebook](https://img.shields.io/badge/Facebook-DroidRooter-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://www.facebook.com/droidrooter)

**Lire dans d'autres langues :** [English](README.md) · [Español](README.es.md) · [العربية](README.ar.md) · [Deutsch](README.de.md) · [日本語](README.ja.md) · [简体中文](README.zh-hans.md) · [Italiano](README.it.md)

</div>

---

## Pourquoi Android ID and Emulator Hider

De nombreuses applications refusent de fonctionner, ou se limitent
discrètement, dès qu'elles pensent que l'appareil est un émulateur, rooté, ou
qu'il exécute un framework de hooks. Ce module change ce que voient ces
vérifications — à la fois au niveau Java et natif — pour que l'application se
comporte comme sur un téléphone de série non modifié.

- Choisissez parmi **12 profils d'appareils réels** (Pixel, Galaxy, POCO,
  OnePlus, Redmi, Nothing), chacun construit à partir d'une allocation IMEI
  GSMA vérifiée et d'une empreinte de build d'usine réelle — pas de valeurs
  inventées.
- Activez chaque protection indépendamment, par application, depuis un seul
  écran.
- Lancez **Device Check** pour voir, en direct, exactement ce qu'une
  application de vérification lirait sur votre appareil en ce moment.

Le masquage de base est gratuit, toujours. Un achat unique débloque des
profils personnalisés, le mode sécurisé et quelques identifiants
supplémentaires — voir **Unlock Pro** dans l'application.

## Ce qui est couvert

| Protection | Ce qui change |
|---|---|
| Identité de l'appareil | Modèle, marque, fabricant, fingerprint, propriétés de build, Android ID, numéro de série |
| Traces d'émulateur | Propriétés qemu/goldfish, fichiers, noms de pilotes du noyau, `/proc/mounts` |
| Processeur | Liste des ABI, `os.arch`, et la chaîne brute vendeur/modèle de `/proc/cpuinfo` (hôtes x86) |
| Graphismes | Fabricant du GPU et chaîne de rendu |
| Capteurs | Noms et fabricants des capteurs |
| Batterie | Niveau, état de santé, statut, capacité, valeurs sysfs |
| Périphériques d'entrée | Noms des périphériques, `/proc/bus/input/devices` |
| Radio téléphonique | IMEI, IMSI, opérateur/pays de la SIM, numéro de ligne, version du modem |
| Caméra | Nombre de caméras et orientation (avant/arrière), par ID de caméra |
| Localisation | Réponse de secours pour les applications qui demandent la dernière position connue et n'obtiennent rien |
| Root | `su`, Magisk, KernelSU et binaires/chemins associés ; `ro.debuggable`/`ro.secure` |
| Xposed | Traces LSPosed/Vector dans `/proc/self/maps`, le gestionnaire de paquets, logcat |

## Prérequis

- Un appareil rooté avec un framework compatible LSPosed prenant en charge la
  **libxposed API 102** moderne, comme [LSPosed](https://github.com/LSPosed/LSPosed)
  ou [Vector](https://github.com/JingMatrix/Vector).
- Android 8.0 ou supérieur.

> [!IMPORTANT]
> Ce module est construit sur la libxposed API moderne. Le Xposed classique
> et EdXposed ne sont pas pris en charge.

## Installation

1. Téléchargez le dernier APK depuis [Releases](../../releases/latest) et
   installez-le.
2. Ouvrez votre gestionnaire Xposed, activez **Android ID and Emulator
   Hider**, et ajoutez-le au scope — **il doit s'inclure lui-même dans le
   scope** pour protéger son propre écran Device Check, en plus de toute
   application que vous souhaitez protéger.
3. Forcez l'arrêt puis rouvrez chaque application incluse dans le scope.

## Utilisation

1. Ouvrez l'application. La carte de statut en haut affiche **Protected** dès
   que le framework a accroché le processus.
2. Choisissez un profil d'appareil — Pixel 8, Galaxy S24, POCO X3 Pro, et neuf
   autres.
3. Activez ou désactivez chaque protection sous **Protection**.
4. Appuyez sur **Device Check** pour voir exactement ce qu'une application de
   vérification lirait — propriétés de build, fingerprint, CPU, capteurs,
   batterie — comparé au profil actif, en direct.

## Compatibilité

| Android | API | Statut |
|---|---|---|
| 16 | 36 | Vérifié sur un appareil réel |
| 15 | 35 | Vérifié sur un appareil réel |
| 14 | 34 | Vérifié sur un appareil réel et un émulateur |
| 13 | 33 | Vérifié sur un appareil réel |
| 12 et inférieur | 31 et inférieur | Pris en charge (minSdk 26), non vérifié indépendamment |

« Vérifié » signifie que le module a été installé, mis dans le scope, et
confirmé actif (les hooks se déclenchent, sans plantage) sur cette version
d'Android pendant le développement.

## FAQ

**Est-ce que ça fait apparaître un vrai appareil comme un émulateur, ou un
émulateur comme un vrai appareil ?**
Les deux. Le masquage est basé sur l'identité, pas sur l'environnement — il
change ce que rapportent les API Java/natives, quel que soit ce qui tourne
réellement en dessous.

**Est-ce que ça contourne Play Integrity ou SafetyNet ?**
Non. L'attestation matérielle repose sur le TEE/StrongBox de l'appareil et
est hors de portée d'un hook Xposed en espace utilisateur — cela nécessite
une approche séparée et dédiée.

**Pourquoi dois-je inclure l'application dans son propre scope ?**
Sans cela, le propre processus de l'application n'est jamais accroché, donc
son écran Device Check afficherait les vraies valeurs de votre appareil au
lieu de celles du profil actif — faussant précisément la fonctionnalité
censée vérifier le masquage.

**Puis-je utiliser un profil qui ne correspond pas au matériel réel de mon
téléphone (par exemple un profil ARM sur un émulateur x86) ?**
Oui — chaque profil masque le processeur, donc Build.SUPPORTED_ABIS,
`os.arch`, et la chaîne brute du vendeur dans `/proc/cpuinfo` basculent tous
pour correspondre au profil, pas à l'hôte.

## Limites

- Tout ce qui ne passe pas par une API Java/native accrochée — sockets bruts,
  vérifications côté serveur, attestation matérielle — voit le véritable
  appareil.
- Les changements s'appliquent au prochain lancement d'une application
  protégée ; une application déjà en cours doit être redémarrée.
- Ce dépôt héberge uniquement les releases. Le code source est fermé.

## Avertissement

Ce module est destiné à la confidentialité, aux tests et à la compatibilité
avec vos propres applications. Vous êtes responsable de son usage. Ne
l'utilisez pas pour enfreindre les conditions d'une application, contourner
des services payants ou frauder qui que ce soit. Le logiciel est fourni tel
quel, sans garantie.

## Remerciements

- [libxposed](https://github.com/libxposed) pour l'API Xposed moderne et sa
  bibliothèque de service.
- [LSPosed](https://github.com/LSPosed/LSPosed) et
  [Vector](https://github.com/JingMatrix/Vector) pour les frameworks sur
  lesquels il fonctionne.

## De la part de DroidRooter

Android ID and Emulator Hider est un projet de **DroidRooter**, une petite
équipe qui construit des outils pour Android rooté.

- **Site web :** [droidrooter.com](https://droidrooter.com)
- **Telegram :** [@DroidRooter](https://t.me/DroidRooter)
- **Facebook :** [facebook.com/droidrooter](https://www.facebook.com/droidrooter)
- **DRVCAM, la caméra virtuelle de DroidRooter :**
  [droidrooter.com/drvcam](https://www.droidrooter.com/drvcam/) envoie votre
  propre vidéo ou images aux applications à la place de la caméra.
- **VirtualNet, l'usurpateur réseau par application de DroidRooter :**
  change ce que les applications savent de votre connexion Wi-Fi/mobile,
  open source.
- **Smali Patcher Reborn :** patche le `services.jar` de votre ROM
  directement sur l'appareil (Magisk/KernelSU/APatch) pour la position
  simulée et les fenêtres sécurisées, Android 10–17 — successeur de Smali
  Patcher / SmaliPatcherEx.

Si cette application vous aide, suivez DroidRooter pour en savoir plus.

## Licence

Propriétaire — tous droits réservés. Distribution binaire uniquement ; le
code source n'est pas publié.
