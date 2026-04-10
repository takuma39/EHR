---
paths:
  - "src/app/api/**"
---

# API ルート規約

## ルート設計
- RESTful: `src/app/api/[resource]/route.ts` の形式
- HTTP メソッドに応じた関数をexport（GET, POST, PUT, DELETE）

## バリデーション
- リクエストボディは Zod スキーマで必ずバリデーション
- バリデーションエラーは 400 で返す

## レスポンス形式
- 成功: `{ data: T }` + 適切なステータスコード（200, 201, 204）
- エラー: `{ error: string, code: string }` + 適切なステータスコード
- Content-Type: `application/json`

## 認証
- 管理者APIは Supabase Auth の JWT を検証
- `supabase.auth.getUser()` でユーザー確認
- 未認証は 401、権限不足は 403 を返す

## セキュリティ
- SQLインジェクション対策: Supabase クライアントのパラメータバインディングを使用
- 入力値のサニタイズを必ず行う
- CORS設定を適切に管理
