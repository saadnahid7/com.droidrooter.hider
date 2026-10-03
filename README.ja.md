<div align="center">

# Android ID and Emulator Hider

**端末の識別情報を偽装し、root と Xposed を隠す。検知を回避する。**

[DroidRooter](https://droidrooter.com) による Xposed/LSPosed モジュール。

[![Release](https://img.shields.io/github/v/release/saadnahid7/com.droidrooter.hider?style=for-the-badge&color=teal)](https://github.com/saadnahid7/com.droidrooter.hider/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/saadnahid7/com.droidrooter.hider/total?style=for-the-badge&color=violet)](https://github.com/saadnahid7/com.droidrooter.hider/releases)
[![Android](https://img.shields.io/badge/Android-8%20to%2016-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#互換性)
[![Xposed API](https://img.shields.io/badge/libxposed%20API-102-orange?style=for-the-badge)](https://github.com/libxposed/api)

[![DroidRooter](https://img.shields.io/badge/DroidRooter-droidrooter.com-2F6BFF?style=for-the-badge)](https://droidrooter.com)
[![Telegram](https://img.shields.io/badge/Telegram-@DroidRooter-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/DroidRooter)
[![Facebook](https://img.shields.io/badge/Facebook-DroidRooter-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://www.facebook.com/droidrooter)

**他の言語で読む:** [English](README.md) · [Español](README.es.md) · [العربية](README.ar.md) · [Deutsch](README.de.md) · [简体中文](README.zh-hans.md) · [Français](README.fr.md) · [Italiano](README.it.md)

</div>

---

## なぜ Android ID and Emulator Hider なのか

多くのアプリは、端末がエミュレーターである、root化されている、あるいは
フック系フレームワークが動いていると判断した瞬間に、動作を拒否したり、
機能をひっそり制限したりします。このモジュールは、Java層・ネイティブ層の
両方で、そうしたチェックが見る内容そのものを書き換え、アプリが手を加えて
いない市販端末と同じように動作するようにします。

- **12 種類の実在する端末プロファイル**（Pixel、Galaxy、POCO、OnePlus、
  Redmi、Nothing）から選択可能。いずれも GSMA で検証済みの IMEI 割り当てと
  実際の工場出荷時ビルドフィンガープリントに基づいており、架空の値ではあり
  ません。
- アプリごとに各保護機能を個別に ON/OFF 可能。1 画面で操作できます。
- **Device Check** を実行すれば、検査アプリが今まさにあなたの端末から読み
  取る内容を、そのままライブで確認できます。

基本のマスキング機能は常に無料です。一度の購入でカスタムプロファイル、
セーフモード、いくつかの追加識別子がアンロックされます — アプリ内の
**Unlock Pro** を参照してください。

## 対応範囲

| 保護項目 | 変更される内容 |
|---|---|
| 端末識別情報 | モデル、ブランド、メーカー、フィンガープリント、ビルドプロパティ、Android ID、シリアル番号 |
| エミュレーターの痕跡 | qemu/goldfish プロパティ、ファイル、カーネルドライバ名、`/proc/mounts` |
| プロセッサ | ABI リスト、`os.arch`、および `/proc/cpuinfo` の生のベンダー/モデル文字列（x86 ホスト） |
| グラフィック | GPU ベンダーとレンダラー文字列 |
| センサー | センサー名とベンダー |
| バッテリー | 残量、健全性、状態、容量、sysfs の値 |
| 入力デバイス | デバイス名、`/proc/bus/input/devices` |
| 電話無線 | IMEI、IMSI、SIM のキャリア/国、電話番号、ベースバンドバージョン |
| カメラ | カメラ台数と向き（前面/背面）、カメラ ID ごと |
| 位置情報 | 最後に取得した位置情報を問い合わせて何も得られないアプリへのフォールバック応答 |
| Root | `su`、Magisk、KernelSU および関連バイナリ/パス、`ro.debuggable`/`ro.secure` |
| Xposed | `/proc/self/maps`、パッケージマネージャー、logcat 内の LSPosed/Vector の痕跡 |

## 必要条件

- 現代的な **libxposed API 102** に対応した LSPosed 互換フレームワークを
  導入した root化端末。例: [LSPosed](https://github.com/LSPosed/LSPosed) や
  [Vector](https://github.com/JingMatrix/Vector)。
- Android 8.0 以降。

> [!IMPORTANT]
> このモジュールは現代的な libxposed API 上に構築されています。従来の
> Xposed や EdXposed はサポートされていません。

## インストール

1. 最新の APK を [Releases](../../releases/latest) からダウンロードして
   インストールします。
2. Xposed マネージャーを開き、**Android ID and Emulator Hider** を有効化
   してスコープに追加します — 自分自身の Device Check 画面を保護するため
   にも**自分自身をスコープに含める必要があります**。保護したい他のアプリ
   も同様に追加してください。
3. スコープに追加した各アプリを強制終了してから再度開いてください。

## 使い方

1. アプリを開きます。フレームワークがプロセスへのフックに成功すると、
   上部のステータスカードに **Protected** と表示されます。
2. 端末プロファイルを選択します — Pixel 8、Galaxy S24、POCO X3 Pro ほか
   9 種類。
3. **Protection** で各保護機能を個別に ON/OFF します。
4. **Device Check** をタップすると、検査アプリが読み取るであろう内容 —
   ビルドプロパティ、フィンガープリント、CPU、センサー、バッテリー — を、
   現在有効なプロファイルと比較しながらライブで確認できます。

## 互換性

| Android | API | 状態 |
|---|---|---|
| 16 | 36 | 実機で検証済み |
| 15 | 35 | 実機で検証済み |
| 14 | 34 | 実機・エミュレーター双方で検証済み |
| 13 | 33 | 実機で検証済み |
| 12 以下 | 31 以下 | サポート対象（minSdk 26）、個別の検証は未実施 |

「検証済み」とは、開発中にそのバージョンの Android でモジュールをインス
トールし、スコープに追加し、動作していること（フックが発動し、クラッシュ
しないこと）を確認したことを意味します。

## FAQ

**実機をエミュレーターに見せかけることも、エミュレーターを実機に見せかける
こともできますか？**
どちらも可能です。マスキングは環境ではなく識別情報に基づいているため、実際
に何が裏で動いているかに関係なく、Java/ネイティブ API が報告する内容を
変更します。

**Play Integrity や SafetyNet を回避できますか？**
いいえ。ハードウェアアテステーションは端末の TEE/StrongBox に支えられて
おり、ユーザー空間の Xposed フックでは手が届きません。これには全く別の
専用のアプローチが必要です。

**なぜアプリ自身をスコープに含める必要があるのですか？**
含めないと、アプリ自身のプロセスが一切フックされないため、Device Check
画面には有効なプロファイルの値ではなく端末の実際の値が表示されてしまい
ます — マスキングを検証するための唯一の機能自体が、誤った結果を示して
しまうということです。

**実機のハードウェアと一致しないプロファイル（例: x86 エミュレーター上で
ARM プロファイル）を使用できますか？**
はい。すべてのプロファイルはプロセッサもマスキングするため、
Build.SUPPORTED_ABIS、`os.arch`、`/proc/cpuinfo` の生のベンダー文字列は
すべてホストではなくプロファイル側に切り替わります。

## 制限事項

- フックされた Java/ネイティブ API を経由しないもの — 生のソケット通信、
  サーバー側のチェック、ハードウェアアテステーション — は実際の端末が見
  えます。
- 変更は保護対象アプリの次回起動時に反映されます。既に起動中のアプリは
  再起動が必要です。
- このリポジトリはリリースのみを公開しています。ソースコードは非公開です。

## 免責事項

このモジュールはプライバシー保護、テスト、そして自分自身が開発したアプリ
との互換性確保を目的としています。使用方法についてはご自身の責任で判断
してください。アプリの利用規約違反、有料サービスの不正回避、他者への詐欺
目的での使用はしないでください。本ソフトウェアは現状のまま提供され、いか
なる保証もありません。

## 謝辞

- 現代的な Xposed API とサービスライブラリを提供する
  [libxposed](https://github.com/libxposed)。
- 本モジュールが動作する基盤である
  [LSPosed](https://github.com/LSPosed/LSPosed) と
  [Vector](https://github.com/JingMatrix/Vector)。

## DroidRooter について

Android ID and Emulator Hider は、root化 Android 向けのツールを開発する
小さなチーム **DroidRooter** のプロジェクトです。

- **ウェブサイト:** [droidrooter.com](https://droidrooter.com)
- **Telegram:** [@DroidRooter](https://t.me/DroidRooter)
- **Facebook:** [facebook.com/droidrooter](https://www.facebook.com/droidrooter)
- **DRVCAM（DroidRooter の仮想カメラ）:**
  [droidrooter.com/drvcam](https://www.droidrooter.com/drvcam/) は、カメラ
  映像の代わりに自分の動画や画像をアプリに送り込みます。
- **VirtualNet（DroidRooter のアプリ別ネットワーク偽装ツール）:**
  アプリに伝わる Wi-Fi/モバイル通信の情報を変更します。オープンソース。
- **Smali Patcher Reborn:** ROM の `services.jar` を端末上で直接パッチし
  （Magisk/KernelSU/APatch）、モック位置情報とセキュアウィンドウに対応。
  Android 10〜17 対応、Smali Patcher / SmaliPatcherEx の後継。

このアプリが役に立ったら、ぜひ DroidRooter をフォローしてください。

## ライセンス

独占的所有権 — 全ての権利を留保します。バイナリ配布のみ。ソースコードは
公開されていません。
