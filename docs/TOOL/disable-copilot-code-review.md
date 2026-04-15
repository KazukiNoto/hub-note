---
icon: lucide/shield-off
---

# GitHub Copilot 自動コードレビューの停止方法

## 概要

GitHub Copilot には、プルリクエストを自動的にレビューする **Copilot code review** 機能があります。
この機能を無効化したい場合は、リポジトリまたは Organization の設定から停止できます。

## 停止手順

1. GitHub リポジトリ（または Organization）の **Settings** を開く
2. 左サイドバーから **Copilot** を選択
3. **Cloud agent Validation tools** セクションを探す
4. **Copilot code review** のトグルを **OFF** にする

```
Settings
  └─ Copilot
       └─ Cloud agent Validation tools
            └─ Copilot code review → OFF
```

!!! warning "注意"
    設定変更はリポジトリ管理者権限が必要です。Organization レベルで設定している場合は Organization の Settings から変更してください。

## 確認ポイント

- OFF にすると、新しいプルリクエストに対して Copilot が自動でレビューコメントを投稿しなくなります
- 既存のレビューコメントは削除されません
- 再度 ON にすればいつでも有効化できます
