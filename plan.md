# tldv Raycast Extension - 実装計画書

## 📋 プロジェクト概要

tldvのRaycast拡張機能を開発し、録画済みミーティングへの素早いアクセスと管理を実現します。

### 目的
- tldvの録画コンテンツへの迅速なアクセス
- Raycastから直接録画の検索・閲覧
- トランスクリプトの検索とコピー
- 録画リンクの共有機能

## 🎯 主要機能

### 1. コアコマンド

#### 1.1 録画一覧 (List Recordings)
- 最近の録画をリスト表示
- サムネイル、タイトル、日時、参加者を表示
- ページネーション対応

#### 1.2 録画検索 (Search Recordings)
- キーワードによる録画検索
- トランスクリプト内検索
- 話者別フィルタリング

#### 1.3 録画詳細表示 (View Recording)
- 録画の詳細情報
- トランスクリプト全文表示
- タイムスタンプ付きセグメント表示
- キーモーメント/ハイライト表示

#### 1.4 クイックアクション
- 録画リンクをコピー
- ブラウザで開く
- 特定タイムスタンプへのリンク生成
- Slack/メールで共有

### 2. 追加機能

#### 2.1 お気に入り管理
- 重要な録画をお気に入り登録
- お気に入りリストへのクイックアクセス

#### 2.2 ノート機能
- 録画へのメモ追加
- タイムスタンプ付きコメント

#### 2.3 統計ダッシュボード
- 録画数の統計
- 視聴時間の集計
- 最もアクティブな参加者

## 🛠 技術仕様

### API統合

#### 認証
- APIキーベース認証
- OAuth 2.0 (利用可能な場合)
- トークンの安全な保存

#### エンドポイント (予定)
```
GET /api/v1/recordings        # 録画一覧取得
GET /api/v1/recordings/{id}   # 録画詳細取得
GET /api/v1/recordings/search # 録画検索
GET /api/v1/transcripts/{id}  # トランスクリプト取得
POST /api/v1/share            # 共有リンク生成
```

### プロジェクト構造

```
tldv-extension/
├── src/
│   ├── api/
│   │   ├── client.ts         # APIクライアント
│   │   ├── auth.ts           # 認証処理
│   │   └── types.ts          # API型定義
│   │
│   ├── commands/
│   │   ├── listRecordings.tsx    # 録画一覧コマンド
│   │   ├── searchRecordings.tsx  # 検索コマンド
│   │   ├── viewRecording.tsx     # 詳細表示コマンド
│   │   └── quickActions.tsx      # クイックアクション
│   │
│   ├── components/
│   │   ├── RecordingItem.tsx     # 録画アイテムコンポーネント
│   │   ├── TranscriptView.tsx    # トランスクリプト表示
│   │   ├── RecordingDetail.tsx   # 録画詳細
│   │   └── SearchBar.tsx         # 検索バー
│   │
│   ├── hooks/
│   │   ├── useRecordings.ts      # 録画データフック
│   │   ├── useSearch.ts          # 検索フック
│   │   └── useAuth.ts            # 認証フック
│   │
│   ├── utils/
│   │   ├── date.ts               # 日付ユーティリティ
│   │   ├── format.ts             # フォーマット関数
│   │   └── cache.ts              # キャッシュ管理
│   │
│   └── types/
│       ├── recording.ts          # 録画型定義
│       ├── transcript.ts         # トランスクリプト型
│       └── user.ts               # ユーザー型
│
├── assets/
│   ├── icon.png                  # 拡張機能アイコン
│   ├── tldv-logo.png            # tldvロゴ
│   └── icons/                   # 各種アイコン
│
├── package.json
├── tsconfig.json
├── README.md
└── CHANGELOG.md
```

## 📅 開発スケジュール

### フェーズ1: 基盤構築 (Week 1)
- [x] プロジェクト設計
- [ ] Raycast拡張機能の初期化
- [ ] 基本的なプロジェクト構造の作成
- [ ] TypeScript設定とLinter設定

### フェーズ2: API統合 (Week 1-2)
- [ ] tldv APIドキュメントの調査
- [ ] APIクライアントの実装
- [ ] 認証フローの実装
- [ ] エラーハンドリング

### フェーズ3: コア機能実装 (Week 2-3)
- [ ] 録画一覧コマンドの実装
- [ ] 検索機能の実装
- [ ] 録画詳細表示の実装
- [ ] トランスクリプト表示機能

### フェーズ4: UX向上 (Week 3-4)
- [ ] キャッシュ機能の実装
- [ ] ローディング状態の改善
- [ ] エラーメッセージの最適化
- [ ] キーボードショートカット

### フェーズ5: 追加機能 (Week 4)
- [ ] お気に入り機能
- [ ] クイックアクション
- [ ] 共有機能
- [ ] 設定画面

### フェーズ6: テスト・最適化 (Week 5)
- [ ] ユニットテスト作成
- [ ] インテグレーションテスト
- [ ] パフォーマンス最適化
- [ ] バグ修正

### フェーズ7: リリース準備 (Week 5-6)
- [ ] ドキュメント作成
- [ ] Raycast Storeへの申請準備
- [ ] スクリーンショット・動画作成
- [ ] リリースノート作成

## 🔧 環境設定

### 必要要件
- Node.js 18+
- npm 8+
- Raycast 1.50+
- TypeScript 5+

### 開発環境セットアップ
```bash
# プロジェクトの初期化
npx create-raycast-extension tldv-extension --template typescript

# 依存関係のインストール
cd tldv-extension
npm install

# 開発サーバー起動
npm run dev
```

### 環境変数
```env
TLDV_API_KEY=your_api_key_here
TLDV_API_BASE_URL=https://api.tldv.io/v1
```

## 📊 成功指標

### パフォーマンス目標
- 録画一覧の表示: < 500ms
- 検索結果の表示: < 1s
- トランスクリプト読み込み: < 2s

### ユーザビリティ目標
- 3クリック以内で録画にアクセス
- インクリメンタル検索対応
- オフラインでの基本機能動作

### 品質目標
- テストカバレッジ: > 80%
- TypeScript strictモード準拠
- アクセシビリティ対応

## 🚀 デプロイメント

### Raycast Store申請チェックリスト
- [ ] すべてのコマンドが正常動作
- [ ] エラーハンドリング実装済み
- [ ] パフォーマンス要件を満たす
- [ ] ドキュメント完備
- [ ] スクリーンショット準備
- [ ] プライバシーポリシー記載
- [ ] ライセンス明記

## 📝 メモ・考慮事項

### セキュリティ
- APIキーの安全な保存
- センシティブ情報のマスキング
- HTTPSの使用

### パフォーマンス
- 大量データのページネーション
- 画像の遅延読み込み
- キャッシュ戦略

### UX/UI
- ダークモード対応
- キーボードナビゲーション
- レスポンシブデザイン

### 将来の拡張
- AIによる要約生成
- 多言語対応
- チーム機能の追加
- カスタムワークフロー

## 📚 参考資料

- [Raycast開発ドキュメント](https://developers.raycast.com/)
- [tldv APIドキュメント](https://doc.tldv.io/)
- [TypeScript ベストプラクティス](https://www.typescriptlang.org/docs/handbook/intro.html)
- [React Hooks ガイド](https://react.dev/reference/react)

## 🤝 コントリビューション

プルリクエストやイシューの報告を歓迎します。
詳細は[CONTRIBUTING.md](./CONTRIBUTING.md)を参照してください。

## 📄 ライセンス

MIT License - 詳細は[LICENSE](./LICENSE)を参照

---

最終更新: 2024年2月25日