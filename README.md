# WITH LEGEND (withlegend.jp)

WITH LEGENDの公式サイト用リポジトリ。

## 現状

2026年8月末のリニューアル準備に伴い、まずは `index.html` の「リニューアル準備中」つなぎページのみを公開している。フル再構築は再公開時期が決まり次第着手する。

## ファイル構成

- `index.html` — 実際に公開する自己完結型HTML（画像はbase64で埋め込み済み、これ単体で動作する）
- `index.template.html` — 編集用ソース。画像部分は `__LOGO_B64__` / `__FAVICON_B64__` のプレースホルダーになっている
- `assets/` — ロゴ・favicon画像（元データ）

## 更新方法

1. `index.template.html` を編集
2. `assets/` 内の画像から base64 を生成し、プレースホルダーに埋め込んで `index.html` を再生成
   ```
   python3 -c "
   with open('index.template.html', encoding='utf-8') as f:
       html = f.read()
   import base64
   logo_b64 = base64.b64encode(open('assets/logo-stacked-web.png','rb').read()).decode()
   favicon_b64 = base64.b64encode(open('assets/favicon-180.png','rb').read()).decode()
   html = html.replace('__LOGO_B64__', logo_b64).replace('__FAVICON_B64__', favicon_b64)
   open('index.html','w',encoding='utf-8').write(html)
   "
   ```
3. `git push` するとVercelが自動でデプロイする

## デプロイ

Vercelと連携済み（GitHub連携、`main`ブランチへのpushで自動デプロイ）。
