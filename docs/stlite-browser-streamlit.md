---
icon: lucide/link
---

# Stliteでブラウザ上でStreamlitを動かす楽しさ

**Source**: <https://zenn.dev/zreactor/articles/abfc83c78deea3>

## 概要

Yu Tachibanaさんによる、サーバーなしでStreamlitアプリをブラウザ上で動かせるライブラリ **Stlite** の使用体験レポート。コスト削減とセキュリティを重視したWebアプリ開発に活用した事例を紹介している。

## Streamlitとは

PythonだけでインタラクティブなWebアプリを作れるフレームワーク。FlaskやHTML/JavaScriptの知識なしに、シンプルなコードでUIを構築できる。

## 作ったもの

医療レポートデータをアップロードし、AIが健康指標を解釈するWebアプリ。設計方針として **サーバーインフラを持たない** ことを優先した。

## Stliteの主なメリット

- **Stlite Sharing** ツールを使えば、PythonコードからHTMLファイルを自動生成
- 生成した単一のHTMLファイルを静的ホスティングサービスにデプロイするだけ
- すべての計算がクライアントサイドで完結するため、**ホスティングコストがゼロ**
- URLを共有するだけで簡単に配布できる

## 遭遇した課題

!!! warning "Pyodideの制限"
    HTTPXに依存するライブラリがPyodideの制約で動作しないことがある。OpenAIの公式SDKも内部でHTTPXを使用しているため、代わりに`requests`ライブラリを使ったコードに書き直す必要があった。

## まとめ

Stliteは以下のようなケースで特に有用：

- サーバーレスでアプリを公開したい
- 静的ホスティング（GitHub Pagesなど）を使いたい
- コストやセキュリティを重視したい

ライブラリの制限に注意しつつも、手軽にPythonアプリをWebで公開できる強力な選択肢。
