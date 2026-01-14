+++
title = ""
date = 2026-01-14T00:00:00
draft = false
share = false
commentable = false
editable = false
+++

## **システム構成と通信アーキテクチャ**

<div style="text-align: center; margin: 30px 0;">
  <img src="/img/technical-work/software_system.png" alt="Software System" style="max-width: 75%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="margin-top: 10px; font-style: italic; color: #666;">図1. ソフトウェアシステム</p>
</div>

Mini-Vのシステムは、高度な情報処理とリアルタイム制御を両立させるために、以下の要素で構成されています。

*   **ハードウェア構成**:<br>メインコンピュータには「NVIDIA Jetson AGX Orin」を使用し、飛行制御コントローラー（フライトコントローラー）には「Pixhawk」を採用しています。
*   **通信ミドルウェア**:<br> ソフトウェア開発の核として「ROS 2 (Robot Operating System 2)」を採用しています。システムはモジュール設計となっており、認識・制御・通信の各サブシステムを複数のメンバーが並行して開発できる構成です。

*   **通信の自動化**:<br> ROS 2を搭載した上位コンピュータ（Jetson）と、低レイヤのマイクロコントローラー（モータードライバや緊急停止装置）間の通信ギャップを埋めるため、独自機構「ProtoLink」を開発しました。

    *   ROS 2のメッセージ定義から、Protocol Bufferメッセージを自動生成します。
    *   nanopbを利用することで、ArduinoやSTM32環境と互換性のある軽量なC構造体を生成し、手動でのプロトコル保守なしにシームレスな通信を実現しています。

<br>

## **物体認識系**

<div style="text-align: center; margin: 30px 0;">
  <img src="/img/technical-work/yolo.png" alt="Image inference with YOLO" style="max-width: 75%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="margin-top: 10px; font-style: italic; color: #666;">図2. YOLOによる画像推論</p>
</div>

環境認識には、カメラとLiDAR（Velodyne VLP16）を組み合わせたハイブリッド・センサーフュージョンを採用しています。処理のフローは以下の通りです。

1.  **視覚認識**:<br> 高速なリアルタイム処理が可能な「YOLO」を採用し、カメラ画像から物体のバウンディングボックス（境界枠）を抽出します。
2.  **点群処理**:<br> 同時に、Velodyne VLP16から得られる3D点群データを、ルールベースのアルゴリズムを用いてクラスタリング（塊ごとの分類）処理します。
3.  **センサーフュージョン**:<br> 2Dの視覚データと3Dの点群クラスタを統合することで、物体の「種別」と「3D空間上の正確な位置」を特定します。
4.  **コストマップ更新**:<br> 統合された障害物情報はPixhawkへ送信され、回避のためのローカルコストマップの更新に使用されます。

<br>

## **自己位置推定**

自己位置推定は、Pixhawkフライトコントローラー上で動作する「ArduPilot」ファームウェアが中心となって処理を行います。

<div style="text-align: center; margin: 30px 0;">
  <img src="/img/technical-work/pixhawk.png" alt="Pixhawk" style="max-width: 100%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="margin-top: 10px; font-style: italic; color: #666;">図3. Pixhawk</p>
</div>

*   **センサー構成**:<br> GNSS（衛星測位システム）とIMU（慣性計測装置）はPixhawkに統合されており、これらのデータをカルマンフィルタで処理して自己位置を推定します。

*   **ビジュアルオドメトリの統合**:<br> GNSSとIMUのデータに加え、ROS 2メインコンピュータから送信されるビジュアルオドメトリ（画像解析による移動量推定）情報を融合させることで、自己位置推定とPID制御を行っています。

<br>

## **計画システムと自律性**

<div style="text-align: center; margin: 30px 0;">
  <img src="/img/technical-work/mission_planner.png" alt="Simulation with Mission planner" style="max-width: 75%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="margin-top: 10px; font-style: italic; color: #666;">図4. Mission plannerによるシミュレーション</p>
</div>



* **視覚情報に基づく動的な経路生成**:<br>
  あらかじめ決められたルートを走るのではなく、カメラとLiDARで捉えた環境情報からリアルタイムに航路を計算します。

    *   **安全な通過ルートの特定**: 左右にある目印を検出し、その幾何学的な中間点を算出することで、安全に通過できるルートを特定します。
    *   **ウェイポイントの自動生成**: 算出した目標地点に対して相対的なウェイポイントを次々と生成し、目的地まで自律的に舵を取ります。

<br>

* **障害物の検知と回避機能**:<br>
  航行ルート上に障害物が存在する場合、ロボットはそれを即座に認識して回避行動をとります。

    *   **コストマップによる空間認識**: 認識された障害物の情報は、ロボットが持つ「ローカルコストマップ（周囲の地図）」に即座に反映されます。
    *   **周回・回避**: 障害物を検知した際は、GNSS情報と照合して位置を特定すると同時に、LiDARで距離を計測しながら安全な距離を保って回避・周回する高度な制御を行います。

<br>

* **状況判断による精密操船**:<br>
  単に移動するだけでなく、外部からの信号やドックの形状を理解し、複雑な動作を行うことが可能です。

    *   **信号解析と動作決定**: 光信号などの外部サインを画像認識で解析し、その指示（色やパターン）に基づいて、時計回りや反時計回りの旋回など、複雑な図形を描くように航行することができます。
    *   **高精度な接近制御**: 岸壁やドックへの着岸が必要な場面では、LiDARの測距データを用いて壁面との距離を数センチ単位で把握し、指定された場所へ正確にアプローチして停止します。

<br>

* **シミュレーションによる安全性検証**:<br>
  これらの複雑な自律行動は、実機を動かす前に仮想空間で徹底的に検証されます。PixhawkとDockerコンテナを活用したSITL（Software-In-The-Loop）環境により、実際の水面よりも広いフィールドでの挙動確認を経て、安全なソフトウェアのみが実機にデプロイされます。
