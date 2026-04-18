---
icon: lucide/link
---

# llm-jp-4-8b-thinking モデル概要

**Source**: <https://huggingface.co/llm-jp/llm-jp-4-8b-thinking>

## 概要

**llm-jp-4-8b-thinking** は、国立情報学研究所（NII）の大規模言語モデル研究開発センターが開発した日本語対応LLMです。LLM-jp-4シリーズの一つで、8Bパラメータを持ち、日本語・英語の両言語に対応しています。

## アーキテクチャ仕様

| 項目 | 値 |
|------|-----|
| パラメータ数 | 8B（80億） |
| レイヤー数 | 32層 |
| 隠れ層サイズ | 4,096 |
| アテンションヘッド数 | 32 |
| コンテキスト長 | 65,536トークン |
| テンソルタイプ | BF16 |

トークナイザーは `llm-jp-tokenizer v4.0` の語彙を使用した Unigram byte-fallback モデルです。

## 訓練プロセス

### 事前訓練

- 総訓練トークン数: **11.7兆トークン**
- 事前訓練 → 中間訓練の2段階パイプライン

### ポスト訓練

- **SFT**（Supervised Fine-Tuning）による微調整
- **DPO**（Direct Preference Optimization）によるアライメント
- 強化学習（RL）は不使用

## 性能評価

LLM-as-a-Judge フレームワークによる評価結果：

| 推論レベル | MT-Bench (JA) | MT-Bench (EN) | AnswerCarefully | llm-jp-instructions |
|------------|:-------------:|:-------------:|:---------------:|:-------------------:|
| low        | 7.23          | 7.54          | 3.58            | 3.50                |
| medium     | 7.54          | 7.79          | 3.69            | 3.54                |

- **MT-Bench**: マルチターン会話タスク（日本語・英語）
- **AnswerCarefully**: 日本語安全性評価（336問）
- **llm-jp-instructions**: 人間作成の単一ターン問答（400問）

## 訓練データセット

| データセット | 用途 |
|-------------|------|
| [llm-jp-corpus-v4.1](https://gitlab.llm-jp.nii.ac.jp/datasets/llm-jp-corpus-v4.1) | 事前訓練コーパス |
| [llm-jp-corpus-midtraining-v2](https://gitlab.llm-jp.nii.ac.jp/datasets/llm-jp-corpus-midtraining-v2) | 中間訓練コーパス |
| [llm-jp-4-thinking-sft-data](https://huggingface.co/datasets/llm-jp/llm-jp-4-thinking-sft-data) | SFTデータ |
| [llm-jp-4-thinking-dpo-data](https://huggingface.co/datasets/llm-jp/llm-jp-4-thinking-dpo-data) | DPOデータ |

## 使用方法

公式クックブック [llm-jp-4-cookbook](https://github.com/llm-jp/llm-jp-4-cookbook) に実装例が掲載されています。

!!! warning "注意"
    モデル付属のトークナイザーを使用する必要があります。OpenAI Harmony ライブラリとの直接互換性はありません。

## ライセンス

**Apache License 2.0**

## リスクと制限事項

!!! note "免責事項"
    - 研究開発の初期段階のモデルであり、完全な安全性・品質保証はありません
    - 人間の意図とセキュリティを確保する調整は限定的です

## まとめ

llm-jp-4-8b-thinking は、NII が主導する日本語LLM開発の成果物です。11.7兆トークンという大規模な訓練データと SFT+DPO によるポスト訓練を組み合わせ、日英両言語で実用的な性能を実現しています。Apache 2.0 ライセンスで公開されており、研究・商用問わず利用可能です。
