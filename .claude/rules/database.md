---
paths:
  - "supabase/**"
  - "src/lib/supabase*"
  - "src/types/database*"
---

# データベース規約

## テーブル設計
- テーブル名・カラム名は snake_case
- 全テーブルに `id` (UUID, PK), `created_at`, `updated_at` を含める
- 外部キーには `_id` サフィックスを付ける（例: `patient_id`）

## Row Level Security (RLS)
- 全テーブルで RLS を必ず有効化
- ポリシーは最小権限の原則に従う
- 管理者ロールと患者ロールを明確に分離

## マイグレーション
- ファイル名: `YYYYMMDDHHMMSS_description.sql`
- 1マイグレーション1責務（複数テーブルの変更を1ファイルに混ぜない）
- ロールバック可能な変更を心がける
- 本番データを破壊する変更は段階的に行う

## 型生成
- スキーマ変更後は `supabase gen types typescript` で型を再生成
- 生成された型を `src/types/database.ts` に配置
- 手動で型を書かず、生成された型を使用する
