# パワポDTPメモ

### 用紙サイズ

| サイズ | mm        | 300dpi      | 600dpi      |
|:-----:|:---------:|:-----------:|:-----------:|
| A4    | 297 x 210 | 3507 x 2480 | 7015 x 4960 |
| B5    | 257 x 182 | 3035 x 2149 | 6070 x 4299 |
| A5    | 210 x 148 | 2480 x 1748 | 4960 x 3496 |
| はがき | 148 x 100 | 1748 x 1181 | 3496 x 2362 |
| L判   | 127 x 89  | 1500 x 1051 | 3000 x 2102 |
| 名刺  | 91 x 55   | 1074 x 649  | 2149 x 1299 |


### CubePDFなどで、塗り足し込みのサイズでPDFにする

⇒オリジナルの用紙サイズをユーザー定義として登録する

[NEC LAVIE公式サイト > サービス＆サポート > Q&A > Q&A番号 021048](https://faq.nec-lavie.jp/qasearch/1007/app/servlet/relatedqa?QID=021048)


### 印刷時に画像の解像度が低い

⇒解決策不明。暫定対応としてPNG書き出ししてからpdf_asでPDF化

[PowerPoint から高解像度 (高dpi) スライドをエクスポートする方法 - Office | Microsoft Docs](https://docs.microsoft.com/ja-jp/office/troubleshoot/powerpoint/change-export-slide-resolution)

例では300までしか書かれていないが、600に設定したら600dpiでPNG化できた
