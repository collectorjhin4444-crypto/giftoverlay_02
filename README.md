# Gift Overlay for TikTok Live Studio

TikTok Live Studio用のギフト紹介オーバーレイです。1080×1920の縦画面に、画像・ギフト名・任意テキストのセットを最大6個ずつ表示し、7個以上ある場合は2秒ごとにページを切り替えてループ表示します。

## ファイル構成

```
/
├ overlay.html      TikTok Live Studioで読み込むオーバーレイ
├ admin.html        編集用ページ(プレビュー付き)
├ data.json         セットデータ
├ images/           webp画像置き場
│  ├ rose.webp
│  ├ cat-paw.webp
│  └ baseball.webp
├ fonts/            フォント置き場
│  ├ NotoSansJP-Black.ttf  (オーバーレイで使用する極太フォント)
│  └ NotoSansJP-Bold.ttf   (予備、現状未使用)
└ README.md
```

## セットアップ

1. このリポジトリをGitHubにアップロード
2. リポジトリ設定で **GitHub Pages** を有効化(Settings → Pages → Source: `main` branch)
3. 公開URLを確認(例: `https://yourname.github.io/your-repo/`)

## 使い方

### 編集 (admin.html)

1. ローカルのブラウザで `admin.html` を開く(またはGitHub PagesのURL `/admin.html` を開く)
2. 「📂 JSON読み込み」で既存の `data.json` をインポート
3. セットの追加・削除・並び替え(↑↓ボタン)・編集
4. 右側のプレビューで実際の見た目を確認
5. 「💾 data.json ダウンロード」でファイルを保存
6. ダウンロードした `data.json` をリポジトリに上書き
7. 画像を追加した場合は `images/` フォルダにも追加
8. `git add`, `git commit`, `git push` でGitHubに反映

### TikTok Live Studio

1. ブラウザソースを追加
2. URL: `https://yourname.github.io/your-repo/overlay.html`
3. 解像度: **幅 1080 × 高さ 1920**
4. カスタムCSS: 不要(背景は最初から透明)

## セットの内容

各セットは以下の3つの項目を持ちます:

```json
{
  "image": "images/rose.webp",
  "name": "ローズ",
  "text": "ありがとう!"
}
```

- **image**: 画像のパス(リポジトリのルートからの相対パス)。168×168の透過webpを推奨
- **name**: ギフト名(画像の右側、上に表示)
- **text**: 任意テキスト(画像の右側、下に表示)

## 動作仕様

- 1ページに最大6セットを縦に並べて表示
- 7個以上ある場合は2秒ごとに次のページにクロスフェード(0.5秒)で切替
- 最後のページの後は1ページ目に戻ってループ
- セットが6個以下の場合は1ページのみ表示し続ける(切替なし)
- セットが0個の場合は何も表示しない
- 画像は左右に±10°ゆっくり揺れるアニメーション
- テキストは白文字に黒い縁取り、極太のNoto Sans JP Black
- フォント読み込み完了まで全体非表示(チラつき防止)
- `data.json` を30秒ごとにポーリングするので、push後しばらく待てば自動反映(リロード不要)
