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
- [x] **Phase 1 - 基盤整備** ✅

#### Phase 1 完了（2025-11-15）

**目標:** URLパラメータ、画像サイズ、テーマ、言語切り替えの基盤実装

**成果:**
- ✅ Week 1（基盤実装）
  - 型定義拡張（`src/types/settings.ts`）
  - テーマシステム実装（`src/styles/themes.ts`, `themes.css`）
  - 設定ストア実装（`src/stores/settings.ts`）
  - URLステートマネージャー実装（`src/utils/url-state.ts`）
- ✅ Week 2（UI統合・テスト）
  - deck-editストアへのUSP統合
  - テーマCSS読み込み
  - カードサイズ・テーマのCSS変数適用
  - オプション画面の拡張（SettingsPanel.vue）
  - E2Eテスト作成（全6テスト成功）

**残タスク:**
- [ ] ドキュメント更新（README.md, CHANGELOG.md）
- [ ] Phase 2への移行準備

#### 現在の作業: ドキュメント更新

##### ✅ 1. USPでの制御と再現（完了）

**実装内容:**
- ✅ URLパラメータ仕様の設計・実装
  - UI状態: mode, sort, tab, ctab, detail
  - 設定: size, theme, lang, dno
- ✅ 双方向同期の実装（`URLStateManager`）
- ✅ deck-editストアとの連携
- ✅ テスト作成（E2Eテスト）

**成果物:**
- `src/utils/url-state.ts`
- `src/stores/deck-edit.ts`（USP統合）

---

##### ✅ 2. 画像大きさ変更オプション（完了）

**実装内容:**
- ✅ 設定ストアの作成（`src/stores/settings.ts`）
- ✅ CSS変数の定義（`--card-width`, `--card-height`）
- ✅ 4段階サイズ定義
  - small: 36×53px
  - medium: 60×88px
  - large: 90×132px
  - xlarge: 120×176px
- ✅ コンポーネント修正
  - `src/components/DeckCard.vue`
  - `src/components/CardList.vue`
- ✅ オプション画面に設定項目追加（SettingsPanel.vue）
- ✅ USPとの連携
- ✅ テスト作成

**成果物:**
- `src/types/settings.ts`（型定義）
- `src/stores/settings.ts`（設定管理）
- `src/options/SettingsPanel.vue`（UI）

---

##### ✅ 3. カラーテーマ選択（完了）

**実装内容:**
- ✅ テーマ定義の作成（`src/styles/themes.ts`, `themes.css`）
  - ダークテーマ（28 CSS変数）
  - ライトテーマ（28 CSS変数）
  - システムテーマ（`prefers-color-scheme`検出）
- ✅ テーマ適用ロジックの実装
- ✅ オプション画面に設定項目追加
- ✅ USPとの連携
- ✅ テスト作成

**成果物:**
- `src/styles/themes.ts`
- `src/styles/themes.css`
- `src/stores/settings.ts`（テーマ管理機能）

---

##### ✅ 4. 言語を拡張機能内メニューから変更（完了）

**実装内容:**
- ✅ 言語設定の永続化（`chrome.storage.local`）
- ✅ オプション画面に言語選択UI追加
  - 言語一覧（auto/ja/en/ko/ae/cn/de/fr/it/es/pt）
- ✅ USPとの連携

**成果物:**
- `src/options/SettingsPanel.vue`（言語選択UI）
- `src/stores/settings.ts`（言語設定管理）

**残課題（Phase 2以降）:**
- API呼び出し時のlocale付与ロジック
- 全APIファイルの修正
- 公式サイト側の言語設定との整合性確認

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
