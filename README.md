# RakuCSV Studio — 楽天市場の商品登録CSV(normal-item.csv)を作成・点検する無料ツール

**👉 使ってみる(登録不要・無料): https://pshun09156-collab.github.io/rakucsv-studio/**

楽天市場の商品一括登録CSV(`normal-item.csv` / SKU対応)を、ブラウザだけで作成・点検できます。インストール不要、商品データは外部に送信されません。

## こんなエラーで止まっていませんか

アップロードしたCSVが弾かれる原因は、実はパターン化できます。本ツールはこれらを**アップロード前に**検出し、直せるものは自動で修正します。

| よくあるエラー | 本当の原因 | 本ツールの対応 |
|---|---|---|
| 「項目名〇〇は正しくありません」が**全項目**に出る | CSVをUTF-8で保存している | 文字コードを検出し、Shift-JIS(cp932)の修正版CSVを出力 |
| 「商品管理番号欄がないか、文字コードがシフトJISではありません」 | 同上 | 同上 |
| 「項目名〇〇は正しくありません」が**一部だけ** | ヘッダー名の誤記(`商品属性1（項目）`など) | 誤記を検出し正式名に自動修正 |
| 文字化けで弾かれる | 環境依存文字(™ ® ① ½ 絵文字 全角ダッシュ)の混入 | 自動で置換・除去 |
| 「カタログIDもしくはカタログIDなしの理由が必須です」 | SKU行の入力漏れ | 欠落しているSKU行を特定して表示 |
| 「スマートフォン用商品説明文に許可されないHTMLタグ」 | SP用にPC用HTML(div/span/h2/table/style)を流用 | 禁止タグを検出して警告 |
| 「画像パスは相対パスでご指定ください」 | フルURL(`https://…`)を入力している | 該当行を検出 |
| 「ジャンルIDが存在しない/古い」 | ジャンル改編で廃止されたID | 形式チェック(最新IDはRMSで要確認) |

## できること

### 1. CSVを作る
- フォームに入力するだけで、RMSにアップロードできる `normal-item.csv` を生成
- **Shift-JIS(cp932)で出力** — UTF-8保存による全項目エラーを回避
- **マルチSKU(バリエーション)対応** — カラー×サイズなど2軸の選択肢からSKU表を自動生成。組み合わせの作り漏れが起きません
- **複数商品の一括生成** — 商品をリストに積み上げて1ファイルにまとめて出力(単品とマルチSKUの混在可)
- 環境依存文字の自動置換、必須項目・形式チェック、SKU管理番号の重複検出

### 2. 手元のCSVを点検する
すでに作ってあるCSVを読み込ませると、上の表のエラー要因を診断します。文字コード・ヘッダー誤記・環境依存文字は、**修正済みのCSVをその場でダウンロード**できます。

### 3. データは外に出ません
すべての処理がブラウザ内で完結します。商品名・価格・在庫といった店舗の情報がサーバーに送信されることはありません。

## 解説記事(無料)

- [「項目名が正しくありません」が全項目に出るときの直し方](https://pshun09156-collab.github.io/rakucsv-studio/articles/rakuten-csv-error-all-items.html)
- [マルチSKU(バリエーション)商品をCSVで登録する方法](https://pshun09156-collab.github.io/rakucsv-studio/articles/rakuten-multi-sku-csv.html)
- [「カタログIDもしくはカタログIDなしの理由が必須です」の対処法](https://pshun09156-collab.github.io/rakucsv-studio/articles/rakuten-catalog-id-error.html)
- [ジャンルID(全商品ディレクトリID)の調べ方](https://pshun09156-collab.github.io/rakucsv-studio/articles/rakuten-genre-id.html)
- [スマートフォン用商品説明文のタグ制限](https://pshun09156-collab.github.io/rakucsv-studio/articles/rakuten-sp-description-tags.html)
- [「画像パスは相対パスでご指定ください」の直し方](https://pshun09156-collab.github.io/rakucsv-studio/articles/rakuten-image-path-error.html)
- [「必須の商品属性を指定してください」の直し方](https://pshun09156-collab.github.io/rakucsv-studio/articles/rakuten-item-attributes.html)

エラーの全パターンと対策をまとめた [完全攻略ガイド(¥980・エラー辞典/チェックリスト付き)](https://note.com/midas_works/n/ncad7544d90c8) もあります。

## 使い方

1. 上のURLを開く
2. 商品情報・SKU情報を入力 →「チェックしてCSVを生成」
3. エラー・警告を確認し、`normal-item.csv` をダウンロード
4. RMSの「商品一括編集」(またはSFTP `/ritem/batch/`)にアップロード

手元のCSVを点検する場合は、ページ下部の「既存CSVの点検」にファイルを読み込ませてください。

## 免責事項

本ツールは非公式であり、楽天グループ株式会社とは一切関係ありません。無保証で提供されます。生成されたCSVはアップロード前に必ず内容をご確認ください。ジャンルごとの必須商品属性・最新のジャンルIDはRMSでご確認ください。

## 不具合報告・要望

[Issues](../../issues) へお寄せください。「このエラーも検出してほしい」といった要望も歓迎します。

## クレジット

文字コード変換に [encoding.js](https://github.com/polygonplanet/encoding.js) (MIT License) を使用しています。
