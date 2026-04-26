---
icon: lucide/glasses
---

# Even G2 スマートグラス & Even Hub 開発ガイド

**Source**: <https://hub.evenrealities.com/>

## 概要

**Even G2** は、Even Realities社が開発したAI搭載スマートグラス。見た目は普通のメガネに近く、日常使いを重視した設計が特徴。**Even Hub** はG2向けのオープンな開発者エコシステム＆アプリストアで、Web技術でアプリを開発できる。

---

## Even G2 ハードウェア仕様

| 項目 | 内容 |
|---|---|
| **ディスプレイ** | デュアルmicro-LED、グリーン単色、4bitグレースケール（16階調） |
| **解像度** | 640×350ピクセル（G1の640×200から向上） |
| **表示量** | 日本語約10行、最大2,000文字表示可能 |
| **重量** | 約37.7g |
| **バッテリー** | 通常使用で最大2日間、充電ケースで7回フル充電可能 |
| **カメラ** | 非搭載（プライバシー配慮） |
| **スピーカー** | 非搭載 |
| **入力方法** | テンプルタップ / R1リングクリック |
| **翻訳対応** | 35言語のリアルタイム翻訳 |

## AI機能

- ユーザーの会話やメモから学習し、文脈に応じたサポートを提供
- 前回の会議内容の要約や買い物リストのリマインドなど
- リアルタイム字幕・翻訳表示

## 専用コントロールリング「Even R1」

- G2と一緒に発売されたスマートリング
- 指の微妙な動きでページスクロールや通知確認が可能
- 目立たず操作できるのが利点

## G1との主な違い

- ディスプレイ解像度が向上（200px → 350px）
- AI機能が強化
- R1リングとの連携が追加
- バッテリー持続時間の改善

---

## Even Hub 開発ガイド

### 開発の仕組み

G2アプリは **通常のWebアプリ** で、特別なフレームワークは不要。以下の流れで動作する：

1. PC上でVite開発サーバーを起動
2. スマートフォンのEven Hubアプリがそのサーバーにアクセス
3. WebView内でアプリが動作し、SDKを通じてグラスに描画コマンドを送信

### 環境構築（3ステップ）

**必要なもの：** Node.js v18+ / npm / Git / Bash

```bash
# ① リポジトリのクローン
git clone https://github.com/BxNxM/even-dev.git

# ② 依存パッケージのインストール
npm install

# ③ 開発サーバーの起動
./start-even.sh
```

### 主なSDKパッケージ

| パッケージ | 説明 |
|---|---|
| `even_hub_sdk` | 公式SDK |
| `even-better-sdk` | 推奨ラッパー（使いやすい） |
| `evenhub-simulator` | ローカルシミュレーター |

### 対応機能

- テキスト表示・リスト表示
- 画像表示
- マイク入力（音声認識）
- REST API / WebSocket通信
- インタラクション制御（タップ、リング操作）

### スターターテンプレート

Even Realitiesが4種類のテンプレートを提供：

| テンプレート | 用途 |
|---|---|
| **minimal** | 最小構成 |
| **asr** | 音声認識 |
| **image** | 画像表示 |
| **text-heavy** | テキスト多め |

### 開発コミュニティ

- **Discord** でパイロット開発者同士がフィードバック・デモ・実践的なTipsを共有
- 2,000人以上の開発者が参加
- 日本語の開発入門記事も複数公開されている

---

## 参考資料

- [Even Hub 公式サイト](https://hub.evenrealities.com/)
- [Even G2 公式サイト](https://www.evenrealities.com/smart-glasses)
- [Even G2 スマートグラス開発入門（1）— 環境構築からHello Worldまで](https://zenn.dev/miyaura/articles/eveng2-part1-getstarted-0ed90d3aa144e8)
- [Even G2 スマートグラス開発入門（2）— インタラクション制御とUI構築](https://zenn.dev/miyaura/articles/eveng2-part2-intructions-44c14f04b8fa08)
- [Even G2開発: SDK機能の動作確認メモ](https://zenn.dev/bigdra/articles/eveng2-sdk-features)
- [Even Realities G2アプリのシンプルな開発方法まとめ](https://www.crossroad-tech.com/entry/even-realities-G2-hello-world)
- [Even Hub Simulator - GitHub](https://github.com/BxNxM/even-dev)
- [Even Realities GitHub](https://github.com/even-realities)
