---
icon: lucide/link
---

# StliteでのStreamlit静的開発環境を普通のPython開発に近づける

**Source**: <https://qiita.com/suzuki_sh/items/9d6f77c6975c69485e08>

## 概要

[Pyodide](https://pyodide.org/) を活用してブラウザ上で動作するStreamlit実装である **Stlite** の開発環境を、通常のPython開発と同様の体験に近づける方法を紹介した記事。サーバーレスで静的サイトホスティングにデプロイ可能な構成を目指している。

## 主なポイント

### 1. 開発環境の構築

- **Dev Container** を活用し、Node.jsベースのコンテナに `uv` パッケージマネージャーを追加して環境を統一化
- 通常のPython開発と同じツールチェーンを維持しつつ、Stlite特有の制約に対応

### 2. Stliteアプリの立ち上げ

- **Rspack** を使用してWebアプリをバンドル
- `index.html` テンプレートに特別なCSSリンクを含める方式でセットアップ

### 3. Python開発体験の向上

- `uv` でPythonファイルを分離管理
- VS CodeのPython拡張機能で静的解析（型チェック・補完）を実現
- ローカルでの開発フローをブラウザ向けビルドから分離

### 4. 依存関係の管理

- `pyproject.toml` の依存関係を `requirements.txt` に変換
- Pyodide環境に必要なパッケージを自動インストール

## まとめ

Dev Container・uv・Streamlitの組み合わせにより、Stliteの「サーバーレス・静的デプロイ」という利点を活かしながら、通常のPython開発体験に近い環境を実現できる。フロントエンドのビルドツール（Rspack）を介することで、ブラウザ動作とローカル開発の両立が可能になっている。
