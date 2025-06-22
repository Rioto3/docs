# UX-AI向け：GitHub Pagesドキュメント配信ガイド

## システム概要

**目的**: シングルページMarkdownドキュメントをGitHub Pages経由で即座に一般公開  
**対象**: 突発的なチラシ・ガイド・説明書の配信  
**特徴**: ルーティング不要、完全独立なドキュメント群

## 基本構成

### リポジトリ情報
- **URL**: https://github.com/Rioto3/docs
- **配信ブランチ**: develop
- **配信URL**: `https://rioto3.github.io/docs/{ファイル名}`

### ファイル構造
```
docs/
├── README.md           # リポジトリ説明（配信対象外）
├── _config.yml         # Jekyll設定
├── sample-document.md  # サンプル
└── {新規ファイル}.md   # あなたが作成するドキュメント
```

## MCP操作手順

### 1. ドキュメント作成
```javascript
github:create_or_update_file({
  owner: "Rioto3",
  repo: "docs", 
  branch: "develop",
  path: "20250622-sample-guide.md",
  content: "# タイトル\n\n内容...",
  message: "Add new document: sample-guide"
})
```

### 2. 配信URL確認
作成後、以下URLでアクセス可能：
`https://rioto3.github.io/docs/20250622-sample-guide`

### 3. 更新・修正
同じMCP関数で`sha`パラメータ付きで更新可能

## ファイル命名規則

### 推奨パターン
- **日付付き**: `20250622-event-flyer.md`
- **機能別**: `tutorial-basics.md`
- **プロジェクト別**: `project-alpha-guide.md`

### URL変換
- `sample-guide.md` → `/sample-guide`
- `20250622-event.md` → `/20250622-event`
- ファイル拡張子は自動除去

## Markdown記法ガイド

### 基本構造
```markdown
# メインタイトル

## セクション見出し

**太字テキスト**  
*斜体テキスト*

- リストアイテム1
- リストアイテム2

[リンクテキスト](https://example.com)

---

**配信日**: 2025年6月22日  
**作成者**: UX-AI
```

### Jekyll自動処理
- フロントマター不要（自動生成）
- 相対リンク自動変換
- GitHub Pages標準テーマ適用

## 運用のベストプラクティス

### コミットメッセージ
- **新規**: `Add document: {説明}`
- **更新**: `Update document: {変更内容}`
- **削除**: `Remove document: {理由}`

### ファイル管理
- **削除**: 不要になったファイルは適宜削除
- **アーカイブ**: 古いファイルは日付で整理
- **バックアップ**: mainブランチに定期的にマージ

### 公開前チェック
- [ ] ファイル名がURLフレンドリー
- [ ] 内容に機密情報なし
- [ ] Markdown記法確認済み
- [ ] 配信URL動作確認

## トラブルシューティング

### 反映されない場合
1. developブランチに正しくpush済みか確認
2. GitHub Pages設定でdevelopブランチ指定済みか確認
3. 5-10分待ってから再アクセス

### URL形式エラー
- ファイル名に日本語・特殊文字使用不可
- 英数字・ハイフン・アンダースコアのみ

### 404エラー
- ファイル拡張子`.md`をURLに含めない
- 大文字小文字を正確に指定

## 実例

### 作成例
```javascript
github:create_or_update_file({
  owner: "Rioto3",
  repo: "docs",
  branch: "develop", 
  path: "ai-workflow-tips.md",
  content: `# AI開発ワークフロー Tips

## Claude + GitHub MCP活用法

### 基本パターン
1. アイデア整理
2. ドキュメント作成
3. 即座配信

---
**更新**: 2025年6月22日`,
  message: "Add AI workflow tips document"
})
```

### 配信URL
`https://rioto3.github.io/docs/ai-workflow-tips`

## まとめ

このシステムにより、UX-AIは思いついたタイミングで即座にドキュメントを一般公開できます。チラシ的な使い方に最適化されており、複雑なナビゲーションや管理画面は不要です。

**重要**: 必ずdevelopブランチにpushし、GitHub Pages設定が正しいことを確認してください。