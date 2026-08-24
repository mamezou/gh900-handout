# 演習 5 日本語訳：GitHub Copilot を使い始める（Getting Started with GitHub Copilot）

GitHub Skills「Getting Started with GitHub Copilot」の日本語版です。開始リンクは日本語化したテンプレート（`mamezou/skills-ja-getting-started-with-github-copilot`）を指しており、自分のリポジトリの **Issues** に Step 1 から順に**日本語で**表示されます。画面と同じ内容を、手元で読み返す用に載せています。

- 演習は **Codespace** の中で VS Code と GitHub Copilot を使います。題材は Mergington High School の課外活動申込サイト（Python / FastAPI）です。
- Copilot を初めて使う場合は、Step 1 でサインインと利用規約への同意を求められます（Copilot Free で構いません）。
- ボタン名、ファイル名、ブランチ名、コマンド、Copilot に入力するプロンプトは、画面と一致させるため英語のままにしています。**指定された名前は変えずに入力してください。** 自動チェックが名前を見ています。
- **Copilot の応答は毎回変わります。** 各所にある「結果の例」（Example Results）は参考例です。同じ結果にならなくても、目的を満たしていれば先に進んでかまいません。
- 各 Step を終えると、bot（Mona）が同じ Issue に次の Step をコメントします。出るまで 20〜30 秒待って、ページを再読み込みしてください。
- 時間の目安：60 分（Step 1〜5 をすべて授業内で行います）。

**演習の開始**: [自分用のリポジトリを作成する](https://github.com/new?template_owner=mamezou&template_name=skills-ja-getting-started-with-github-copilot&owner=%40me&name=skills-getting-started-with-github-copilot&description=GitHub+Skills:+Getting+Started+with+GitHub+Copilot&visibility=public)
→ **Create repository** を押し、20 秒待ってから再読み込み → **Issues** タブに Step 1 が出ます。

> **注意**: このページは手順の全体像です。実施するときは、まず上の開始リンクから自分のリポジトリを作り、
> リポジトリの **Issues** に届く手順に沿って進めてください。このページは読み返し用です。

---

## Step 1: Copilot を使ってみる（Hello Copilot）

「Getting Started with GitHub Copilot」演習へようこそ！ 🤖

演習では、GitHub Copilot のいろいろな機能を使って、Mergington High School の生徒が課外活動に申し込めるウェブサイトを作り込んでいきます。 🎻 ⚽️ ♟️

<img width="600" alt="Mergington High School のウェブアプリ" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/mergington-high-school-webapp.png" />

### 📖 理論：GitHub Copilot を知る

<img width="150" align="right" alt="copilot ロゴ" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/copilot-logo.png" />

GitHub Copilot は AI コーディングアシスタントです。コードを速く、少ない手間で書けるようにし、問題解決や共同作業により多くの力を使えるようにします。

GitHub Copilot は開発者の生産性を高め、ソフトウェア開発の速度を上げることが確かめられています。詳しくは GitHub ブログの [Research: quantifying GitHub Copilot's impact on developer productivity and happiness](https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/) を参照してください。

IDE で作業するとき、GitHub Copilot とは主に次の形でやり取りします。

| やり取りの方法 | 📝 説明 | 🎯 向いている場面 |
| --- | --- | --- |
| **⚡ Inline suggestions**（インライン候補） | 入力中に AI がコード候補を表示します。1 行から関数全体まで、文脈に合った補完を出します。 | 今書いている行の補完。ときにはコードのかたまり全体 |
| **💭 Inline Chat**（インラインチャット） | 今開いているファイルや選択範囲に絞ったチャット。特定のコードについて質問できます。 | コードの説明、特定の関数のデバッグ、狙いを定めた改善 |
| **💬 Ask Mode** | 自分のコードベース、コーディング、技術一般の概念についての質問に答えることに向いたモードです。 | コードの動きの理解、アイデア出し、質問 |
| **🤖 Agent Mode** | ほとんどのコーディング作業で推奨される既定のモード。自律的に編集し、ツールを使い、作業が終わるまで進めます。 | 日々のコーディング作業。範囲の狭い修正から、複数ファイルにまたがる実装まで |
| **🧭 Plan Agent** | コードを変更する前に、計画を書き出し、確認の質問をすることに向いたモードです。 | 先に計画をレビューしてから実装に渡したいとき |

作業していくと、GitHub Copilot は `github.com` のサイト上のいろいろな場所や、VS Code・JetBrains・Xcode といった普段の開発環境でも手助けしてくれることがわかります。

ただし今日のコーディングでは、[GitHub Codespace](https://github.com/features/codespaces) という設定済みの開発環境の中で VS Code を使って練習します。

> **ヒント**: 現在の機能と今後の機能については、[GitHub Copilot Features](https://docs.github.com/en/copilot/about-github-copilot/github-copilot-features) のドキュメントで学べます。

### ⌨️ やること：Copilot Chat にプロジェクトを紹介してもらう

まず開発環境を起動し、Copilot にプロジェクトのことを教えてもらい、実際に動かしてみましょう。

1. 下のボタンを使って、**Create Codespace** のページを新しいタブで開きます。設定は既定のままで構いません。

   [![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/<自分のアカウント>/skills-getting-started-with-github-copilot?quickstart=1)

2. **Repository** の欄が、元のリポジトリではなく自分のコピーになっていることを確認してから、緑色の **Create Codespace** ボタンをクリックします。
   - ✅ 自分のコピー: `<自分のアカウント>/skills-getting-started-with-github-copilot`
   - ❌ 元のリポジトリ: `/skills/getting-started-with-github-copilot`

3. ブラウザーの中で Visual Studio Code が読み込まれるまで少し待ちます。
4. 左のサイドバーで拡張機能タブをクリックし、`GitHub Copilot Chat` と `Python` の拡張機能がインストールされ、有効になっていることを確認します。

   <img width="350" alt="VS Code の Copilot 拡張機能" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/copilot-extension-vscode.png" />

   <img width="350" alt="VS Code の Python 拡張機能" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/python-extension-vscode.png" />

   <details>
   <summary>🔎 GitHub Copilot Chat 拡張機能が見当たらないとき ❓</summary>

   GitHub Copilot Chat の拡張機能が見当たらない場合は、GitHub Copilot にサインインしているか確認してください。VS Code ウィンドウの右下にある **GitHub Copilot** アイコンを探します。

   | ステータスバーのアイコン | サインインが必要 | Copilot が有効 |
   | --- | --- | --- |
   | <img width="300" alt="AI 機能の利用を促す Copilot メニュー" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/copilot-sign-in-button.png" /> | <img width="300" alt="Copilot Chat のサインインボタン" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/copilot-sign-in-button-clicked.png" /> | <img width="300" alt="インライン候補が有効になった Copilot メニュー" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/copilot-signed-in.png" /> |

   サインインが確認できていれば、拡張機能タブに表示されていなくても先に進めます。

   </details>

5. VS Code の上部にある **Toggle Chat** アイコンを見つけてクリックし、Copilot Chat のサイドパネルを開きます。

   <img width="150" alt="Toggle Chat アイコン" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/toggle-chat-icon.png" />

   > **注**: GitHub Copilot を初めて使う場合は、先に進むために利用規約への同意が必要になることがあります。

6. 最初のやり取りなので、**Ask Mode** になっていることを確認します。

   <img width="350" alt="Copilot Chat での Ask Mode の選択" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/ask-mode-selection.png" />

7. 次のプロンプトを入力して、Copilot にプロジェクトを紹介してもらいます。

   > ![Prompt](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > Please briefly explain the structure of this project.
   > What should I do to run it?
   > ```

   > **注**: Copilot が案内する手順に従う必要はありません。環境はすでに用意してあります。

8. プロジェクトのことが少しわかったので、実際に動かしてみましょう。左のサイドバーで `Run and Debug` タブを選び、**Start Debugging** アイコンを押します。

   <img width="300" alt="Run and Debug タブ" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/run-and-debug-tab.png" />

9. ブラウザーでウェブページを見たいので、URL とポートを探します。表示されていない場合は、下部のパネルを開いて **Ports** タブを選びます。

10. 一覧からポート `8000` と、対応するリンクを探します。リンクにマウスを重ね、**Open in browser** のアイコンを選びます。

    ![Open in browser アイコン](https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/open-in-browser-icon.png)

### ⌨️ やること：ターミナルのコマンドを Copilot に思い出させてもらう 🙋

よくできました！ アプリのことがわかり、動くことも確認できたので、次はカスタマイズ用のブランチを作るのを Copilot に手伝ってもらいましょう。

1. VS Code の下部パネルで **Terminal** タブを選び、右側のプラス `+` をクリックして新しいターミナルウィンドウを作ります。

   > **注**: 新しいターミナルを使うと、ウェブアプリを動かしている既存のデバッグセッションを止めずに済みます。

2. 新しいターミナルウィンドウの中で、キーボードショートカット `Ctrl + I`（Windows）または `Cmd + I`（Mac）を使い、**Copilot の Terminal Inline Chat** を開きます。

3. 忘れてしまったコマンド（ブランチを作って publish する方法）を Copilot に聞いてみましょう。

   > ![Prompt](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > Hey copilot, how can I create and publish a new Git branch called "accelerate-with-copilot"?
   > ```

   > **ヒント**: 思ったとおりの答えが返ってこなくても、必要なことを続けて説明できます。Copilot は会話の履歴を覚えていて、次の応答に反映します。

4. `Run` ボタンを押すと、Copilot がターミナルのコマンドを入れて実行してくれます。コピーと貼り付けは不要です。

5. 少し待ってから、VS Code の下部ステータスバーの左側で現在のブランチを確認します。`accelerate-with-copilot` になっていれば、Step 1 は完了です。

6. ブランチが GitHub に push されたので、Mona が作業を確認しています。少し待って、Issue のコメントを見てください。進捗と次の Step が投稿されます。

<details>
<summary>うまくいかないとき 🤷</summary><br/>

反応がないときは、次の点を確認してください。

- ブランチ名が正確に `accelerate-with-copilot` になっているか（前後に余計な文字を付けない）。
- ブランチが実際に自分のリポジトリへ publish されているか。

</details>

---

## Step 2: Copilot で作業を進める（Getting work done with Copilot）

前の Step では、GitHub Copilot にプロジェクトの内容を教えてもらいました。説明を受けるだけでも大きな時間短縮ですが、次は実際の作業をしてみましょう。

🐛 **ウェブサイトにバグがあります** 🐛

申し込みの流れにおかしいところが見つかりました。生徒が同じ活動に **2 回以上**申し込めてしまいます。原因を突き止め、きれいな修正の形にするところまで、Copilot がどこまでやってくれるか見てみましょう。

始める前に、Copilot の仕組みを簡単に押さえます。 🧑‍🚀

### 📖 理論：Copilot の仕組み

ひとことで言うと、Copilot はとても専門性の高い同僚だと考えられます。うまく働いてもらうには、背景（コンテキスト）と、はっきりした指示（プロンプト）を渡す必要があります。さらに、人によって経験や得意なことが違うように、Copilot にも複数のモデルがあります。

- **どうやってコンテキストを渡す？**: 開発環境の中では、Copilot は近くのコードと開いているタブを自動的に見ています。チャットを使う場合は、ファイルを明示的に指定することもできます。

- **どのモデルを選ぶ？**: 演習ではあまり気にしなくて構いません。いろいろなモデルを試すのも楽しみのひとつです。モデル選びはまた別のレッスンで。 🤖

- **プロンプトはどう書く？**: はっきりと具体的に書くほど、Copilot はよい仕事をします。ただし従来の仕組みと違って、後から追加のプロンプトで指示を補うことができます。

> **ヒント**: Copilot の知識と能力を補う方法は他にもあります。[chat participants](https://docs.github.com/en/copilot/using-github-copilot/copilot-chat/github-copilot-chat-cheat-sheet?tool=vscode#chat-participants)、[chat variables](https://docs.github.com/en/copilot/using-github-copilot/copilot-chat/github-copilot-chat-cheat-sheet?tool=vscode#chat-variables)、[slash commands](https://docs.github.com/en/copilot/using-github-copilot/copilot-chat/github-copilot-chat-cheat-sheet?tool=vscode#slash-commands-1)、[MCP tools](https://code.visualstudio.com/docs/copilot/chat/mcp-servers) などです。

### ⌨️ やること：Copilot で申し込みのバグを直す 🐛

1. バグの原因がどこにありそうか、Copilot に聞いてみましょう。**Copilot Chat** パネルを **Ask mode** で開き、次を入力します。

   > ![Prompt](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > #codebase Students are able to register twice for an activity.
   > Where could this bug be coming from?
   > ```

2. 問題が `src/app.py` ファイルの `signup_for_activity` メソッドにあるとわかったので、Copilot のすすめに従って直しに行きます（半分手作業で行います）。まずコメントを書き、続きは Copilot に埋めてもらいます。

   1. `src/app.py` ファイルを開きます。

      > **ヒント**: Copilot がチャットの中で `src/app.py` に触れている場合は、チャットビューでファイル名を直接クリックして開けます。

   2. ファイルの下のほうにある `signup_for_activity` 関数を探します。

   3. 生徒を追加する処理を説明しているコメント行を探します。コメント行の上が、申し込み済みかどうかの確認を入れるのに自然な場所です。

   4. 次のコメントを入力して Enter を押し、次の行へ移ります。少し待つと、Copilot の候補が薄い文字（シャドーテキスト）で表示されます。 🎉

      コメント:

      ```python
      # Validate student is not already signed up
      ```

      <img width="700" alt="エディター上の Copilot のシャドーテキスト候補" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/shadow-text.gif" />

   5. `Tab` を押して Copilot の候補を受け入れ、シャドーテキストをコードに変えます。

   <details>
   <summary>結果の例</summary><br/>

   Copilot は日々成長していて、いつも同じ結果になるとは限りません。候補が気に入らない場合のために、演習を作ったときに得られた正しい候補の例を載せておきます。例を使って先に進んでも構いません。

   ```python
   @app.post("/activities/{activity_name}/signup")
   def signup_for_activity(activity_name: str, email: str):
      """Sign up a student for an activity"""
      # Validate activity exists
      if activity_name not in activities:
         raise HTTPException(status_code=404, detail="Activity not found")

      # Get the activity
      activity = activities[activity_name]

      # Validate student is not already signed up
      if email in activity["participants"]:
        raise HTTPException(status_code=400, detail="Student is already signed up")

      # Add student
      activity["participants"].append(email)
      return {"message": f"Signed up {email} for {activity_name}"}
   ```

   </details>

### ⌨️ やること：Copilot にサンプルデータを作ってもらう 📋

新しいプロジェクトの開発では、テスト用に本物らしい架空のデータがあると便利なことがよくあります。Copilot はサンプル作りがとても得意なので、課外活動のサンプルをもう少し追加してみましょう。あわせて、**Inline Chat** という別のやり取りの方法も使います。

**Inline Chat** と **Copilot Chat** パネルは似ていますが、扱う範囲が違います。Copilot Chat は複数ファイルにまたがる質問や、調べながらの質問に向いています。Inline Chat は、目の前の 1 行やかたまりについて的を絞って助けてほしいときのほうが速いです。

1. `src/app.py` ファイルの上のほう（23 行目あたり）にある `activities` 変数を探します。サンプルの課外活動が設定されています。

2. `activities` 辞書の全体を、上から下へマウスでドラッグして選択します。選択すると、次のプロンプトのためのコンテキストを Copilot に渡せます。

   <img width="700" alt="インラインチャットを開く前に選択した activities 辞書" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/activities-dict-highlighted.png" />

3. キーボードの `Ctrl + I`（Windows）または `Cmd + I`（Mac）で Copilot の Inline Chat を開きます。

   > **ヒント**: 選択した行のどこかを `右クリック` → `Open Inline Chat` でも Inline Chat を開けます。

4. 次のプロンプトを入力し、Enter を押すか右側の **Send** ボタンを押します。

   > ![Prompt](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > Add 2 more sports related activities, 2 more artistic
   > activities, and 2 more intellectual activities.
   > ```

5. 少し待つと、Copilot がコードを直接書き換え始めます。追加と削除がひと目でわかるように、変更部分は違う見た目で表示されます。変更を確かめてから、**Keep** ボタンを押します。

   <details>
   <summary>結果の例</summary><br/>

   Copilot は日々成長していて、いつも同じ結果になるとは限りません。候補が気に入らない場合のために、演習を作ったときに得られた結果の例を載せておきます。うまくいかないときは、例を使って先に進んでも構いません。

   ```python
   # In-memory activity database
   activities = {
      "Chess Club": {
         "description": "Learn strategies and compete in chess tournaments",
         "schedule": "Fridays, 3:30 PM - 5:00 PM",
         "max_participants": 12,
         "participants": ["michael@mergington.edu", "daniel@mergington.edu"]
      },
      "Programming Class": {
         "description": "Learn programming fundamentals and build software projects",
         "schedule": "Tuesdays and Thursdays, 3:30 PM - 4:30 PM",
         "max_participants": 20,
         "participants": ["emma@mergington.edu", "sophia@mergington.edu"]
      },
      "Gym Class": {
         "description": "Physical education and sports activities",
         "schedule": "Mondays, Wednesdays, Fridays, 2:00 PM - 3:00 PM",
         "max_participants": 30,
         "participants": ["john@mergington.edu", "olivia@mergington.edu"]
      },
      "Basketball Team": {
         "description": "Competitive basketball training and games",
         "schedule": "Tuesdays and Thursdays, 4:00 PM - 6:00 PM",
         "max_participants": 15,
         "participants": []
      },
      "Swimming Club": {
         "description": "Swimming training and water sports",
         "schedule": "Mondays and Wednesdays, 3:30 PM - 5:00 PM",
         "max_participants": 20,
         "participants": []
      },
      "Art Studio": {
         "description": "Express creativity through painting and drawing",
         "schedule": "Wednesdays, 3:30 PM - 5:00 PM",
         "max_participants": 15,
         "participants": []
      },
      "Drama Club": {
         "description": "Theater arts and performance training",
         "schedule": "Tuesdays, 4:00 PM - 6:00 PM",
         "max_participants": 25,
         "participants": []
      },
      "Debate Team": {
         "description": "Learn public speaking and argumentation skills",
         "schedule": "Thursdays, 3:30 PM - 5:00 PM",
         "max_participants": 16,
         "participants": []
      },
      "Science Club": {
         "description": "Hands-on experiments and scientific exploration",
         "schedule": "Fridays, 3:30 PM - 5:00 PM",
         "max_participants": 20,
         "participants": []
      }
   }
   ```

   </details>

6. ウェブサイトを開いて、新しい活動が表示されていることを確認できます。

### ⌨️ やること：作業内容の説明を Copilot に書いてもらう 💬

バグを直し、サンプルの活動を増やせました。次は、作業をコミットして GitHub に push します。今回も Copilot に手伝ってもらいましょう。

1. 左のサイドバーで `Source Control` タブを選びます。

   > **ヒント**: ソース管理の場所からファイルを開くと、単に開くのではなく元との差分が表示されます。

2. `app.py` ファイルを探し、`+` を押して変更をステージング領域にまとめます。

   ![変更をステージするアイコン](https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/staging-changes-icon.png)

3. ステージした変更の一覧の上にある **Message** の入力欄を見つけます。ただし、今は**何も入力しないでください**。
   - ふだんは入力欄に変更内容の短い説明を書きますが、今回は Copilot に手伝ってもらいます。

4. **Message** 入力欄の右にある **Generate Commit Message** ボタン（きらきらのアイコン）を見つけてクリックします。

5. **Commit** ボタンと **Sync Changes** ボタンを押して、変更を GitHub に push します。

6. Mona が確認しています。Issue のコメントを待ってください。フィードバックと次のレッスンが投稿されます。

<details>
<summary>うまくいかないとき 🤷</summary><br/>

反応がないときは、次の点を確認してください。

- `src/app.py` の変更を、`accelerate-with-copilot` ブランチに push したか。

</details>

---

## Step 3: Copilot Agent Mode を使う（Engage Hyperdrive - Copilot Agent Mode）🚀

### 📖 理論：Copilot Agent Mode とは

Copilot の [agent mode](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode) は、AI 支援コーディングの次の段階です。自律的な相棒プログラマーとして、指示に応じて複数の手順にわたるコーディング作業を行います。

Copilot Agent Mode は、コンパイルエラーや lint エラーに反応し、ターミナルやテストの出力を見ながら、作業が終わるまで自動で修正を繰り返します。

#### Agent Mode の要点

| 観点 | 👩‍🚀 Agent Mode |
| --- | --- |
| 自律性と計画 | ざっくりした依頼を複数の手順に分解し、作業が終わるまで繰り返します。 |
| コンテキストの収集 | 今のコンテキストを使い、必要なら関連するファイルを自分で見つけられます。 |
| ツールの利用 | 使うツールを自動で選んで呼び出します。`#codebase` のような書き方でツールを指定することもできます。 |
| 承認と安全のための確認 | 影響の大きい操作は、実行前に承認を求める設定にできます。主導権を保てます。 |

#### 🧰 Agent Mode のツール

Agent Mode は、依頼を処理する中で専門的な作業を行うためにツールを使います。たとえば次のような作業です。

- プロンプトを実行するのに必要なファイルを探す
- ウェブページの内容を取得する
- テストやターミナルのコマンドを実行する

> **ヒント**: VS Code には多くの組み込みツールがありますが、**MCP tools** を通じて Agent Mode に分野固有の能力を追加することもできます。
>
> 詳しくは [MCP servers](https://code.visualstudio.com/docs/copilot/customization/mcp-servers) と [GitHub MCP Server](https://github.com/github/github-mcp-server) を参照してください。

では **Agent Mode** を試してみましょう。 👩‍🚀

### ⌨️ やること：Copilot で新しい機能を追加する 🚀

ウェブサイトは活動を一覧表示していますが、参加者は伏せられたままです。 🤫

Copilot を使って、各活動の下に申し込み済みの生徒を表示するように変えてみましょう。

1. Copilot Chat ウィンドウの下部にあるドロップダウンで、**Agent** モードに切り替えます。

   <img width="350" alt="Agent モードのドロップダウン" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/agent-mode-dropdown.png" />

2. ウェブページに関係するファイルを開き、各エディターウィンドウ（またはファイル）をチャットパネルへドラッグして、コンテキストとして使うよう Copilot に伝えます。

   - `src/static/app.js`
   - `src/static/index.html`
   - `src/static/styles.css`

   > **注**: ファイルをコンテキストに追加するのは任意です。追加しなくても、Copilot Agent Mode は `#codebase` などのツールを使って、プロンプトから関連ファイルを探せます。ファイルを指定すると Copilot を正しい方向へ導きやすくなり、特に大きなコードベースで役立ちます。

   <img width="400" alt="コンテキストに追加されたファイル" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/files-added-to-context.png" />

   > **ヒント**: **Add Context...** ボタンを使うと、GitHub の issue やターミナルウィンドウの結果など、他の情報もコンテキストとして渡せます。

3. 活動の現在の参加者を表示するようにプロジェクトを更新してほしい、と Copilot に頼みます。編集の提案が届いて適用されるまで少し待ちます。

   > ![Prompt](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > Hey Copilot, can you please edit the activity cards to add a participants section.
   > It will show what participants that are already signed up for that activity as a bulleted list.
   > Remember to make it pretty!
   > ```

   Copilot が作業を終えたあと、どの変更を残すかは自分で決めます。

   下の **Keep** ボタンを使って、すべての変更をまとめて受け入れる／破棄する、または 1 件ずつ確認して決める、のどちらもできます。チャットパネルからでも、編集された各ファイルを見ながらでも操作できます。

   <img width="900" alt="変更を残すか破棄するかのボタン" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/review-changes-buttons.png" />

4. すぐに変更を受け入れる前に、もう一度ウェブサイトを見て、想定どおりに更新されているか確認してください。

   更新後の活動カードの例を示します。アプリの再起動やページの再読み込みが必要なことがあります。

   <img width="350" alt="参加者情報が入った活動カード" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/activity-card-with-participants.png" />

   > **注**: 活動カードの見た目は違うかもしれません。Copilot はいつも同じ結果を出すとは限りません。

   <details>
   <summary>うまくいかないとき 🤷</summary><br/>

   ウェブサイトが読み込まれないときは、次の点を確認してください。

   - VS Code のデバッガーを再起動し、最新版のサイトが配信されているようにする。
   - URL を忘れた、ウィンドウを閉じてしまった場合は、Step 1 を見直す。
   - ページをハード再読み込みするか、プライベートウィンドウで開いて、新しいコピーを取得してみる。

   </details>

5. 変更が問題ないと確認できたら、パネルで提案された編集を 1 つずつ確認し、**Keep** を押して適用します。

   > **ヒント**: 提案された変更を受け入れる、手で直す、チャットで追加の指示を出して調整する、のいずれもできます。

### ⌨️ やること：Agent モードで「登録解除」ボタンを動くように追加する

もう少し自由度の高い依頼を試して、ウェブアプリに機能を足してみましょう。

思ったとおりの結果にならない場合は、別のモデルを試したり、追加のフィードバックを出して結果を調整したりできます。

1. Copilot が **Agent** モードのままであることを確認します。

   <img width="250" alt="Agent モード" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/agent-mode-dropdown.png" />

2. **Tools** アイコンをクリックして、いま Copilot Agent Mode が使えるツールを一通り見てみます。

   <img width="250" alt="Tools アイコン" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/tools-icon.png" />

3. 試してみましょう。参加者を削除する機能を追加するよう Copilot に頼みます。

   > ![Prompt](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > #codebase Please add a delete icon next to each participant and hide the bullet points.
   > When clicked, it will unregister that participant from the activity.
   > ```

   `#codebase` ツールは、いまの作業に関係するファイルやコードのかたまりを Copilot が探すために使います。

   > **注**: 演習では、結果をなるべく同じにするために `#codebase` ツールを明示的に指定しています。
   > `#codebase` を**付けずに**同じプロンプトを試して、Agent Mode が自分でプロジェクト全体のコンテキストを集めるかどうかを見てみるのもよいでしょう。

4. Copilot が終わったら、コードの変更とウェブサイト上の結果を確認します。結果が気に入ったら **Keep** ボタンを押します。気に入らなければ、Copilot にフィードバックを返して調整してみてください。

   > **注**: ウェブサイトに変更が反映されない場合は、デバッガーの再起動が必要なことがあります。

5. 申し込みのバグを直すよう Copilot に頼みます。

   > **ヒント**: 申し込みの流れを自分でも試しておくと、前後の動きの違いがはっきりわかります。

   > ![Prompt](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > I've noticed there seems to be a bug.
   > When a participant is registered, the page must be refreshed to see the change on the activity.
   > ```

6. Copilot が終わったら、結果を確認し、ウェブサイト上で申し込みの流れを検証します。

   結果が気に入ったら **Keep** ボタンを押します。気に入らなければ、Copilot にフィードバックを返してみてください。

7. すべての変更を `accelerate-with-copilot` ブランチに **Commit** して **push** します。

8. Mona が確認しています。Issue のコメントを待ってください。次の Step が投稿されます。

---

## Step 4: Planning Agent で実装を計画する（Plan your implementation with the Planning Agent）🧭

前の Step では、Agent Mode のおかげで速く動き、新しい機能を出せました。 🚀

今度は 1 回だけ速度を落として、設計者のように進めます。まずしっかりしたテスト方針を決めてから、実装に渡します。計画を先に立てると見通しがよくなり、想定外が減り、結果もきれいになります。 🧪

### 📖 理論：Copilot Plan Agent とは

Copilot の [Plan Agent](https://code.visualstudio.com/docs/copilot/agents/planning) は、コードを変更する前に解決策を設計する手助けをします。

いきなり編集を始めるのではなく、依頼内容を調べ、確認の質問をし、練り直せる実装計画を書き出します。

#### Plan Agent の要点

| 観点 | 🧭 Plan Agent |
| --- | --- |
| 目的 | コーディングを始める前に、構造化された実装計画を作ります。 |
| コンテキストの収集 | 読み取り専用の調査で、要件と制約を理解します。 |
| 進め方 | 確認の質問をし、答えを使って計画を更新します。 |
| 繰り返し | 実装前に何度でも計画を練り直せます。 |
| 安全性 | 計画を承認して **Agent Mode** に引き渡すまで、ファイルを編集しません。 |
| 引き渡し | **Start implementation** ボタンで、承認した計画を **Agent Mode** に渡してコーディングを始めます。 |

> **ヒント**: 大まかな依頼から始めて、後続のプロンプトで制約や詳細を足していけます。

### ⌨️ やること：バックエンドのテストを計画して実装する

バックエンドにはまだテストがまったくありません。**Plan Agent** で計画を作り、質問に答えて、実装を開始しましょう。

1. **Copilot Chat** パネルを開き、**Plan Agent** に切り替えます。

   <img width="350" alt="Plan モードのドロップダウン" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/plan-mode-dropdown.png" />

2. まずは大まかなプロンプトから始めます。細かいところは Copilot が埋めるのを手伝ってくれます。

   > ![Prompt](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > Let's plan for adding backend FastAPI tests in a separate tests directory.
   > ```

3. Copilot が最初の計画を作るまで待ちます。質問されたら、できる範囲で答えてください。

   > **注**: 完璧を目指さなくて構いません。計画は後から練り直せます。

4. 後続のプロンプトで、計画を練り直したり詳細を足したりできます。

   例を示します。

   > ![Prompt](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > Let's use the AAA (Arrange-Act-Assert) testing pattern to structure our tests
   > ```

   > ![Prompt](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > Make sure we use `pytest` and add it to `requirements.txt` file
   > ```

5. 提案された計画を確認し、納得できたら **Start implementation** をクリックして **Agent Mode** に引き渡します。

   <img width="350" alt="Start implementation ボタン" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/plan-mode-start-implementation.png" />

   ボタンを押すと **Plan** から **Agent Mode** に切り替わったことに注目してください。切り替わったあとは、前の Step と同じように Copilot がコードベースを編集できます。

6. 作った計画を Copilot が実装していく様子を見ます。ツールの実行（コマンドの実行や仮想環境の作成など）の許可を求められることがあります。作業を続けられるよう承認してください。

7. 変更を確認し、テストが正常に実行されることを確かめます。必要なら、実装が終わるまで指示を続けてください。

   **🎯 目標: 先へ進む前に、すべてのテストを通す（緑にする）こと。 ✅**

   > **注**: Agent Mode は 1 回で終えることもあれば、追加のプロンプトが必要なこともあります。

8. すべての変更を `accelerate-with-copilot` ブランチに **Commit** して **push** します。

9. Mona が確認しています。Issue のコメントを待ってください。次の Step が投稿されます。

<details>
<summary>うまくいかないとき 🤷</summary><br/>

- テストが実行されなかった場合は、実行するよう Copilot に頼んでください。
- `requirements.txt` に `pytest` が追加され、`tests/` ディレクトリがあることを確認してください。

</details>

---

## Step 5: pull request で GitHub Copilot を使う（Using GitHub Copilot within a pull request）

おめでとうございます！ 演習のコーディング（と VS Code での作業）は終わりです。残りは作業のマージです。 🎉 締めくくりに、pull request を速く進められる、利用が限られた 2 つの Copilot 機能を学びましょう。

### 📖 理論：pull request のための GitHub Copilot

#### Copilot pull request summaries

ふだんは、自分のメモやコミットメッセージを見返して、pull request の説明としてまとめます。コミットメッセージがそろっていなかったり、コードに説明が足りなかったりすると、まとめるのに時間がかかります。Copilot は pull request のすべての変更を見て、重要なところを参照付きで示してくれます。

#### Copilot code review

自分の作業は多くの目で見てもらうほどよいので、通常のピアレビューの前に、Copilot に一度見てもらいましょう。Copilot は、簡単な調整で直せるよくある間違いを見つけるのが得意です。ただし、責任を持って使うことを忘れないでください。

> **注**: 2 つの機能は **GitHub Copilot** の有料プランでのみ使えます。[[docs]](https://docs.github.com/en/copilot/get-started/plans)

### ⌨️ やること：Copilot で PR を要約してレビューする

**Copilot pull request summaries** と **Copilot code review** はどちらも利用が限られているため、以下の手順のほとんどは任意です。利用できない場合は、任意と書かれた手順を飛ばしてください。

1. ブラウザーで別のタブを開き、自分の演習リポジトリを開きます。

2. 新しい pull request の作成をすすめる**通知バナー**が出ているかもしれません。バナーをクリックするか、上部の **Pull Requests** タブから **pull request を新規作成**します。次の内容を使ってください。

   - **base:** `main`
   - **compare:** `accelerate-with-copilot`
   - **title:** `Improve student activity registration system`

3. （任意）PR の説明欄のツールバーで **Copilot** アイコンをクリックし、**Summary** を選びます。少し待つと、変更内容にもとづいた説明が Copilot によって追加されます。 📝

   <img alt="Copilot の Summary ボタン" width="450px" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/copilot-summarize-button.png">

4. （任意）右側の情報パネルの上部にある **Reviewers** の欄で、**Copilot アイコン**の横の **Request** ボタンをクリックします。少し待つと、Copilot が pull request にレビューコメントを追加します。

   <img alt="Copilot のレビュー依頼ボタン" width="300px" src="https://raw.githubusercontent.com/skills/getting-started-with-github-copilot/main/.github/images/copilot-review-button.png">

   > **ヒント**: Copilot にレビューを依頼した記録がログに残ることに注目してください。

5. 一番下の **Merge pull request** ボタンを押します。よくできました！ 完了です。 🎉

6. Mona が確認しています。Issue のコメントを待ってください。フィードバックと、演習の最終レビューが投稿されます。

---

## 終わったら

- Microsoft Learn に戻り、モジュールの**知識チェック**（モジュール評価）を受けてください。
- Codespace は**停止**してください。ただし**削除はしないでください**。
- 演習リポジトリは削除しないでください。
