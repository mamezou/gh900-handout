# 演習 2 日本語訳：GitHub の概要（Introduction to GitHub）

GitHub Skills「Introduction to GitHub」の日本語訳です。演習そのものは英語で、自分のリポジトリの **Issues** に
Step 1 から順に表示されます。画面の英語とこの訳を見比べながら進めてください。

- ボタン名、ファイル名、ブランチ名、コミットメッセージは、画面と一致させるため英語のままにしています。**指定された名前はそのまま入力してください。** 自動チェックはその名前を見ています。
- 各 Step を終えると、bot（Mona）が同じ Issue に次の Step をコメントします。出るまで 20〜30 秒待って、ページを再読み込みしてください。
- 時間の目安：45 分。ブラウザーだけで完結します。

**演習の開始**: [自分用のリポジトリを作成する](https://github.com/new?template_owner=skills&template_name=introduction-to-github&owner=%40me&name=skills-introduction-to-github&description=Exercise:+Introduction+to+GitHub&visibility=public)
→ **Create repository** を押し、20 秒待ってから再読み込み → **Issues** タブに Step 1 が出ます。

---

## Step 1: ブランチを作る（Create a branch）

「Introduction to GitHub」へようこそ！

**GitHub とは**: Git をバージョン管理に使う共同作業のプラットフォームです。オープンソースソフトウェアを公開・貢献する場として広く使われています。

**リポジトリとは**: ファイルとフォルダーを含むプロジェクトのことです。リポジトリはファイルとフォルダーのバージョンを追跡します。

**ブランチとは**: リポジトリの「並行するバージョン」です。リポジトリには最初 `main` という 1 本のブランチがあり、これが正式版とみなされます。ブランチを追加すると、`main` のコピーの上で、本体に影響を与えずに安全に変更できます。多くの人は、特定の機能に取り組むときにブランチを使います。ブランチがあるので、あなたが作業している間も全員の成果は安全に保たれます。

**プロフィール README とは**: GitHub のプロフィールページの上部に表示される「自己紹介」です。

### ⌨️ やること：最初のブランチ

1. ブラウザーで新しいタブを開き、さっき作った自分のリポジトリ（この演習のコピー）を開きます。説明はこのタブで読み、操作はもう一方のタブで行います。
2. リポジトリ上部のメニューで **< > Code** タブを開きます。

   ![Code タブ](https://raw.githubusercontent.com/skills/introduction-to-github/main/.github/images/code-tab-highlight.png)

3. **main** と書かれたブランチのドロップダウンをクリックします。

   <img width="300" alt="ブランチ選択" src="https://raw.githubusercontent.com/skills/introduction-to-github/main/.github/images/branch-selection-dropdown.png">

4. **Find or create a branch...** の入力欄に `my-first-branch` と入力します。

   > **注**: この名前が次の Step へ進む条件としてチェックされます。

5. **Create branch: `my-first-branch` from main** という文字をクリックしてブランチを作ります。

   <img width="300" alt="ブランチ作成" src="https://raw.githubusercontent.com/skills/introduction-to-github/main/.github/images/create-branch-prompt.png">

   - 作ったブランチに自動で切り替わります。
   - ドロップダウンの表示が新しいブランチ名になります。

6. ブランチが GitHub に作られたので、Mona があなたの作業を確認しています。少し待って、Issue のコメントを見てください。進捗と次の Step が投稿されます。

<details>
<summary>うまくいかないとき 🤷</summary>

- ブランチ名が正確に `my-first-branch` になっているか確認してください（前後に余計な文字を付けない）。
</details>

---

## Step 2: ファイルをコミットする（Commit a file）

ブランチができました！ 🎉

ブランチを作ると、`main` を変えずにプロジェクトを編集できます。次はファイルを作って、最初のコミットをしましょう。

**コミットとは**: プロジェクト内のファイルやフォルダーに対する「変更のひとまとまり」です。コミットはブランチの中に存在します。

### ⌨️ やること：最初のコミット

コミットは、ファイルの追加・削除・名前変更や中身の変更を記録します。この演習では「新しいブランチに新しいファイルを追加する」がコミットになります。

> **注**: `.md` は Markdown ファイルの拡張子です。Markdown は M08 の演習で扱います。

1. **< > Code** タブで、ブランチが `my-first-branch` になっていることを確認します。
2. **Add file** ドロップダウン → **Create new file** をクリックします。

   <img width="300" alt="Create new file" src="https://raw.githubusercontent.com/skills/introduction-to-github/main/.github/images/create-new-file-option.png">

3. **Name your file...** 欄に `PROFILE.md` と入力します。
4. **Enter file contents here** の領域に次の内容を貼り付けます。

   ```
   Welcome to my GitHub profile!
   ```

   ![PROFILE.md の追加](https://raw.githubusercontent.com/skills/introduction-to-github/main/.github/images/add-profile-file.png)

5. 右上の **Commit changes...** をクリックします。ダイアログが開きます。
6. GitHub がコミットメッセージを提案しますが、練習として自分で入れます。**Commit message** 欄に `Add PROFILE.md` と入力します。

   - **コミットメッセージ**と任意の**拡張説明**は、変更の意図を伝えるためのものです。複数ファイルを変えたときに特に役立ちます。

   <img width="400" alt="コミットメッセージ" src="https://raw.githubusercontent.com/skills/introduction-to-github/main/.github/images/commit-message-dialog.png">

7. 他の欄は今は無視して、**Commit changes** をクリックします。
8. Mona が確認しています。Issue のコメントを待ってください。

<details>
<summary>うまくいかないとき 🤷</summary>

- ブランチが `my-first-branch` になっているか確認してください。
- `PROFILE.md` がリポジトリの直下（ルート）に作られているか確認してください。
</details>

---

## Step 3: pull request を開く（Open a pull request）

コミットできました！ ✨

プロジェクトに変更を加えてコミットしたので、次は pull request で「この変更を取り込んでほしい」と提案します。

**pull request とは**: 共同作業は pull request の上で行われます。pull request はあなたのブランチの変更を他の人に見せ、受け入れる・却下する・追加の変更を提案する、ができます。今回の pull request は、あなたのブランチで行った変更を `main` に適用する提案になります。

### ⌨️ やること：pull request を作る

コミットの後、「ブランチに push がありました」というメッセージと **Compare & pull request** ボタンが出ているかもしれません。

![Compare & pull request](https://raw.githubusercontent.com/skills/introduction-to-github/main/.github/images/compare-pull-request-button.png)

このボタンを押せば自動で作成画面に進めます（その場合は下の 5 へ）。練習のため、1〜4 の手動手順でも作れます。

1. リポジトリ上部の **Pull requests** タブをクリックします。
2. **New pull request** ボタンをクリックします。
3. ドロップダウンで次のブランチを選びます。

   - **base:** `main`
   - **compare:** `my-first-branch`

   ![ブランチの選択](https://raw.githubusercontent.com/skills/introduction-to-github/main/.github/images/branch-selection-comparison.png)

4. **Create pull request** をクリックします。
5. pull request のタイトルを入力します。既定ではコミットメッセージが入っていますが、`Add my first file` に書き換えます。
6. 次の欄は変更の**説明**です。ここまでにやったこと（新しいブランチを作った、ファイルを作った、コミットした）を短く書きます。

   ![pull request の作成](https://raw.githubusercontent.com/skills/introduction-to-github/main/.github/images/create-pull-request-form.png)

7. **Create pull request** をクリックします。
8. Mona が確認しています。Issue のコメントを待ってください。

<details>
<summary>うまくいかないとき 🤷</summary>

- pull request のタイトルが `Add my first file` になっているか確認してください。
- 説明欄が空でないか確認してください。
</details>

---

## Step 4: pull request をマージする（Merge your pull request）

よくできました！ 😎

pull request を作れたので、マージします。

**マージとは**: pull request（ブランチ）の変更を `main` に取り込むことです。

![Merge pull request ボタン](https://raw.githubusercontent.com/skills/introduction-to-github/main/.github/images/merge-pull-request-button.png)

### ⌨️ やること：pull request をマージする

1. **Merge pull request** をクリックします。

   > **注**: pull request 上でワークフローが実行中だと、ボタンが押せないことがあります。終わるまで少し待つと押せるようになります。

2. **Confirm merge** をクリックします。

   > **ヒント**: このダイアログ、ファイルを追加したときと似ていませんか？ マージもコミットの一種です。

3. マージが終わったブランチは不要なので、**Delete branch** をクリックして削除します。

   ![Delete branch](https://raw.githubusercontent.com/skills/introduction-to-github/main/.github/images/delete-branch-button.png)

4. Mona が確認して、最後のまとめを投稿します。お疲れさまでした！ 🎉

<details>
<summary>うまくいかないとき 🤷</summary>

- 前の Step がすべて完了しているか確認してください。完了していないとマージボタンが灰色のままです。
</details>

---

## 終わったら

- Microsoft Learn に戻り、モジュールの**知識チェック**（モジュール評価）を受けてください。
- このリポジトリは削除しないでください。後のモジュールで振り返りに使います。
