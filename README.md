# ゴルフ組分けコーディネーター

参加者の組分けを支援する単一HTMLのWebアプリです。

## 構成

- `public/` — 公開されるファイルのみを置く。ここに置いたものは全世界から閲覧可能になる
- `public/_headers` — セキュリティヘッダ。CSPで通信先を許可リスト方式に限定している
- `wrangler.jsonc` — Cloudflare Workersの設定

### 接続先を追加するときは `_headers` も更新する

CSPは許可リスト方式なので、**新しい外部URLを使うコードを書いたら `_headers` の `connect-src` に
足さないとブラウザに遮断される**。設定画面でURLを変更できる箇所も同様。

現在の許可先（`connect-src`）:

| 用途 | ホスト |
|---|---|
| 住所・地名検索 | msearch.gsi.go.jp |
| 地物データ検索 | overpass-api.de / overpass.kumi.systems |
| 経路探索 | router.project-osrm.org / routing.openstreetmap.de |

## デプロイ

`main`ブランチへのpushで、Cloudflare Workersに自動でビルド・公開されます。

- 公開URL: https://golf-pairing.my-sakura.workers.dev

### 初回のみ必要な設定

Cloudflareダッシュボード → Workers & Pages → `golf-pairing` → 設定 → ビルド →
「リポジトリに接続」で、このリポジトリと `main` ブランチを指定する。
デプロイコマンドは `npx wrangler deploy`、ビルドコマンドは空欄。

## 経緯

もともとCloudflareへ手動デプロイのみで運用しており、リポジトリが存在しなかった。
公開中のファイルを回収してこのリポジトリを作成している。
