# 演習 15 日本語訳：リポジトリで点をつなげる（Connect the dots）

GitHub Skills「Connect the dots」の日本語版です。開始リンクは日本語化したテンプレート（`mamezou/skills-ja-connect-the-dots`）を指しており、自分のリポジトリの README に Step 1 から順に**日本語で**表示されます。画面と同じ内容を、手元で読み返す用に載せています。

- ボタン名、ファイル名、ブランチ名、コミットメッセージは、画面と一致させるため英語のままにしています。**指定された名前は変えずに入力してください。** 自動チェックは名前を見ています。
- 各 Step を終えると、GitHub Actions が README を次の Step に書き換えます。出るまで 20〜30 秒待って、ページを再読み込みしてください。
- 時間の目安：25 分（Step 1〜3）。ブラウザーだけで完結します。

**演習の開始**: [自分用のリポジトリを作成する](https://github.com/new?template_owner=mamezou&template_name=skills-ja-connect-the-dots&owner=%40me&name=skills-connect-the-dots&description=My+clone+repository&visibility=public)
→ **Create repository** を押し、20 秒待ってから再読み込み → リポジトリの **README** に Step 1 が出ます。

> **注意**: このページは手順の全体像です。実施するときは、まず上の開始リンクから自分のリポジトリを作り、
> リポジトリの **README** に表示される手順に沿って進めてください。このページは読み返し用です。

---

## Step 1: 重複した Issue を整理する（Resolve duplicate issues）

コースへようこそ 🎉

GitHub には、GitHub 上の別の情報を参照するための特別な機能があります。たとえば、別の Issue や pull request を番号で参照すると、番号がリンクになります。同時に、リンク先の Issue や pull request の側にも相互参照（cross-reference）が作られます。双方向の参照によって、GitHub 上の情報どうしの関係を追えます。

![Issue から PR へのリンクと、PR 側に作られた相互参照](https://user-images.githubusercontent.com/6351798/172456846-2daec570-08b0-4ffa-a7cb-41acc50b836e.png)

複数のメンバーで共同作業をしていると、Issue が重複することがあります。上の例では、新しい Issue `#8346` が以前の Issue `#8249` の重複です。相互参照の機能があるので、こうした重複をたどり、適切なタイミングで Issue をクローズできます。

### 参照を作る（Creating references）

別の Issue へリンクすると、GitHub の中に参照が自動で作られます。完全な URL を書く必要すらありません。コメントの中に `#5` と入力すれば、Issue または pull request の 5 番へのリンクになります。

クロスリンクを作りたいときは、`#` 記号を入力した直後に Issue や pull request のタイトルを打ち始めてください。GitHub が正しいリンク先の候補を提案します。さらに詳しくは [Autolinked References and URLs](https://docs.github.com/en/articles/autolinked-references-and-urls) を参照してください。

### ⌨️ やること：クロスリンクされた Issue を見つけてクローズする

1. Issue #1（Welcome）を開きます。
2. コメントに `Duplicate of #2` と入力し、Issue #1 をクローズします。
3. 20 秒ほど待ってから、手順を読んでいるページ（README）を再読み込みします。[GitHub Actions](https://docs.github.com/en/actions) が自動で次の Step に更新します。

---

## Step 2: 履歴からコミットを見つける（Find a commit in history）

重複の指摘をありがとうございます 👋

バージョン管理の重要な点のひとつは、過去をさかのぼって見られることです。`git blame` を使ってコミットの背景をたどると、コードについて人を _blame_（責める）する以上のことができます。なぜコミットが行われたのかという経緯が見えます。関連する pull request はどれか。誰が pull request を承認したか。マージ前にどんなテストが実行されたか。

履歴を調べる分かりやすい理由は、履歴を知るためです。Issue と pull request があれば、最低限の情報だけでなく、より完全な経緯が分かります。

### `git blame` とは（What's `git blame`?）

`git blame` は、ファイルの各行を最後に変更したリビジョンと作者を表示する Git の機能です。誰がいつコミットしたか、さらになぜコミットしたかまで調べられます。ファイルへの変更を誰が入れたのか分からないときは、`git blame` で確認できます。`git blame` という名前は責任追及のように聞こえますが、判断の背景を理解するために使えます。

### SHA（Secure Hash Algorithm）とは（What's a Secure Hash Algorithm (SHA)?）

SHA は特定のオブジェクトへの参照です。演習ではコミットへの参照を指します。GitHub では、特定のコミットを開くと、どんな変更が入ったか、誰が入れたか、pull request の一部だったかを確認できます。

### ⌨️ やること：履歴からコミットを見つける

1. 自分のリポジトリの Code タブを開きます。
   - _ヒント: リポジトリは別のタブで開いているかもしれません_
2. `docs` をクリックして `/docs` ディレクトリに入ります。
3. `_sidebar.md` をクリックしてファイルを表示します。
4. ファイルの上部にある **Blame** をクリックし、直近のリビジョンの詳細を見ます。
5. コミットメッセージ `add sidebar to documentation` をクリックして、コミットの詳細を表示します。
6. SHA の先頭 7 文字をコピーします（`commit` の後ろに並ぶ 40 文字の 16 進数の、最初の 7 文字です）。
7. 手順 6 の SHA をコメント本文にして Issue #2 にコメントし、"Comment" ボタンをクリックします。
8. 20 秒ほど待ってから、手順を読んでいるページ（README）を再読み込みします。[GitHub Actions](https://docs.github.com/en/actions) が自動で次の Step に更新します。

---

## Step 3: 壊れたサイドバーを直す（Fix a broken sidebar）

コミットを見つけられましたね ❤️

サイドバーが確かに追加されたこと、`add sidebar to documentation` のコミットで行われたことが分かりました。もう少し掘り下げて、変更をめぐる計画や会話がコメントとして残っていないか調べましょう。

すでに見たとおり、Issue や pull request での会話は別の作業を参照できますが、得られる文脈はクロスリンクだけにとどまりません。Git はバージョン管理です。たとえば、前の Step で見つけたコミットには、次のような情報がひも付いています。

- 誰がコミットをしたか。
- ほかにどんな変更が含まれていたか。
- いつコミットされたか。
- どの pull request の一部だったか。

pull request が重要なのは、コミットがいつ行われたかを超えた情報が分かるからです。_なぜ_ コミットが行われたかを知ることができます。履歴を調べるのは誰かを _責める_ ためではなく、全体像を見るためです。なぜ判断がされたのか。誰が関わったのか。各コミットのビルド結果とテスト結果はどうだったのか。誰が変更を要求し、誰が承認したのか。

### コミットから pull request を見つける（Finding a pull request from a commit）

GitHub でコミットを表示すると、多くの情報が見られます。コミットの画面から、コミットが作られた pull request へのリンクもたどれます。次の Step で使います。

![GitHub のコミット画面で、pull request へのリンクを示したスクリーンショット](https://user-images.githubusercontent.com/16547949/67341250-3edbb480-f4fd-11e9-805a-6bce5a8ba2d1.png)

### ⌨️ やること：壊れたサイドバーを直す

1. main ブランチで `docs/_sidebar.md` ファイルを編集します。
2. 4 行目にある参照 `(doc-references__.md)` のつづりを `(doc-references.md)` に直します。
3. コミット用に新しいブランチ `fix-sidebar` を選択または作成し、pull request を開始します。
4. **base:** に **main**、**compare:** に **fix-sidebar** が選ばれていることを確認します。
5. 右側の **Assignees** で、自分を pull request の担当者に割り当てます。
6. pull request のコメントに `Closes #2` と入力し、Issue #2 を自動リンクします。
7. **Create pull request** をクリックし、20 秒ほど待ちます。
8. pull request をマージします。
9. ブランチ `fix-sidebar` を削除します。
10. 20 秒ほど待ってから、手順を読んでいるページ（README）を再読み込みします。[GitHub Actions](https://docs.github.com/en/actions) が自動で次の Step に更新します。

---

## 完了（Finish）

おめでとうございます、コースを完了しました 🎉

<img src="https://octodex.github.com/images/collabocats.jpg" alt="celebrate" width="300" align="right">

今回のコースでは、情報を見つけて共有する方法を学びました。GitHub のリポジトリの中では、どんな変更が行われたかの履歴と、さらに重要な「なぜ変更が行われたか」を調べられます。

### 次にできること（What's next?）

GitHub Pages を有効にすると、`docs/index.html` を Web サイトとして表示できます。

1. `docs/index.html` の中の `USERNAME` を自分の GitHub ユーザー名に、`REPONAME` を自分のリポジトリ名に置き換えます。
2. リポジトリ名の下、右上にある ⚙️ **Settings** をクリックします。
3. 左下の **Pages** をクリックします。
4. **GitHub Pages** の欄で、**Select branch** のドロップダウンから `main` を、**Select folder** のドロップダウンから `/docs` を選びます。
5. **Save** ボタンをクリックします。
6. 30 秒ほど待ってからページを再読み込みします。"Your site is published at ..." と表示されたら、リンクから公開されたサイトを見られます。

さらに学ぶ・参加するための情報です。

- 学生の方は [Student Developer Pack](https://education.github.com/pack) を確認してください。
- コースの感想は [discussion board](https://github.com/orgs/skills/discussions/categories/connect-the-dots) で聞かせてください。
- [ほかの GitHub Skills コースを受ける](https://github.com/skills)。
- [GitHub Getting Started のドキュメントを読む](https://docs.github.com/en/get-started)。
- 貢献できるプロジェクトを探すには [GitHub Explore](https://github.com/explore) を見てください。

---

## 終わったら

- Microsoft Learn に戻り、モジュールの**知識チェック**（モジュール評価）を受けてください。
- 作成したリポジトリは削除しないでください。後のモジュールで振り返りに使います。
