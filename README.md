# 整体院向けスマートカルテ

患者が自らタブレットで入力する、AI親和性の高い次世代型電子カルテUI。  
整体院・接骨院のスタッフ（管理者）および来院患者向け。

---

## 技術スタック

| 分野 | 技術 |
|------|------|
| Framework | Next.js 14+ (App Router) |
| Language | TypeScript (strict mode) |
| Styling | Tailwind CSS + shadcn/ui |
| Animation | Framer Motion |
| Backend/DB | Supabase (Auth, Database, RLS) |
| Deployment | Vercel |

---

## ディレクトリ構成

```
EHR/
├── CLAUDE.md                    # Claude Code プロジェクト指示書
├── .claude/
│   ├── settings.json            # Claude Code 設定
│   ├── rules/                   # パス別コーディング規約
│   │   ├── frontend.md          # src/app, src/components 向け
│   │   ├── api.md               # src/app/api 向け
│   │   └── database.md          # supabase/ 向け
│   └── skills/                  # カスタムスラッシュコマンド
│       ├── requirements/        # /requirements
│       ├── basic-design/        # /basic-design
│       ├── detailed-design/     # /detailed-design
│       ├── design/              # /design (進捗確認)
│       ├── implement/           # /implement
│       ├── review/              # /review
│       ├── test/                # /test
│       ├── research/            # /research
│       └── fact-check/          # /fact-check
├── src/
│   ├── app/
│   │   ├── api/                 # APIルート
│   │   ├── patient/             # 患者モード画面
│   │   └── admin/               # 管理者モード画面
│   ├── components/
│   │   ├── ui/                  # shadcn/ui コンポーネント
│   │   └── features/            # 機能別コンポーネント
│   ├── lib/                     # ユーティリティ
│   ├── types/                   # TypeScript 型定義
│   └── hooks/                   # カスタムフック
├── supabase/
│   ├── migrations/              # DBマイグレーション
│   └── seed.sql
└── 設計/                        # 設計書
    ├── 01_要件定義.md
    ├── 02_基本設計.md
    └── 03_詳細設計.md
```

---

## セットアップ

```bash
npm install
npm run dev       # http://localhost:3000
```

| コマンド | 説明 |
|---------|------|
| `npm run dev` | 開発サーバー起動 |
| `npm run build` | プロダクションビルド |
| `npm run lint` | ESLint 実行 |
| `npm run test` | テスト実行 |
| `npx supabase migration new <name>` | マイグレーション作成 |

---

## Claude Code スキル一覧

このプロジェクトでは Claude Code のカスタムスキル（スラッシュコマンド）を使って AI と協力して開発を進めます。

### 設計フェーズ

| コマンド | エージェント | モデル | 用途 |
|---------|------------|--------|------|
| `/design` | 設計ナビゲーター | Sonnet | 設計全体の進捗確認・次のアクション提案 |
| `/requirements` | ビジネスアナリスト | Opus | 要件定義書の作成・更新・レビュー |
| `/basic-design` | シニアアーキテクト | Opus | 基本設計書（画面設計・DB設計・API設計） |
| `/detailed-design` | リードエンジニア | Opus | 詳細設計書（型定義・処理フロー・実装仕様） |

### 実装フェーズ

| コマンド | エージェント | モデル | 用途 |
|---------|------------|--------|------|
| `/implement` | シニアエンジニア | Opus | 設計書に基づいてコードを実装 |
| `/review` | シニアエンジニア | Opus | コードレビュー（セキュリティ・品質・設計整合性） |
| `/test` | QAエンジニア | Sonnet | テストコードの作成・実行 |

### 調査・品質管理

| コマンド | エージェント | モデル | 用途 |
|---------|------------|--------|------|
| `/research` | テックリサーチャー | Sonnet | 技術調査・ライブラリ比較 |
| `/fact-check` | 品質保証スペシャリスト | Sonnet | コードと設計書の整合性検証 |

---

## 推奨ワークフロー

### 設計から始める場合

```
/design                            # 全体の進捗確認
/requirements 作成                 # 要件定義書を作成（ヒアリング付き）
/requirements レビュー             # 要件の品質チェック
/basic-design 作成                 # 基本設計（全体）
/basic-design 作成 DB設計          # DB設計だけ絞って作成
/detailed-design 作成 患者入力画面  # 特定画面の詳細設計
/fact-check 設計書                 # 設計書間の整合性確認
```

### 実装する場合

```
/implement 患者入力画面             # 設計書を読んで実装
/review 直近の変更                  # 実装したコードをレビュー
/test src/components/BodyMap.tsx   # テストを生成・実行
```

### 技術的な疑問がある場合

```
/research ボディマップSVG実装       # SVGボディマップの実装方法を調査
/research Supabase RLS設計         # RLSのベストプラクティスを調査
```

### 整合性チェック

```
/fact-check 全体                   # プロジェクト全体を検証
/fact-check DB                     # DB スキーマと型定義の整合性
/fact-check 設計書                 # 設計書間の矛盾を検出
```

---

## デザインガイドライン（Epigenetic AI 準拠）

| 役割 | カラーコード | 用途 |
|------|------------|------|
| ベース | `#FFFFFF` | 背景 |
| メイン | `#007BFF` | ボタン、進行状況バー |
| アクセント | `#FF4D4D` | 痛み部位ハイライト |
| サクセス | `#28A745` | 完了メッセージ、保存成功 |
