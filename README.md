# Dynamic Adaptive Pruning with Terminal Attractor for LLMs
（※日本語のタイトルを入れる場合：大規模言語モデルにおけるターミナルアトラクタを用いた動的適応型プルーニング）

## 概要 (Overview)
本リポジトリは、大規模言語モデル（LLM）の効率化を目的とした新しいモデル圧縮手法の実験コードを公開しています。
パラメータの削除によって生じるネットワークの構造破壊に対し、「適応型プルーニング（AGIP）」による安全な削減と、「ターミナルアトラクタ（TA）項」を用いた再学習アルゴリズムを組み合わせることで、勾配消失を防ぎつつ有限時間での高精度なリカバリー（Perplexityの回復）を実現する手法を提案・検証しています。

本実験では、GPT-2モデルとWikiText-2データセットを用いて、提案手法の有効性をベースラインと比較しています。

## リポジトリの構成 (File Structure)
実験の段階に合わせて、以下の3つのJupyter Notebook (`.ipynb`) が含まれています。

1. **`ベースライン_maxgrad4.0.ipynb` (Baseline)**
   * 比較の基準となる標準的なファインチューニングおよびプルーニングを実行します。特殊な更新式や動的制御は含みません。
2. **`AGIP30％_maxgrad4.0.ipynb` (AGIP Only)**
   * 学習の進行（Lossの大きさ）に応じて、プルーニングの削除率を動的に調整する「適応型プルーニング（AGIP）」のみを適用したモデルです。目標スパース率を30%に設定しています。
3. **`TA+AGIP30__maxgrad4.0.ipynb` (Proposed Method: TA + AGIP)**
   * 本研究の提案手法です。AGIPによる動的プルーニングに加え、重みの更新式にターミナルアトラクタ（TA）項を導入しています。Lossのβ乗を分子、勾配ノルムを分母に配置することで、平坦な地形でも誤差を駆動源として強制的に収束へ向かわせます。

## 環境構築 (Prerequisites)
実行には Python 3.10 以上および、CUDA対応のGPU（推奨: NVIDIA T4 / RTX 4080 など）が必要です。

必要なライブラリは以下の通りです。
```bash
pip install torch torchvision torchaudio
pip install transformers datasets accelerate scikit-learn matplotlib
```
著者
さとちから０９２０/佐藤　力

富山県立大学　レネ研究室
