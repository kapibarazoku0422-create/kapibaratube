# 🐹 カピバラチューブ

仙人Tubeと全く同じ仕組み（FastAPI + Invidious）でYouTubeを広告なしで見れるサイト。

## 特徴
- **広告なし**
- **埋め込み禁止動画も再生可能**
- **APIキー不要**（Invidious経由なので）
- **超高速**（複数インスタンス同時リクエスト）
- **虹色カピバラチューブロゴ**

---

## デプロイ方法

### 🥇 Render（最推奨・無料）

1. https://render.com にサインイン
2. **New +** → **Web Service**
3. GitHubと連携してこのリポジトリを選択
4. 設定：
   - **Name**: capybara-tube
   - **Region**: Singapore（日本から速い）
   - **Runtime**: Docker
5. **Create Web Service** → 数分でURLが発行される

---

### 🚂 Railway（無料枠あり）

1. https://railway.app にログイン
2. **New Project** → **Deploy from GitHub repo**
3. リポジトリを選択 → **Deploy Now**
4. **Settings** → **Public Networking** → **Generate Domain**

---

### ☁️ Google Cloud Run

```bash
gcloud run deploy capybara-tube \
  --source . \
  --region asia-northeast1 \
  --allow-unauthenticated \
  --port 8000
```

---

### 🖥️ 自前サーバー（Docker）

```bash
git clone <このリポジトリ>
cd capybara-tube
docker build -t capybara-tube .
docker run -d -p 8000:8000 capybara-tube
```

---

## ローカルで試す

```bash
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```
→ http://localhost:8000 で開く

---

## 動画が再生できない場合

`main.py` の `INVIDIOUS_INSTANCES` に稼働中のインスタンスを追加してください。
稼働インスタンス一覧: https://api.invidious.io/

---

## ファイル構成

```
capybara-tube/
├── main.py              # FastAPIバックエンド
├── requirements.txt     
├── Dockerfile           
├── vercel.json          
└── templates/
    ├── base.html        # 共通レイアウト（虹色ロゴ）
    ├── home.html        # ホーム
    ├── search.html      # 検索結果
    ├── watch.html       # 動画視聴（YouTube風レイアウト）
    ├── short.html       # ショート
    ├── channel.html     # チャンネル
    ├── history.html     # 視聴履歴
    ├── status.html      # インスタンス稼働状況
    └── error.html       # エラー
```
