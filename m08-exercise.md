# 演習 8 日本語訳：Markdown でコミュニケーションする（Communicate using Markdown）

GitHub Skills「Communicate using Markdown」の日本語版です。開始リンクは日本語化したテンプレート（`mamezou/skills-ja-communicate-using-markdown`）を指しており、自分のリポジトリの **Issues** に Step 1 から順に**日本語で**表示されます。画面と同じ内容を、手元で読み返す用に載せています。

- ボタン名、ファイル名、ブランチ名、入力する文字列は、画面と一致させるため英語のままにしています。**指定された名前は変えずに入力してください。** 自動チェックは名前を見ています。
- 各 Step を終えると、bot（Mona）が同じ Issue に次の Step をコメントします。出るまで 20〜30 秒待って、ページを再読み込みしてください。
- 時間の目安：25 分（Step 1〜5 すべて）。ブラウザーだけで完結します。

**演習の開始**: [自分用のリポジトリを作成する](https://github.com/new?template_owner=mamezou&template_name=skills-ja-communicate-using-markdown&owner=%40me&name=skills-communicate-using-markdown&description=Exercise%3A+Communicate+using+Markdown&visibility=public)
→ **Create repository** を押し、20 秒待ってから再読み込み → **Issues** タブに Step 1 が出ます。

> **注意**: このページは手順の全体像です。実施するときは、まず上の開始リンクから自分のリポジトリを作り、
> リポジトリの **Issues** に届く手順に沿って進めてください。このページは読み返し用です。

---

## Step 1: 見出しを追加する（Add headings）

**Markdown とは**: GitHub 上でのやり取りに使う[軽量な記法](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)です。見出し、リスト、**太字**、_斜体_、表など、さまざまな書式を付けられます。GitHub の次のような場所で使えます。

- [issue](https://docs.github.com/issues/tracking-your-work-with-issues/about-issues)、[pull request](https://docs.github.com/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)、[discussion](https://docs.github.com/discussions/collaborating-with-your-community-using-discussions/about-discussions) のコメント
- 拡張子が `.md` または `.markdown` のファイル
- [Gist](https://docs.github.com/github/writing-on-github/editing-and-sharing-content-with-gists/creating-gists) に書いたテキスト

**見出しとは**: セクションの先頭に置く、少し大きな文字のことです。大きさは 6 段階あります。

### 例

```md
# This is an `<h1>` heading, which is the largest

## This is an `<h2>` heading

###### This is an `<h6>` heading, which is the smallest
```

`#` が 1 個のときがいちばん大きく、6 個のときがいちばん小さくなります。

### ⌨️ やること：Markdown ファイルを作る

1. ブラウザーで新しいタブを開き、説明は元のタブで読み、操作は新しいタブで行います。

1. 上部のメニューで **Code** タブを開きます。

1. 次の名前で新しいブランチを作ります。

   ```md
   start-blog
   ```

1. ファイル一覧の上にある **Add file** ボタンをクリックし、**Create new file** を選びます。

1. ファイル名は次のとおりにします。

   ```md
   day-1.md
   ```

1. エディターの 1 行目に、レベル 1 の見出しでページのタイトルを書きます。

   ```md
   # Daily Learning
   ```

1. 各ブログ記事の名前として、レベル 2 の見出しを 2 つ追加します。

   ```md
   ## Morning Planning

   ## Review
   ```

1. エディターの上にある **Preview** の切り替えをクリックして、表示結果を確認します。

1. 右上の **Commit changes** ボタンをクリックし、`start-blog` ブランチに直接コミットします。

1. Mona が確認しています。Issue のコメントを待ってください。

<details>
<summary>うまくいかないとき 🤷</summary>

- 編集しているファイルとブランチが正しいか確認してください。
- 記法を見直してください。`#` と最初の単語の間には半角スペースが必要です。
</details>

---

## Step 2: リストを作る（Make a list）

Markdown では、よく使う 3 種類のリストが使えます。

- [順序なしリスト](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#lists) — 箇条書き
- [順序付きリスト](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#lists) — 番号付き
- [タスクリスト](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#task-lists) — チェックボックス

### 順序なしリスト

各項目を 1 行ずつ書き、行頭に `-`、`*`、`+` のいずれかを付けます。

```md
- Item 1
- Item 2
- Item 3
```

- Item 1
- Item 2
- Item 3

### 順序付きリスト

行頭の記号を数字に変えると順序付きリストになります。番号は Markdown 側で自動的に振られます。

```md
1. Step 1
1. Step 2
1. Step 3
```

1. Step 1
1. Step 2
1. Step 3

### タスクリスト

タスクリストは、順序なしリストにチェックボックスを付けたものです。未完了は空の角かっこ `[ ]`、完了済みは `[x]` と書きます。空の角かっこの中には半角スペースが必要です。

```md
- [x] This task is complete
- [ ] This task is not complete
```

- [x] This task is complete
- [ ] This task is not complete

> **ヒント**: issue や pull request でもタスクの記法を使って[進捗を伝える](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/about-tasklists)ことができます。

### ⌨️ やること：朝の計画にアイデアと目標を追加する

1. `start-blog` ブランチで、`day-1.md` ファイルを開いて編集します。

1. **Morning Planning** のレベル 2 見出しの下に、達成したい目標を管理するための次のタスクリストを追加します。

   ```md
   - [ ] Check out the [github blog](https://github.blog/) for topic ideas.
   - [ ] Learn about [GitHub Pages](https://skills.github.com/#first-day-on-github).
   - [ ] Convert my first blog post into an actual webpage.
   ```

1. **Preview** タブで Markdown の書式を確認します。

1. 右上の **Commit changes** ボタンをクリックし、`start-blog` ブランチに直接コミットします。

1. Mona が確認しています。Issue のコメントを待ってください。

<details>
<summary>うまくいかないとき 🤷</summary>

- 編集しているファイルとブランチが正しいか確認してください。
- 記法を見直してください。タスクリストの `[ ]` の中には半角スペースが必要です。
</details>

---

## Step 3: コード例を追加する（Add a code sample）

[コードブロック](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#quoting-code)と、言語に応じた[シンタックスハイライト](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks)を学びます。

> **ヒント**: 多くのプログラミング言語に対応しています。ほかの言語も試してみてください。

### 例：ターミナルコマンド

````md
```bash
git clone https://github.com/skills/communicate-using-markdown
```
````

```bash
git clone https://github.com/skills/communicate-using-markdown
```

### 例：JavaScript のコード

````md
```js
var myVar = "Hello, world!";
```
````

```js
var myVar = "Hello, world!";
```

### ⌨️ やること：コード例を追加する

1. `start-blog` ブランチで、`day-1.md` ファイルを開いて編集します。

1. **Review** のレベル 2 見出しの下に、GitHub Blog で知ったコードの記録として次の内容を追加します。

   ````md
   Convert an image or video from dark mode to light mode using [ffmpeg](https://www.ffmpeg.org)

   ```bash
   ffmpeg -i input.mp4 -vf "negate,hue=h=180,eq=contrast=1.2:saturation=1.1" output.mp4
   ```
   ````

1. **Preview** タブで Markdown の書式を確認します。

1. 右上の **Commit changes** ボタンをクリックし、`start-blog` ブランチに直接コミットします。

1. Mona が確認しています。Issue のコメントを待ってください。

<details>
<summary>うまくいかないとき 🤷</summary>

- 編集しているファイルとブランチが正しいか確認してください。
- 記法を見直してください。コードブロックはバッククォート 3 個 ` ``` ` です。アポストロフィ 3 個 `'''` ではありません。
</details>

---

## Step 4: 画像を追加する（Add an image）

[Markdown での画像](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#images)の入れ方を、相対 URL・絶対 URL・サイズ指定・簡単な配置指定とあわせて学びます。

### Markdown の記法

画像は、リポジトリ内のファイルへの相対 URL か、インターネット上のどこかを指す絶対 URL で表示できます。

角かっこの中に書く説明文は、画像を読み込めなかったときに表示されます。スクリーンリーダーを使う人には読み上げられます。

なお、Markdown の記法には画像サイズを変える方法がありません。

### 例

リポジトリ内の画像への相対 URL:

```md
![Mona the Octocat](myrepo/original.png)
```

インターネット上の画像への絶対 URL:

```md
![Mona the Octocat](https://octodex.github.com/images/original.png)
```

<img alt="Mona the Octocat" src="https://octodex.github.com/images/original.png" width="200">

### 簡単な HTML

画像を小さくしたい、テキストの横に並べたい、ということはよくあります。HTML の記法を使うと、もう少し自由に指定できます。

- `alt` は代替テキストを指定します。
- `src` は画像の URL を指定します。
- `width` と `height` はピクセル単位でサイズを指定します。
- `align` は配置（`left`、`right`）を指定します。

```md
<img alt="Mona the Octocat" src="https://octodex.github.com/images/original.png"
width="200" align="right">
```

### ⌨️ やること：飾りを追加する

今のブログ記事はかなり素っ気ないので、飾りを足します。

1. `start-blog` ブランチで、`day-1.md` ファイルを開いて編集します。

1. **Morning Planning** のレベル 1 見出しの下に画像を挿入します。

   ```md
   ![Cloudy morning](https://octodex.github.com/images/cloud.jpg)
   ```

1. **Preview** タブで Markdown の書式を確認します。

   - 画像が大きすぎることに気づくはずです。

1. 単純な Markdown 版を、サイズと配置を指定した HTML 版に置き換えます。見栄えがよくなります。

   ```md
   <img alt="Cloudy morning" src="https://octodex.github.com/images/cloud.jpg" width="100" align="right">
   ```

1. 右上の **Commit changes** ボタンをクリックし、`start-blog` ブランチに直接コミットします。

1. Mona が確認しています。Issue のコメントを待ってください。

<details>
<summary>うまくいかないとき 🤷</summary>

- 編集しているファイルとブランチが正しいか確認してください。
- 記法を見直してください。HTML の画像タグは `img` で始まり、`src` 属性を含んでいる必要があります。
</details>

---

## Step 5: 作業を仕上げる（Finish work）

最初のブログ記事ができたので、`main` ブランチにマージします。

### ⌨️ やること：ブログ記事をマージする

1. 上部のメニューで **Pull requests** タブを開きます。

1. ブランチに `main` と `compare:start-blog` を指定して、新しい pull request を作成します。

1. （任意）pull request にわかりやすいタイトルと説明を付けます。

1. 下にスクロールして **Merge** ボタンをクリックします。

1. **Merge pull request** をクリックします。

1. pull request がマージされると、Mona が最後のまとめを投稿します。お疲れさまでした！ 🎉

---

## 終わったら

- Microsoft Learn に戻り、モジュールの**知識チェック**（モジュール評価）を受けてください。
- 演習用のリポジトリは削除しないでください。後のモジュールで振り返りに使います。
