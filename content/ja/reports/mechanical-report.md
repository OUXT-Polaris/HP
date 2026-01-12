+++
title = ""
date = 2026-01-12T00:00:00
draft = false
share = false
commentable = false
editable = false
+++

## 船体（ハル）の設計改良

### 課題と反省 (RoboBoat 2025)
RoboBoat 2025において、私たちは自律航行中の転覆によりタスクを完了できないという悔しい結果を経験しました。
その構造的な原因は、主に以下の2点にありました。

*   **重心の高さ**: 機体全体の重心位置が高すぎたこと。
*   **船体形状の不安定さ**: 以前採用していた「湾曲したハイロッカー型（バナナ型）」のポンツーンは、水面での安定性に欠けていました。

### 2026年に向けた構造の抜本的改良
転覆を防ぎ、ミッションを確実に成功させるため、以下の構造変更を行いました。

*   **船体形状の変更（フラットボトム化）**  
    不安定だったバナナ型をやめ、底面が平らな「フラットボトム型」のポンツーンを新たに設計・採用しました。
*   **低重心化（Low Center of Gravity）**  
    電子機器を収めるエンクロージャー（防水ケース）の取り付け位置を物理的に下げ、重心を低く設定し直しました。また、ハル内部にバッテリーとモータドライバを収納できる設計にすることで、さらなる低重心化を実現しました。

<div style="text-align: center; margin: 30px 0;">
  <img src="/img/technical-work/placeholder1.jpg" alt="Hull comparison" style="max-width: 100%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="margin-top: 10px; font-style: italic; color: #666;">Fig 1. The top hull is our new one, and the bottom is the old design. The arrow indicates the cavity that holds the battery box.</p>
</div>



## その他の詳細設計と実装

### 気密性と配線の確保
ハル内部のバッテリーやモータードライバを、外部の電装ボックスと接続するための配線経路を再設計しました。
コネクタを通し、かつ気密性を保つために、以下の手法を採用しています。

1.  ハルに配線用の穴を開ける。
2.  タッパー（密閉容器）を用いて穴を塞ぎ、気密区画を作成。
3.  接着にはエポキシ樹脂を使用し、完全な防水・気密を実現（Fig 4参照）。

### フレームとの接続強度の確保
ハルとフレームの接続には、各ハルの中央1箇所に専用の治具を作成して固定する方法をとっています。
しかし、1点固定ではモーメント荷重（ねじれや曲げの力）によって治具が破壊されるリスクがありました。
そこで、フレームから伸びる支持パーツを追加作成し、ハルの両端を支える構造にしました（Fig 5参照）。これにより負荷を分散させ、安定した接続を実現しています。
完成した機体は、縦横ともに1m未満のコンパクトなサイズに収まりました。
2人で簡単に持ち運ぶことができ、運搬やセットアップの負担を大幅に軽減しています。

<div style="display: flex; flex-wrap: wrap; justify-content: center; gap: 20px; margin-top: 30px;">
  <div style="flex: 1; min-width: 300px; text-align: center;">
    <img src="/img/technical-work/placeholder4.jpg" alt="Wiring and sealing detail" style="max-width: 100%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
    <p style="margin-top: 10px; font-style: italic; color: #666;">Fig 4. Detail of the wiring and sealing using epoxy and tupperware.</p>
  </div>
  <div style="flex: 1; min-width: 300px; text-align: center;">
    <img src="/img/technical-work/placeholder5.jpg" alt="Frame connection support" style="max-width: 100%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
    <p style="margin-top: 10px; font-style: italic; color: #666;">Fig 5. Additional support structure.</p>
  </div>
</div>
