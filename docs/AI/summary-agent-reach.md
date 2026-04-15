---
icon: lucide/link
---

# Agent Reach - AI エージェント向けインターネットアクセスプラットフォーム

**Source**: <https://github.com/Panniantong/Agent-Reach/blob/main/docs/README_ja.md>

## 概要

Agent Reach は、AI エージェント（Claude Code、Cursor など）に対して、複数のプラットフォームへのワンクリックインターネットアクセスを提供するツールです。Twitter、Reddit、YouTube、Bilibili、GitHub など、多数のプラットフォームの面倒な初期設定を排除し、単一のインストール手順で統合的にアクセスできるようにしています。

## 主な解決課題

従来、AI エージェントを多様なプラットフォームに接続するには以下のステップが必要でした：

- 各プラットフォーム用のツールを個別に探す
- 依存関係をインストール
- 設定を個別にデバッグ

Agent Reach はこれをすべて一つのインストールに統合しています。

## インストール方法

AI エージェント内に以下のコマンドをペーストするだけです：

```
Install Agent Reach: https://raw.githubusercontent.com/Panniantong/agent-reach/main/docs/install.md
```

## 対応プラットフォーム

- **Web ブラウジング** - Jina Reader 経由
- **Twitter/X** - ビュー、検索（クッキー対応）
- **YouTube/Bilibili** - 字幕、1800+ のビデオサイト対応
- **GitHub** - パブリックリポジトリの即座アクセス
- **Reddit、小红书（Xiaohongshu）、WeChat、Weibo、RSS、LinkedIn**
- **Douyin** - ウォーターマークなしのビデオ分析

## 設計思想

Agent Reach は「フレームワークではなくスカフォルディング」として機能します。

- ツール選択と設定の判断を処理
- 上流のツール（twitter-cli、yt-dlp、rdt-cli など）に直接委譲
- ラッパーレイヤーなし
- すべてのチャネルが置き換え可能な設計

## 主な利点

- **完全無料** - オプションの $1/月のプロキシでサーバーアクセス可能
- **プライバシー保護** - クッキーはローカルに保存
- **プラグイン可能なアーキテクチャ** - 基盤となるツールを必要に応じて交換可能
- **ビルトイン診断** - `agent-reach doctor` コマンドで診断可能

## ライセンス

MIT License
