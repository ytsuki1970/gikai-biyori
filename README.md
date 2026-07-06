# 議会びより（非公式）

全国の市町村議会を、町民の目線でやさしくまとめる非公式ポータル**シリーズ**。
「[みんなの国会](https://minna-no-kokkai.com/)」に着想を得た、単一ファイル HTML の非営利プロジェクトです。

## 構成（モノレポ＋サブパス）
```
gikai-biyori/            ← リポジトリ直下＝ gikai-biyori.jp/
  index.html             ← シリーズトップ（まち一覧）
  chikuzen/index.html    ← 筑前町 議会びより（gikai-biyori.jp/chikuzen/）
  CNAME                  ← gikai-biyori.jp
```
新しい自治体版を足すときは `自治体スラッグ/index.html` を追加し、トップの一覧（`index.html` の `.towns`）にカードを1枚足すだけ。各版は `DATA.site` を書き換えれば名前まわりが切り替わります。

---

# 独自ドメイン（gikai-biyori.jp）の取得と接続

## 手順1：ドメインを取得（ご自身で）
1. レジストラで `gikai-biyori.jp` を検索して登録。
   - おすすめ：**Xserverドメイン** / **お名前.com** / **ムームードメイン**（いずれも .jp 対応）。
   - 汎用JP（`gikai-biyori.jp`）でOK。年額の目安 3,000〜4,000円。
2. もし別名（例 `gikaibiyori.jp`）を取った場合は、下の **CNAME ファイルの中身をその名前に合わせて**書き換えてください。

## 手順2：GitHubリポジトリを作成して push
```
cd C:\Users\ytsuk\dev\gikai-biyori
git init
git add .
git commit -m "議会びより：シリーズトップ＋筑前町版"
git branch -M main
git remote add origin https://github.com/ytsuki1970/gikai-biyori.git
git push -u origin main
```

## 手順3：GitHub Pages を有効化＋独自ドメイン設定
1. リポジトリ **Settings → Pages**。
2. Source =「Deploy from a branch」、Branch = `main` / `(root)` → Save。
3. **Custom domain** に `gikai-biyori.jp` と入力して Save（`CNAME` ファイルは同梱済み）。
4. DNS が通ったら **Enforce HTTPS** にチェック。

## 手順4：レジストラ側で DNS を設定
`gikai-biyori.jp`（apex）を GitHub Pages に向けます。**A レコードを4つ**登録：

| 種別 | ホスト/名前 | 値 |
|------|------------|-----|
| A | @（空欄） | 185.199.108.153 |
| A | @（空欄） | 185.199.109.153 |
| A | @（空欄） | 185.199.110.153 |
| A | @（空欄） | 185.199.111.153 |
| CNAME | www | ytsuki1970.github.io |

（任意）IPv6 で AAAA も足す場合：
```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

反映まで数分〜最大48時間。完了後：
- https://gikai-biyori.jp/ → シリーズトップ
- https://gikai-biyori.jp/chikuzen/ → 筑前町 議会びより

## ローカルで見る
```
python -m http.server 8933 --directory .
# → http://localhost:8933/         （トップ）
# → http://localhost:8933/chikuzen/（筑前町版）
```

## 注意（非公式）
各自治体・議会の公式サイトではありません。公開情報を有志がまとめたものです。
議決結果や発言の正確な内容は、必ず公式の会議録・録画配信でご確認ください。
