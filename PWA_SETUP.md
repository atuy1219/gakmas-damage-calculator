# PWA (Progressive Web App) セットアップ

## 概要
このアプリケーションは、GitHub Pages上でPWA（Progressive Web App）としてインストール可能です。

## 変更内容

### 問題
GitHub Pagesでプロジェクトページとして公開する場合、アプリケーションはサブディレクトリ（例: `https://atuy1219.github.io/gakmas-score-calculator/`）から配信されます。
以前のPWA設定では絶対パス（`/`で始まるパス）を使用していたため、サブディレクトリから配信される場合に正しく動作しませんでした。

### 解決策
以下のファイルを相対パス（`./`で始まるパス）を使用するように修正しました：

1. **manifest.json**
   - `id`: `/` → `./`
   - `start_url`: `/` → `./`
   - `scope`: `/` → `./`
   - アイコンのパス: `icon-192.png` → `./icon-192.png`

2. **service-worker.js**
   - キャッシュするリソースのパスを相対パスに変更
   - `/index.html` → `./index.html`など

3. **index.html**
   - Service Workerの登録パス: `/service-worker.js` → `./service-worker.js`

## PWA要件
このアプリケーションは以下のPWA要件を満たしています：

- ✅ Web App Manifest (`manifest.json`)
- ✅ Service Worker (`service-worker.js`)
- ✅ HTTPS配信（GitHub Pagesにより提供）
- ✅ 適切なサイズのアイコン（192x192、512x512）
- ✅ `display: standalone` 設定
- ✅ テーマカラーとバックグラウンドカラー
- ✅ Apple iOS PWAサポート用のメタタグ

## インストール方法

### デスクトップ（Chrome、Edge）
1. アプリケーションをブラウザで開く
2. アドレスバーの右側にある「インストール」アイコンをクリック
3. 確認ダイアログで「インストール」をクリック

### モバイル（Android）
1. Chrome でアプリケーションを開く
2. メニュー（⋮）から「ホーム画面に追加」を選択
3. 名前を確認して「追加」をタップ

### iOS
1. Safari でアプリケーションを開く
2. 共有ボタン（□↑）をタップ
3. 「ホーム画面に追加」を選択
4. 名前を確認して「追加」をタップ

## 開発者向け情報

### ローカルでのテスト
PWAはHTTPSまたはlocalhostでのみ動作します。ローカルでテストする場合：

```bash
# Python 3を使用
python3 -m http.server 8000

# Node.jsを使用（http-serverパッケージ）
npx http-server -p 8000
```

その後、`http://localhost:8000`にアクセスしてください。

### キャッシュのクリア
Service Workerのキャッシュをクリアする場合：
1. ブラウザの開発者ツールを開く
2. Application/アプリケーションタブを選択
3. Service Workersセクションで「Unregister」をクリック
4. Cacheセクションで古いキャッシュを削除
5. ページをリロード
