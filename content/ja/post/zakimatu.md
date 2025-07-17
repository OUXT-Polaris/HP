---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "nebulaで絶え間のない点群を感じよう"
subtitle: ""
summary: ""
authors: [ざきまつ]
tags: [OUXT勉強会]
categories: [OUXT勉強会]
date: 2025-01-29T23:36:59+09:00
lastmod: 2025-01-29T23:36:59+09:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

## はじめに
OUXT Polaris学生メンバー、ソフトウェア担当の松崎です。
専門は制御理論ですが、OUXTでは認識系統を担当しています。

今回は、Volodyne VLP-16をROS 2で使用する際に "ros-drivers" ではなく、サードパーティ製のドライバパッケージである "nebula" を使ってみたので、導入方法の紹介と使用感・Rviz2でのデータ比較を行います。

つづきは、こちらのリンクから！⇩

https://note.com/santana3/n/nd3f68c2f4de5