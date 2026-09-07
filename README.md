# あそびば

娘のための、小さなあそびを集める場所です。
HTML・CSS・JavaScript の静的サイトとして、GitHub Pages で公開します。
パッケージのインストールやビルドは不要です。

## 構成

```text
public/                    # このフォルダーだけを公開
  index.html               # あそびを選ぶトップページ
  assets/style.css          # トップページのスタイル
  ponkey/                  # PonKey（旧 ponkey-site/）
    index.html
    assets/                # ゲームで使う画像
.github/workflows/pages.yml # main への push で自動公開
```

## 手元であそぶ

リポジトリのルートで次を実行し、<http://localhost:8000> を開きます。

```sh
python3 -m http.server 8000 --directory public
```

PonKey はキーボードを押すと音・文字・イラストが出るあそびです。
画面のタップでも音とイラストを楽しめます。
開始時に、対応ブラウザーでは全画面表示になります。
右上の「あそびばへ」からトップページに戻れます。

## GitHub Pages で公開する

1. GitHub のこのリポジトリで **Settings → Pages** を開きます。
2. **Build and deployment → Source** を **GitHub Actions** に設定します。
3. この変更を `main` にコミットして push します。
4. **Actions → Deploy to GitHub Pages** が成功すると公開完了です。
   設定前に push 済みの場合は、同じ画面の **Run workflow** から `main` を選んで再実行できます。

標準の公開先（独自ドメイン未設定の場合）：

- トップページ: <https://esorastudio.github.io/asobiba/>
- PonKey: <https://esorastudio.github.io/asobiba/ponkey/>

以降は `main` への push ごとに自動更新されます。
公開対象は `public/` のみです。README や開発用ファイルは含みません。
GitHub 側で Pages の設定を有効にするまでは、ワークフローの設定処理が失敗することがあります。

参考: [GitHub Pages のカスタムワークフロー（公式ドキュメント）](https://docs.github.com/ja/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)

## あそびを追加する

1. `public/` にあそびごとのフォルダーを作ります（例: `public/drawing/`）。
2. その中に `index.html` と必要な画像・CSS・JavaScript を置きます。
3. `public/index.html` の `.games` 内の `<li>` を複製し、リンク・画像・タイトル・説明を変更します。
   `id` と `aria-labelledby` / `aria-describedby` も新しいあそび固有の名前に変更します。
4. あそびのページに `<a href="../">あそびばへ</a>` を置きます。
5. 手元で確認して `main` に push します。公開設定の変更は不要です。

リンクと画像パスには `./drawing/`、`assets/example.png`、`../` のような相対パスを使います。
`/drawing/` のように `/` から始めると、GitHub Pages の `/asobiba/` 以下ではリンク先がずれます。
各あそびの素材はそのあそびのフォルダー内にまとめ、共通の素材だけ `public/assets/` に置きます。
