# 整体院向けスマートカルテ

## プロジェクト概要
患者が自らタブレットで入力する、AI親和性の高い次世代型電子カルテUI。
整体院・接骨院のスタッフ（管理者）および来院患者向け。

## 技術スタック
- **Framework:** Next.js 14+ (App Router)
- **Language:** TypeScript (strict mode)
- **Styling:** Tailwind CSS + shadcn/ui
- **Animation:** Framer Motion
- **Backend/DB:** Supabase (Auth, Database, RLS)
- **Deployment:** Vercel

## ディレクトリ構成
```
src/
├── app/             # Next.js App Router ページ
│   ├── api/         # APIルート
│   ├── patient/     # 患者モード画面
│   └── admin/       # 管理者モード画面
├── components/      # 再利用可能なReactコンポーネント
│   ├── ui/          # shadcn/ui コンポーネント
│   └── features/    # 機能別コンポーネント
├── lib/             # ユーティリティ（Supabaseクライアント等）
├── types/           # TypeScript 型定義
└── hooks/           # カスタムフック
supabase/
├── migrations/      # DBマイグレーション
└── seed.sql         # 初期データ
設計/                 # 設計書（日本語Markdown）
```

## ビルド・テストコマンド
- `npm install` — 依存関係インストール
- `npm run dev` — 開発サーバー起動 (localhost:3000)
- `npm run build` — プロダクションビルド
- `npm run lint` — ESLint実行
- `npm run test` — テスト実行
- `npx supabase migration new <name>` — マイグレーション作成

## コーディング規約

### 命名規則
- **変数・関数:** camelCase（英語）
- **コンポーネント:** PascalCase（英語）
- **DBカラム:** snake_case（Supabase規約準拠）
- **ファイル名:** kebab-case（コンポーネントはPascalCase.tsx）
- **型・インターフェース:** PascalCase、接頭辞なし（IやTは付けない）

### インポート順序
1. React / Next.js
2. 外部ライブラリ
3. 内部モジュール（`@/`エイリアス使用）
4. 型定義

### コンポーネント設計
- 関数コンポーネント + Hooks のみ（クラスコンポーネント禁止）
- Server Components をデフォルトとし、必要な場合のみ `"use client"` を使用
- propsは分割代入で受け取る

### エラーハンドリング
- APIルートではZodでバリデーション
- エラーレスポンス形式: `{ error: string, code: string }`
- Supabase操作は必ずエラーチェック

## デザインガイドライン（Epigenetic AI準拠）
- **ベースカラー:** `#FFFFFF` (White)
- **メインカラー:** `#007BFF` (Epigenetic Navi Blue) — ボタン、進行状況バー
- **アクセント:** `#FF4D4D` (Epigenetic Age Red) — 痛み部位ハイライト
- **サクセス:** `#28A745` (Epigenetic Risk Marker Green) — 完了、保存成功

## 言語方針
- **UIテキスト:** 日本語
- **コード（変数名、コメント等）:** 英語
- **設計書:** 日本語
- **コミットメッセージ:** 英語（Conventional Commits形式）

## データベース方針
- 全テーブルでRow Level Security (RLS) を有効化
- マイグレーションは `supabase/migrations/` にコミット
- 型定義は `supabase gen types` で生成
