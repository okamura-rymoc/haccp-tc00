# HACCP 衛生管理（Streamlit）— Render デプロイ手順

## 同梱物
- `haccp_1_app.py` … アプリ本体（DB/ログは `DATA_DIR` → 既定 `/app/data`）
- `requirements.txt`
- `Dockerfile`

## 環境変数（任意）
- `COMPANY_NAME` … PDFに表示する会社名（既定: 株式会社○○○○○）
- `FACTORY_NAME` … PDFに表示する工場名（既定: △△△△工場）
- `DATA_DIR` … 変更不要（既定 `/app/data`）

## Render での手順（概要）
1. 本ディレクトリ一式を GitHub リポジトリに push
2. Render ダッシュボード → **New > Web Service**
3. リポジトリを選択 → Docker を自動認識
4. （任意）**Environment** に `COMPANY_NAME` `FACTORY_NAME` `CLIENT_ID` を追加
5. （推奨）**Disks** で Persistent Disk を `/app/data` にマウント
6. Deploy → `https://xxxxx.onrender.com` で動作確認
7. **Settings > Custom Domains** で `haccp-xxx.rymoc.co.jp` を追加
   ムームードメイン側で CNAME を「DNS Target」に向ける

## ローカル確認
```bash
docker build -t haccp-app .
docker run --rm -p 8501:8501 -v $(pwd)/data:/app/data -e COMPANY_NAME="株式会社テスト" -e FACTORY_NAME="第一工場" haccp-app
# → http://localhost:8501
```