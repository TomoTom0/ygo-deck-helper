# 作業中のタスク

## v0.4.0開発 - Phase 1: 基盤整備

### 開発状況
- **ブランチ**: `feature/v0.4.0-foundation`
- **ベースブランチ**: `dev`
- **開始日**: 2025-11-15
- **現在のバージョン**: 0.3.2 → 0.4.0開発中

### 現在の進捗

#### 完了した作業
- [x] v0.4.0実装順序の計画策定
- [x] 現状の実装状況調査
- [x] 調査結果のドキュメント化（`tmp/wip/v0.4.0-investigation.md`）
- [x] ブランチ作成（`feature/v0.4.0-foundation`）

#### 現在の作業: Phase 1 - 基盤整備

**目標:** URLパラメータ、画像サイズ、テーマ、言語切り替えの基盤実装

##### 1. USPでの制御と再現（優先度：最高）

**目的:** 画面の全状態をURLパラメータで再現可能にする

**現状:**
- ✅ `dno`パラメータのみ実装済み（デッキ番号指定）

**必要な作業:**
- [ ] URLパラメータ仕様の設計
  - 表示モード（list/grid）
  - ソート順
  - カードタブ（info/qa/related/products）
  - 画像サイズ（small/medium/large/llarge）
  - テーマ（dark/light/system）
  - 言語（auto/ja/en/ko/...）
  - フィルター条件
- [ ] 双方向同期の実装（状態↔URL）
- [ ] 各機能との連携
- [ ] テスト作成

**関連ファイル:**
- `src/stores/deck-edit.ts`
- `src/stores/settings.ts`（新規作成予定）

---

##### 2. 画像大きさ変更オプション（優先度：高）

**目的:** 4段階の画像サイズ切り替えを実装

**現状:**
- デッキセクション: 36px × 53px（固定）
- リスト表示: 36px幅
- グリッド表示: 60px幅

**v0.4.0の要件:**
- small（36px）
- medium（60px）
- large（未定義、要検討）
- llarge（未定義、要検討）

**必要な作業:**
- [ ] 設定ストアの作成（`src/stores/settings.ts`）
- [ ] CSS変数の定義（`--card-width`, `--card-height`）
- [ ] 各コンポーネントでCSS変数を使用するよう修正
  - `src/components/DeckCard.vue`
  - `src/components/CardList.vue`
  - `src/components/CardInfo.vue`
- [ ] オプション画面に設定項目追加
- [ ] USPとの連携
- [ ] テスト作成

---

##### 3. カラーテーマ選択（優先度：高）

**目的:** ダーク/ライト/システムテーマの切り替え実装

**現状:**
- CSS変数でグラデーションカラーのみ設定（ハードコード）
- テーマ切り替え機能なし

**必要な作業:**
- [ ] テーマ定義の作成（`src/styles/themes.ts`）
  - ダークテーマ
  - ライトテーマ
  - システムテーマ（`prefers-color-scheme`検出）
- [ ] テーマ適用ロジックの実装
- [ ] オプション画面に設定項目追加
- [ ] USPとの連携
- [ ] 全コンポーネントのテーマ対応確認
- [ ] テスト作成

**関連ファイル:**
- `src/content/edit-ui/index.ts`
- `src/components/DeckEditTopBar.vue`
- `src/components/RightArea.vue`
- `src/components/CardDetail.vue`
- その他全Vueコンポーネント

---

##### 4. 言語を拡張機能内メニューから変更（優先度：高）

**目的:** 拡張機能内で言語を選択できるようにする

**現状:**
- ✅ 言語検出機能実装済み（10言語対応）
- ❌ 言語変更機能なし（公式サイトの設定に依存）

**必要な作業:**
- [ ] 言語設定の永続化（`chrome.storage.local`）
- [ ] API呼び出し時のlocale付与ロジック
  - 全APIファイルの確認と修正
  - `request_locale`パラメータの統一的な付与
- [ ] オプション画面に言語選択UI追加
  - 言語一覧（auto/ja/en/ko/ae/cn/de/fr/it/es/pt）
- [ ] USPとの連携
- [ ] テスト作成（各言語での動作確認）

**課題:**
- 公式サイト側の言語設定との整合性
- セッション管理への影響

**関連ファイル:**
- `src/utils/language-detector.ts`
- `src/api/*.ts`（全APIファイル）
- `src/options/App.vue`

---

### 次のステップ: Phase 2 - UI・データ管理

以下の機能は Phase 1 完了後に着手：

5. デッキメタデータの編集
6. loadダイアログでの画像を含めた実用的な表示
7. デッキ編集画面でシャッフル、ソート、スクショボタン追加
8. 検索チャットでの高度な操作（絞り込み、デッキ内の画像表示）
9. import/export（csv, json, png）

---

### 次のステップ: Phase 3 - 検証機能

以下の機能は Phase 2 完了後に着手：

10. 禁止制限順守確認on/off
11. 禁止制限リストの差分表示

---

## 技術的なメモ

### 開発方針
- TDD（Test-Driven Development）を推奨
- 段階的リリース（Phase 1完了時にv0.4.0-alpha等）
- 基盤が先に完成するので、後続機能の実装が楽になる

### ブラウザ制御
- Chrome DevTools Protocol（CDP）を使用
- Playwrightは使用不可（ログイン制約）
- WebSocket経由でChromiumを制御

### テスト
- 単体テスト: Jest
- E2Eテスト: Chrome CDP経由のNode.jsスクリプト
- テストページ: `https://www.db.yugioh-card.com/yugiohdb/#/ytomo/test`

---

## 参考資料

- **調査結果詳細**: `tmp/wip/v0.4.0-investigation.md`
- **マイルストーン**: `tasks/milestone.md`
- **実装設計**: `docs/design/implementation-design.md`
