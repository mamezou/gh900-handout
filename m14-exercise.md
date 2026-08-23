# 演習 14 日本語訳：pull request をレビューする（Review pull requests）

GitHub Skills「Review pull requests」の日本語訳です。演習の本文は英語で、自分のリポジトリの **Issues** に
Step 1 から順に表示されます。画面の英語と日本語訳を見比べながら進めてください。

- ボタン名、ファイル名、ブランチ名、pull request のタイトル、コミットメッセージは、画面と一致させるため英語のままにしています。**指定された名前は変えずに入力してください。** 自動チェックは名前を見ています。
- 各 Step を終えると、bot（Mona）が同じ Issue に次の Step をコメントします。出るまで 20〜30 秒待って、ページを再読み込みしてください。
- 時間の目安：30 分（Step 1〜5）。ブラウザーだけで完結します。

**演習の開始**: [自分用のリポジトリを作成する](https://github.com/new?template_owner=skills&template_name=review-pull-requests&owner=%40me&name=skills-review-pull-requests&description=Exercise%3A+Review+pull+requests&visibility=public)
→ **Create repository** を押し、20 秒待ってから再読み込み → **Issues** タブに Step 1 が出ます。

---

## Step 1: pull request を開く（Open a pull request）

まずは、`update-game` ブランチに最近追加された変更について **pull request** を開くところから始めます。

### 📖 理論：pull request とは

**pull request** は、あるブランチの作業を別のブランチへマージする前にレビューするための共同作業の場です。会話の管理と変更の確認をしやすくするため、いくつかのタブに分かれています。

- **Conversation** — pull request の活動記録です。共同作業者やコミュニティが、アイデア・提案・全般的なフィードバックを書き込む場でもあります。
- **Commits** — 提案元のブランチにだけ存在するコミットの一覧です。
- **Checks** — GitHub Actions による自動処理を pull request に適用したときの結果です。Checks は別の演習で扱います。😎
- **Files Changed** — 変更前後を見比べられる差分（Diff）の表示です。Diff の画面からコメントやレビューを追加することもできます。

> **ヒント**: 作業が途中のものは、下書きの pull request（draft pull request）として作成できます。誤ってマージされたり、早すぎるタイミングでレビューされたりするのを防げます。

### ⌨️ やること：pull request を作る

1. ブラウザーで新しいタブを開き、演習用のリポジトリを開きます。説明は元のタブで読み、操作は新しいタブで行います。

2. 上部のメニューで **Pull requests** タブを選びます。

3. 右側の **New pull request** ボタンをクリックします。

4. **Compare changes** の欄で次のとおり選び、**Create pull request** ボタンをクリックします。

   - **base:** `main`
   - **compare:** `update-game`

5. **title**（タイトル）と **description**（説明）に次の内容を入力します。

   ```md
   Update game over message
   ```

   ```md
   Update the game over message so people know how to play again!
   ```

6. **Create pull request** をクリックします。

7. pull request ができたので、Mona が確認しています。Issue のコメントを待ってください。進捗と次の Step が投稿されます。

---

## Step 2: 自分を担当者にする（Assign yourself）

pull request を開けました！ 👋

### 📖 理論：pull request の担当者（assignee）

**pull request の担当者（assignee）** は、変更内容をいちばんよく知っている人のことです。質問があるときに誰へ連絡すればよいかを把握しておくための、簡単なしくみです。

### ⌨️ やること：自分を担当者にする

1. さきほど作った pull request を開いていない場合は、戻ります。

2. 右側の **Assignees** の下にある **assign yourself** という文字をクリックします。

3. 自分を担当者にすると、Mona が確認しています。Issue のコメントを待ってください。

---

## Step 3: レビューする（Leave a review）

自分を担当者にできました！ 🎉

### 📖 理論：pull request のレビュー

**pull request のレビュー** は、他の共同作業者やコミュニティのメンバーから、提案された変更に対してもらうフィードバックです。品質を保ち、プロジェクトを前に進めるのに役立ちます。さらに大切なのは、他の人が問題にどう取り組んでいるかを見て、プロジェクトへの理解を深め、開発者として成長できる機会になることです。

レビューをもらういちばんの方法は、依頼することです。レビュアーを指定すると、レビュアーは次の 3 つの方法でフィードバックできます。

- **Comment** — 承認も却下もしない、一般的なフィードバックです。
- **Approve** — ルールセット、コードオーナー、ほかのポリシーが適用されている場合に、マージを可能にします。
- **Request Changes** — 提案された変更が期待に達しておらず、追加の作業が必要という意味です。修正後に、あらためてレビューを依頼します。

**Files changed** タブが、フィードバックを集める主な場所です。レビューを提出する前に、行に直接コメントを付けられます。

#### レビューの一般的な進め方

1. **title**（タイトル）と **description**（説明）が明確で簡潔かを確認します。意図した変更と、関連する Issue が分かるようになっているのが望ましいです。

2. **Files changed** タブを確認し、提案されたコードがすべて説明どおりかを確かめます。

3. たいていの変更では、実際に動かしてみて、意図どおりかを検証します。

4. レビューの要件、テスト、品質確認などについては、リポジトリのコントリビューションガイドを参照します。

#### レビューの観点

- 潜在的な問題・リスク・制約を見つける。
- 変更や改善を提案する。
- レビュー中の pull request が考慮していない、今後の変更について知らせる。
- 認識が合っているかを確かめる質問をする。
- 作成者がうまくやれている点、今後も続けてほしい点を挙げる。
- 重要なフィードバックから優先して伝える。
- 簡潔に、かつ意味のある詳しさで書く。
- pull request の作成者に敬意と思いやりを持って接する。

### ⌨️ やること：レビューする

1. pull request で **Files changed** タブをクリックします。

2. 変更内容をひととおり確認します。

   - 変更は単純な言い回しの調整であることに注目してください。

3. 差分表示の上にある **Submit review** ボタンをクリックします。

4. 次のコメントを入力し、**Submit review** ボタンをクリックします。

   ```md
   Looks good to me. I think this is more intuitive. Nice work!
   ```

   <img width="300" alt="Submit review ボタン" src="https://raw.githubusercontent.com/skills/review-pull-requests/main/.github/images/submit-review-button.png" />

   > 🪧 **注**: 自分の pull request に対しては、**Approve** と **Request changes** は選べません。

5. レビューを提出すると、Mona が確認しています。Issue のコメントを待ってください。

   > ❗ **注意**: まだ pull request をマージしないでください。

---

## Step 4: 変更を提案する（Suggest changes）

レビューできました ✨

レビューをしていると、説明するより直したほうが早い、ちょっとした変更が見つかることがよくあります。誤字や言い回しの修正などです。こうした場面では **Add a suggestion** の機能がぴったりです。

### 📖 理論：suggested changes（変更の提案）

**Add a suggestion** は、コメント入力欄にあるボタンです。押すと、専用の書式のコードブロックが挿入されます。GitHub は、コメントを表示するだけでなく **Commit suggestion** ボタンも表示します。作成者はボタンひとつで提案を受け入れてコミットできます。コードエディターを開く必要はありません。便利ですね！

### ⌨️ やること：変更を提案する

1. pull request で **Files changed** をクリックします。

2. `index.html` ファイルの差分表示を探します。

3. 変更された行の行番号の横にカーソルを合わせます。

4. プラスのアイコンをクリックすると、クリックした行へのコメント入力欄が開きます。

5. **Add a suggestion** ボタンをクリックすると、元の行が編集できる形で挿入されます。

   <img width="300" alt="Add a suggestion ボタン" src="https://raw.githubusercontent.com/skills/review-pull-requests/main/.github/images/add-a-suggestion-button.png" />

6. 提案の内容を次のとおりに書き換え、**Comment** ボタンをクリックします。

   ````md
   ```suggestion
   <h2 hidden>Game over! Want to play again?! Just click refresh. 🧑‍🚀!</h2>
   ```
   Let's make it a bit more friendly. 🤓
   ````

### ⌨️ やること：提案された変更を適用する

1. pull request のメニューで **Conversation** タブを選びます。

2. 下へスクロールし、**Commit suggestion** ボタンをクリックすると、コミットメッセージの入力欄が開きます。

3. コミットメッセージを次の内容に書き換え、**Commit changes** ボタンをクリックします。

   ```markdown
   Make the end game experience more friendly
   ```

4. 変更をコミットすると、Mona が確認しています。Issue のコメントを待ってください。

---

## Step 5: pull request をマージする（Merge your pull request）

あと少しです！ ❤️

レビューが集まり、フィードバックも反映できたので、変更をマージします。

### ⌨️ やること：pull request をマージする

1. pull request のメニューで **Conversation** タブを選びます。

2. 下へスクロールし、**Merge pull request** ボタンをクリックします。

3. （任意）`update-game` ブランチを削除します。

4. pull request をマージすると、Mona が確認して、最後のまとめを投稿します。お疲れさまでした！ 🎉

---

## 終わったら

- Microsoft Learn に戻り、モジュールの**知識チェック**（モジュール評価）を受けてください。
- 作成したリポジトリは削除しないでください。後のモジュールで振り返りに使います。
