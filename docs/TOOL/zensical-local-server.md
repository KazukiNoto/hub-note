---
icon: lucide/server
---

# Zensical ローカルサーバーの起動

Zensical の開発サーバーを起動して、変更内容をリアルタイムで確認することができます。

## ローカルサーバーの起動コマンド

```bash
zensical serve
```

このコマンドで Zensical の開発サーバーが起動します。

## デフォルト設定

- **アクセスURL**: `http://localhost:8000`
- **自動リロード**: ファイルの変更を検知して自動的にリロードされます
- **対象ファイル**: `docs/` 配下のMarkdownファイルと `zensical.toml` の変更を監視

## 使用方法

1. リポジトリのルートディレクトリで以下を実行：

```bash
zensical serve
```

2. ブラウザで `http://localhost:8000` にアクセス

3. `docs/` 配下のMarkdownファイルを編集すると、ブラウザが自動的にリロードされます

4. サーバーを停止するには `Ctrl+C` を押します

## その他の便利なコマンド

- **本番ビルド（検証用）**:
```bash
zensical build --clean
```

- **ビルド結果の確認**: `site/` ディレクトリに生成されたHTMLを確認できます

## 注意事項

- ローカルサーバーは開発用です。本番環境への公開はGitHub Actionsで自動デプロイされます
- `site/` ディレクトリはGitの対象外（`.gitignore`で除外）です
