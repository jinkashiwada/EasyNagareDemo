# 2D Fluid Demo / 2次元流体デモ

## 日本語

### 概要

このリポジトリは，オープンキャンパスや研究室紹介で使用するための，ブラウザ上で動作する2次元流体デモです。高校生や保護者がiPadやPCで直接操作しながら，流れ，速度場，渦度，障害物後流，数値シミュレーションの雰囲気を直感的に体験できることを目的としています。

公開対象は，連続式を近似的に考慮した `index.html` です。英語版は `index_en.html` です。

### ファイル

- `index.html`: 日本語版。連続式を近似的に考慮した展示用デモ。
- `index_en.html`: 英語版。同じ計算モデルの英語UI。

### 操作方法

- 画面を指またはマウスでなぞると，その方向へ外力を加えます。
- `一様流 ON/OFF`: 左から右へ流れる基本流を切り替えます。
- `障害物を描く`: 指またはマウスで障害物セルを追加します。
- `コンター`: 流速または渦度の表示を切り替えます。
- `ベクトル`: 速度ベクトルの表示/非表示を切り替えます。
- `流入流速`: 左端から入る一様流の強さを調整します。
- `粒子軌跡`: `なし`，点粒子，または長い軌跡を切り替えます。
- `低解像度`: iPadなどで重い場合に計算格子を粗くします。
- `リセット`: 速度場，障害物，粒子を初期化します。

### 計算モデル

このデモは厳密なCFDソルバーではありません。展示用に軽量化した平面2次元の速度場モデルです。

主な変数は以下です。

- `u`: X方向速度
- `v`: Y方向速度
- `solid`: 障害物マスク
- `pressure`: 圧力投影用の擬似圧力
- `divergence`: 速度場の発散

毎フレームで以下の処理を行います。

1. 境界条件の適用
2. 指やマウス操作による外力の付加
3. 速度場の移流
4. 簡易的な拡散・平滑化
5. 速度場の減衰
6. 発散の計算
7. Jacobi反復による圧力ポアソン方程式の近似解
8. 圧力勾配による速度補正
9. 描画

連続式については，非圧縮条件

```text
∂u/∂x + ∂v/∂y = 0
```

を厳密に満たすのではなく，少数回の圧力投影によって近似的に満たす構成です。iPadでのリアルタイム応答性を重視しているため，完全収束は行っていません。

### 注意

このデモは研究用の解析結果を得るためのものではありません。水理学，流体力学，数値シミュレーションの導入展示として，流れ場や渦度場を視覚的に理解するための教材です。

計算はWebサーバーではなく，アクセスした端末のブラウザ上で実行されます。

---

## English

### Overview

This repository contains an interactive two-dimensional fluid demo that runs entirely in a web browser. It is intended for open-campus events and laboratory outreach. Visitors can use an iPad or PC to interact with the flow and visually explore velocity fields, vorticity, wakes behind obstacles, and the idea of numerical simulation.

The primary public page is `index.html`, which provides the Japanese version with an approximate incompressibility projection. The English version is `index_en.html`.

### Files

- `index.html`: Japanese version. Main public demo with approximate incompressibility.
- `index_en.html`: English version using the same numerical model.

### Controls

- Drag with a finger or mouse to add force to the flow.
- `Uniform Flow ON/OFF`: Toggle the left-to-right background flow.
- `Draw Obstacles`: Draw solid obstacle cells with a finger or mouse.
- `Contour`: Switch between speed and vorticity contours.
- `Vectors`: Show or hide velocity vectors.
- `Inflow`: Adjust the inflow velocity at the left boundary.
- `Particles`: Disable particles, show points, or extend particle trails.
- `Low Resolution`: Use a coarser grid when performance is limited.
- `Reset`: Reset the velocity field, obstacles, and particles.

### Numerical Model

This is not a rigorous CFD solver. It is a lightweight browser-based planar 2D velocity-field model designed for educational visualization.

The main variables are:

- `u`: velocity in the X direction
- `v`: velocity in the Y direction
- `solid`: obstacle mask
- `pressure`: pseudo-pressure used for projection
- `divergence`: divergence of the velocity field

Each animation frame performs:

1. Boundary-condition update
2. User-applied forcing
3. Velocity advection
4. Simplified diffusion/smoothing
5. Velocity damping
6. Divergence calculation
7. Approximate pressure Poisson solve using Jacobi iterations
8. Velocity correction by the pressure gradient
9. Rendering

The incompressibility condition

```text
∂u/∂x + ∂v/∂y = 0
```

is not solved to full convergence. Instead, a small fixed number of pressure-projection iterations is used to reduce divergence while keeping the demo responsive on iPad-class devices.

### Scope

This demo is not intended to produce research-grade simulation results. It is an outreach and teaching tool for introducing hydraulics, fluid mechanics, velocity fields, vorticity, wakes, and real-time numerical visualization.

All computation runs in the visitor's browser. The web server only serves static files.
