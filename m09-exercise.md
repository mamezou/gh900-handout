# 演習 9：最初の pull request（First Contributions）

実在のオープンソースプロジェクト [First Contributions](https://github.com/firstcontributions/first-contributions) に
pull request を出します。「初めて貢献する人の練習」を受け入れるために運営されているので、安心して提出してください。

本家に日本語の手順があります：
[README.ja.md](https://github.com/firstcontributions/first-contributions/blob/main/docs/translations/README.ja.md)

ただし本家の README は**手元の PC に Git が入っている前提**で `git clone` から始まります。この研修では PC に Git を
入れていないので、**GitHub 上で fork し、その fork に Codespace を作って、そのターミナルで操作**します。Codespace の中には
リポジトリがすでに置かれているので `git clone` は行いません。それ以外は本家の手順と同じです。

- ボタン名、コマンド、ファイル名、ブランチ名は画面と一致させるため英語のままにしています。
- 提出内容は**インターネットに公開されます**。実名やメールアドレスは不要です。GitHub のユーザー名で構いません。
- 時間の目安：30 分。終わったら Microsoft Learn の知識チェックへ進んでください。

---

## 手順（Codespace で行う）

1. [First Contributions](https://github.com/firstcontributions/first-contributions) を開き、README をざっと読みます。
2. 右上の **Fork** → **Create fork** を押します。自分のアカウントにコピー（fork）ができます。
3. **自分の fork のページ**で **< > Code** → **Codespaces** タブ → **Create codespace on main** を押します。
   1〜3 分で VS Code の画面が開きます。**「自分の fork のページ」から作るのが大事です。**
   元のリポジトリ側で Codespace を作ると、あとで push できません。

4. ターミナルを開き（`Ctrl+Shift+P` → `View: Toggle Terminal`）、作業用のブランチを作ります。
   `<your-name>` は自分の名前やユーザー名に置き換えてください。

   ```bash
   git switch -c add-<your-name>
   ```

5. 左のエクスプローラーで `Contributors.md` を開きます。名前がずらりと並んでいるので、**先頭と末尾は避けて**、
   途中のどこかに自分の 1 行を追加して保存します。書き方は前後の行に合わせてください。

   ```md
   - [<GitHub ユーザー名>](https://github.com/<GitHub ユーザー名>)
   ```

6. 変更が 1 行だけになっているか確認します。

   ```bash
   git status
   git diff
   ```

7. 変更をステージして、コミットします。

   ```bash
   git add Contributors.md
   git commit -m "Add <your-name> to Contributors list"
   ```

8. 自分の fork に push します。Codespace には GitHub の認証が済んでいるので、パスワードは聞かれません。

   ```bash
   git push -u origin add-<your-name>
   ```

9. ブラウザーで自分の fork のページを開くと、**Compare & pull request** ボタンが出ています。押してください。
10. 画面上部の **base** が元のリポジトリの `main`、**compare** が自分のブランチになっているか確認します。
11. 件名と本文を書いて **Create pull request** を押します。本文にはテンプレートが入っているので、
    当てはまる項目の `[ ]` を `[x]` にしてください。

提出できたら完了です。しばらくすると保守担当者が `main` にマージし、完了のメールが届きます。

---

## Codespace が使えないとき（ブラウザーだけで行う）

1. fork を作るところまでは同じです（手順 1〜2）。
2. 自分の fork で `Contributors.md` を開き、鉛筆アイコン（**Edit this file**）を押します。
3. 先頭と末尾を避けて、途中に自分の 1 行を追加します。
4. 右上の **Commit changes...** を押し、ダイアログで
   **Create a new branch for this commit and start a pull request** を選び、ブランチ名を入れてコミットします。
5. そのまま pull request の作成画面に進むので、base と compare を確認して **Create pull request** を押します。

## pull request の件名と本文の書き方

- 件名は「この変更を適用すると〜する」と読める形で、命令形・現在形で書きます（`added` ではなく `add`）。
- 件名は 50 文字以内。大文字で始めて、末尾にピリオドは付けません。
- 本文には「何を変えたか」と「なぜ変えたか」を書きます。「どうやって」は書きません。

## 終わったら

- Microsoft Learn に戻り、モジュールの**知識チェック**（5 分）を受けてください。
- **fork は削除しないでください。** マージされるまでブランチが必要です。Codespace は停止だけしてください。
- pull request の URL を控えておいてください。モジュールのまとめで使います。
