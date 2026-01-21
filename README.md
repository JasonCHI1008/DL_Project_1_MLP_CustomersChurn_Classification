# Customer Churn Prediction using MLP (Deep Learning)

## 📌 プロジェクト概要 (Project Overview)

このプロジェクトの目的は、深層学習モデル（MLP）を使って、お客さんが解約するかどうか（チャーン）を予測することと、その解約に一番大きく影響している要因を分析することです。

顧客データを詳しく分析してモデルを作ることで、精度の高い予測モデルができました。それだけでなく、『特徴量重要度（Feature Importance）』の分析を行って、お客さんが離れてしまう根本的な原因を明らかにしました。。

## 🛠️ 方法論とワークフロー (Methodology)

本プロジェクトは、主に以下の 3 つのフェーズで進行しました。

### 1. 探索的データ分析 (EDA) と前処理 (Preprocessing)

モデル構築の前に、データの包括的な分析とクリーニングを行いました。

- **単変量分析 (Univariate Analysis):** 各特徴量とターゲット変数の分布をプロットし、クラスの不均衡（Class Imbalance）やデータの基本特性を確認しました。
- **多変量分析 (Multivariate Analysis):** 解約ラベルと各特徴量の関係を調査し、ヒートマップを用いて特徴量間の相関関係を可視化しました。
- **特徴量エンジニアリング:**
  - **ワンホットエンコーディング (One-Hot Encoding):** カテゴリカル変数を数値特徴量に変換しました。
  - **標準化 (Standardization):** 学習効率の向上とスケールの違いによる影響を防ぐため、訓練データの特徴量を標準化しました。

### 2. モデル構築 (Model Construction)

MLP（多層パーセプトロン）ニューラルネットワークを構築しました。

- **アーキテクチャ設計:** 層が進むにつれてノード数が減少するファネル型構造（例：`128 -> 64 -> 32 -> 16`）を採用し、各層に ReLU 活性化関数、出力層に Sigmoid 関数（二値分類用）を使用しました。
- **ハイパーパラメータ調整:**
  - 検証データセット（Validation Set）を用いてパラメータチューニングを実施しました。
  - **ベスト構成:** Optimizer: Adam, Learning Rate: 0.001, Dropout: 0.2, Batch Norm: False.
  - 過学習（Overfitting）を防ぐため、Early Stopping と Dropout を適用しました。

### 3. モデル評価 (Model Evaluation)

最終的なモデルをテストデータセット（Test Set）で厳密に評価しました。

- **過学習の確認:** 学習曲線（Training/Validation/Test の Loss と Accuracy）を比較し、モデルの汎化性能を確認しました。
- **評価指標:** Accuracy, Precision, Recall, F1-score, ROC-AUC などの主要な分類指標を使用しました。
- **要因分析:** モデルの予測根拠を理解するため、テストセットに対して **Permutation Feature Importance** を適用しました。

## 📊 結果と成果 (Results)

モデルはテストセットにおいて優れた性能を示しました。

| Metric       | Score                                      |
| :----------- | :----------------------------------------- |
| **Accuracy** | **93.6%**                                  |
| **ROC-AUC**  | **0.952**                                  |
| **Recall**   | **99.8%** (解約者の検出漏れが極めて少ない) |

_(ここに ROC 曲線 や 混同行列 の画像を挿入してください)_
`![ROC Curve](./path/to/your/roc_curve.png)`

### 重要な発見 (Key Insights)

**Permutation Feature Importance** 分析の結果、顧客解約に影響を与える 3 大要因が特定されました。

1.  **Payment Delay (支払遅延):** 解約の最も強力なシグナルです。
2.  **Age (年齢):** 顧客の年齢層が解約率に大きく影響しています。
3.  **Support Calls (サポートへの問い合わせ):** 頻繁な問い合わせは、解約の前兆である傾向が高いです。

対照的に、`Tenure`（契約期間）や `Subscription Type`（サブスクリプションの種類）の影響度は比較的低いことが分かりました。

## 🚀 結論 (Conclusion)

本プロジェクトでは、堅牢な MLP モデルの学習に成功しました。このモデルは、解約しそうな顧客を極めて高い確率で特定できる（High Recall）だけでなく、ビジネスアクションに繋がる洞察も提供します。「支払遅延」や「頻繁なサポート利用」が見られる顧客層に対して、優先的にリテンション施策（引き留め策）を実施することを推奨します。

---

## 💻 使用技術 (Tech Stack)

- **Language:** Python
- **Deep Learning:** PyTorch
- **Data Processing:** Pandas, NumPy, Scikit-learn
- **Visualization:** Matplotlib, Seaborn
