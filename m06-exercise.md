# 演習 6 日本語訳：Codespaces でコーディングする（Code with Codespaces）

GitHub Skills「Code with Codespaces」の日本語版です。開始リンクは日本語化したテンプレート（`mamezou/skills-ja-code-with-codespaces`）を指しており、自分のリポジトリの **Issues** に Step 1 から順に**日本語で**表示されます。画面と同じ内容を、手元で読み返す用に載せています。

- コマンド、ファイル名、コミットメッセージ、ボタン名、`devcontainer.json` の内容は、画面と一致させるため英語のままにしています。**指定された名前は変えずに入力してください。** 自動チェックは名前を見ています。
- 各 Step を終えると、bot（Mona）が同じ Issue に次の Step をコメントします。出るまで 20〜30 秒待って、ページを再読み込みしてください。
- 時間の目安：15 分。授業内の到達点は **Step 1** です。Step 2〜4 は時間があれば、または授業後に進めてください。

**演習の開始**: [自分用のリポジトリを作成する](https://github.com/new?template_owner=mamezou&template_name=skills-ja-code-with-codespaces&owner=%40me&name=skills-code-with-codespaces&description=Exercise:+Code+with+Codespaces&visibility=public)
→ **Create repository** を押し、20 秒待ってから再読み込み → **Issues** タブに Step 1 が出ます。

- VS Code の画面が日本語表示になっている場合、ボタン名は日本語で出ます（例: **Keep** →「保持」、**Commit** →「コミット」、**Source Control** →「ソース管理」）。手順は英語名で書いているので、対応する日本語のボタンを探してください。

> **注意**: このページは手順の全体像です。実施するときは、まず上の開始リンクから自分のリポジトリを作り、
> リポジトリの **Issues** に届く手順に沿って進めてください。このページは読み返し用です。

---

## Step 1: codespace を起動してコードを push する（Start a codespace and push some code）

### Codespaces の何がすごいのか

**codespace** は、クラウド上でホストされる開発環境です。リポジトリの中の設定ファイルで内容が決まります。プロジェクト専用の開発環境を何度でも同じ形で作れるので、新しい開発者の立ち上げが簡単になり、「自分のマシンでは動くのに」という有名なセリフを避けられます 😎

各 codespace は [Dev Container specification](https://containers.dev/implementors/spec/) に従い、GitHub が [Docker コンテナー](https://code.visualstudio.com/docs/devcontainers/containers)としてホストします。

でも心配は要りません。Docker の知識も、自分のマシンへの Docker のインストールも不要です。

> **ヒント**: Dev Container の設定はリポジトリの一部なので、自分の Docker ホストを使ってローカルで動かすこともできます。

codespace には、ローカル開発と比べて次のような利点があります。

- リポジトリのページから直接 codespace を起動できる。
- ブラウザーで開発できる。IDE のインストールは不要。
  - ローカルにインストールした VS Code からリモートの codespace につなぐこともできる。
- プロジェクトの実行に必要なものを、あらかじめ設定しておける。
  - **[features](https://containers.dev/features)** を追加して、よく使う開発ツールを入れる。
  - codespace のライフサイクルの各段階でスクリプトを実行する（例：python / npm のパッケージをインストールする）。
  - プロジェクトに合わせて VS Code の設定と拡張機能を用意する。
- 通信が速い（コンテナーがデータセンター内にあるため）。

> **ヒント**: codespace は、pull request のレビューのような短時間の用途でも役に立ちます。届いたコード変更を試すために、自分の環境が正しいかを確認する必要がありません。

始めましょう。codespace を起動し、アプリケーションを実行し、変更を加えて push します。普段の開発と同じ流れです 🤓

### ⌨️ やること：codespace を起動する

1. 2 つ目のタブを開き、自分のリポジトリを開きます。**Code** タブにいることを確認します。
2. ファイル一覧の右上にある緑色の **<> Code** ボタンをクリックします。

   <img width="300" alt="緑色の Code ボタン" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/green-code-button.png" />

3. **Codespaces** タブを選び、**Create codespace on main** ボタンをクリックします。新しいウィンドウが開いて VS Code が起動し、リモートの codespace に接続します。作成には数分かかるので待ちます。
4. VS Code ウィンドウの左下を見て、リモート接続を確認します。

   <img width="350" alt="VS Code のリモート接続状態" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/remote-connection-status.png"/>

> **ヒント**: リポジトリに設定が含まれていない場合、GitHub は [universal](https://github.com/devcontainers/images/tree/main/src/universal) の codespace イメージを使います。よく使われる便利なツールが一通り入っています。

### ⌨️ やること：アプリケーションを実行する

1. VS Code の codespace にいることを確認します。
2. 左のサイドバーで **Explorer** タブを選び、`src/hello.py` を開きます。

   <img width="250" alt="VS Code の Explorer タブ" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/vs-code-explorer-tab.png" />

3. 下部パネルで **TERMINAL** タブを選びます。

   <img width="350" alt="VS Code の TERMINAL タブ" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/vs-code-terminal-tab.png" />

4. codespace のリモートターミナルに次のコマンドを貼り付けて、入っているツールのバージョンを表示します。後で比較するのでバージョンを控えておきます。

   ```bash
   node --version
   dotnet --version
   python --version
   gh --version
   ```

5. 次のコマンドを貼り付けて、codespace のリモートターミナルで Python プログラムを実行します。

   ```bash
   python src/hello.py
   ```

### ⌨️ やること：codespace からリポジトリに変更を push する

1. `src/hello.py` の中身を次の内容に置き換えて、ファイルを保存します。

   ```py
   print("Hello World!")
   ```

2. メッセージを直したら、変更をコミットして GitHub に push します。VS Code のソース管理の機能を使うか、次のターミナルコマンドを使います。

   ```bash
   git add 'src/hello.py'
   git commit -m 'fix: incomplete hello message'
   git push
   ```

3. （任意）ブラウザーに戻って `src/hello.py` を開き、変更が反映されているか確認します。
4. 変更が GitHub に push されると、Mona が確認しています。Issue のコメントを待ってください。進捗と次の Step が投稿されます。

<details>
<summary>うまくいかないとき 🤷</summary>

- codespace の作成には数分かかります。VS Code が接続するまで待ってください。
- `git push` でエラーが出る場合は、codespace のターミナルで実行しているか確認してください。
</details>

---

## Step 2: codespace でカスタムイメージを使う（Use a custom image in your codespace）

さきほど作った codespace には、リポジトリ側の設定がありませんでした。設定がないため、GitHub は既定の Docker イメージを使いました。既定のイメージは便利ですが、内容が一定にならず、実行環境のバージョンも固定されません。開発環境を何度でも同じ形で作るには、設定を指定することが重要です。

使う Docker コンテナーイメージを指定してみます。

### codespace はどう設定するのか

設定はリポジトリの中の `.devcontainer/devcontainer.json` で直接指定します。設定を複数持つこともできます。

`devcontainer.json` を作り、よく使う設定をいくつか入れてみましょう。VS Code の設定、ポート転送、ライフサイクルスクリプトの実行といった他の項目については、GitHub の [Codespaces ドキュメント](https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces)を参照してください。

### ⌨️ やること：codespace をカスタマイズする

1. VS Code の codespace にいることを確認します。
2. VS Code のファイルエクスプローラーで、設定ファイルを作ります。

   ```txt
   .devcontainer/devcontainer.json
   ```

   または、次のターミナルコマンドでも作れます。

   ```bash
   mkdir -p .devcontainer
   touch .devcontainer/devcontainer.json
   ```

3. `.devcontainer/devcontainer.json` を開き、次の内容を追加します。まずは基本的なイメージから始めます。

   ```json
   {
     "name": "Basic Dev Environment",
     "image": "mcr.microsoft.com/devcontainers/base:debian"
   }
   ```

   > 💡 **ヒント**: name は任意ですが、設定が複数あるとき、GitHub で codespace を作る際に見分けやすくなります。

4. 保存すると、VS Code に「設定の変更を検出しました」という通知が出ているはずです。**Accept** を選ぶと開発コンテナーが再ビルドされます。または、コマンドパレット（`CTRL`+`Shift`+`P`）から `Codespaces: Rebuild Container` を実行します。**Rebuild** を選びます。フルビルドは必要ありません。

   <img width="350" alt="rebuild codespace コマンド" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/rebuild-codespace-command.png"/>

5. codespace の再ビルドと VS Code の再接続に数分かかるので待ちます。
6. 下部パネルを開き、**TERMINAL** タブを選びます。
7. 次のコマンドでツールのバージョンをもう一度確認します。どれも入っていないことがわかります。

   ```bash
   node --version
   dotnet --version
   python --version
   gh --version
   ```

8. ⚠️ 現在、Codespaces には [Git-LFS](https://git-lfs.com/) がインストールされている前提になっている不具合があります。次のコマンドを実行して、影響を受ける Git フックを削除します。

   ```bash
   rm .git/hooks/post-checkout
   rm .git/hooks/post-commit
   rm .git/hooks/post-merge
   rm .git/hooks/pre-push
   ```

9. 新しい設定を確認できたので、変更をコミットします。VS Code のソース管理の機能を使うか、次のターミナルコマンドを使います。

   ```bash
   git add '.devcontainer/devcontainer.json'
   git commit -m 'feat: Add codespace configuration'
   git push
   ```

10. dev container の設定をコミットすると、Mona が確認しています。Issue のコメントを待ってください。

<details>
<summary>うまくいかないとき 🤷</summary>

- ファイルの場所が `.devcontainer/devcontainer.json` になっているか確認してください。
- JSON の書き方（かっこ、カンマ）が正しいか確認してください。
</details>

---

## Step 3: Features を追加する（Add Features）

コンテナーの feature、VS Code の拡張機能、VS Code の設定、ホストの要件など、さらに細かく codespace をカスタマイズできます。

GitHub CLI と、VS Code で Python プログラムを実行するための拡張機能、そして codespace の初回作成時にパッケージをインストールする独自スクリプトを追加します。

### ⌨️ やること：Python のサポートを追加する

1. VS Code でコマンドパレット（`CTRL`+`SHIFT`+`P`）を開き、次のコマンドを選びます。

   ```txt
   Codespaces: Add Dev Container Configuration Files...
   ```

   <img width="350" alt="VS Code の dev container 設定コマンド" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/configure-dev-container-command.png" />

2. `Modify your active configuration...` を選びます。
3. feature の一覧から `devcontainers` の `Python` を検索して選びます。

   - 既定値ではなく、`Configure Options` を選びます。
   - `Install Tools` は `true` のままにします。
   - Python のバージョンは `3.10` を選びます。

4. `.devcontainer/devcontainer.json` を開きます。
5. 次のような項目が追加されているか確認します。

   ```json
   "features": {
      "ghcr.io/devcontainers/features/python:1": {
         "installTools": true,
         "version": "3.10"
      }
   },
   ```

### ⌨️ やること：VS Code の拡張機能を追加する

1. 左のナビゲーションで **Extension** タブを選びます。

   <img width="200" alt="VS Code の拡張機能タブ" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/vs-code-extensions-tab.png" />

2. `python` を検索し、`Python` と `Python Debugger` を見つけます。

   <img width="250" alt="VS Code の Python 拡張機能" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/python-extensions.png" />

3. どちらも右クリックし、`Add to devcontainer.json` を選びます。

   <img width="250" alt="Add to devcontainer.json ボタン" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/add-to-devcontainer-button.png" />

4. `.devcontainer/devcontainer.json` を開きます。
5. 次のような項目が追加されているか確認します。

   ```json
   "customizations": {
      "vscode": {
         "extensions": [
            "ms-python.python",
            "ms-python.debugpy"
         ]
      }
   },
   ```

### ⌨️ やること：独自スクリプトを追加する

Dev Container specification には、codespace をさらにカスタマイズするための [ライフサイクルスクリプト](https://containers.dev/implementors/json_reference/#lifecycle-scripts) を実行できる場所が複数あります。初回ビルド（または再ビルド）の後に 1 回だけ実行される `postCreateCommand` を追加します。

1. VS Code のファイルエクスプローラーで、次の名前のスクリプトファイルを作ります。

   ```txt
   .devcontainer/postCreate.sh
   ```

   または、次のターミナルコマンドでも作れます。

   ```bash
   touch .devcontainer/postCreate.sh
   ```

2. 次のターミナルコマンドで、スクリプトを実行可能にします。

   ```bash
   chmod +x .devcontainer/postCreate.sh
   ```

3. `.devcontainer/postCreate.sh` を開き、次のコードを追加します。蒸気機関車のアニメーションをインストールする内容です。

   ```bash
   #!/bin/bash

   sudo apt-get update
   sudo apt-get install sl
   echo "export PATH=\$PATH:/usr/games" >> ~/.bashrc
   echo "export PATH=\$PATH:/usr/games" >> ~/.zshrc
   ```

4. `.devcontainer/devcontainer.json` を開きます。
5. `features` や `customizations` と同じ階層（トップレベル）に `postCreateCommand` の項目を作ります。

   ```json
   "postCreateCommand": ".devcontainer/postCreate.sh"
   ```

6. 新しい設定ができたので、変更をコミットします。VS Code のソース管理の機能を使うか、次のターミナルコマンドを使います。

   ```shell
   git add '.devcontainer/devcontainer.json'
   git add '.devcontainer/postCreate.sh'
   git commit -m 'feat: Add features, extensions, and postCreate script'
   git push
   ```

7. VS Code のコマンドパレット（`CTRL`+`Shift`+`P`）を開き、`Codespaces: Rebuild Container` を実行します。**Rebuild** を選びます。フルビルドは必要ありません。

   <img width="350" alt="rebuild codespace コマンド" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/rebuild-codespace-command.png"/>

8. codespace の再ビルドと VS Code の再接続に数分かかるので待ちます。
9. カスタマイズをコミットすると、Mona が確認しています。Issue のコメントを待ってください。

> **ヒント**: アカウントに [dotfiles をインストールする](https://docs.github.com/en/codespaces/setting-your-user-preferences/personalizing-github-codespaces-for-your-account)設定もできます。個人の設定とプロジェクトの設定を組み合わせられます。

### ⌨️ やること：（任意）カスタマイズを確認する

codespace を再ビルドしたので、Python の拡張機能、Python のバージョン、独自スクリプトが正しく反映されたか確認します。

1. codespace にいることを確認します。
2. 左のサイドバーで拡張機能タブをクリックし、Python の拡張機能がインストールされ、有効になっているか確認します。

   <img width="250" alt="VS Code の Python 拡張機能" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/python-extensions.png" />

3. 左のサイドバーで **Run and Debug** タブを選び、**Start Debugging** のアイコンを押します。VS Code が下部パネルを開き、実行ログを表示します。

   <img width="250" alt="Run and Debug タブの開始ボタン" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/run-and-debug-start-button.png"/>

4. 下部パネルで **TERMINAL** タブに切り替えます。
5. 次のコマンドを実行して、入っている Python のバージョンを表示します。他のツールは入っていないことがわかります。

   ```bash
   node --version
   dotnet --version
   python --version
   gh --version
   ```

6. 次のコマンドを実行して、蒸気機関車のアニメーションを表示します。

   ```bash
   sl
   ```

<details>
<summary>うまくいかないとき 🤷</summary>

- `sl` が見つからない場合は、再ビルドが終わっているか、ターミナルを開き直したか確認してください。
- `devcontainer.json` のトップレベルに `postCreateCommand` があるか確認してください。
</details>

---

## Step 4: 作った Codespace を試す（Test out our Codespace）

最後のテストとして、新しく参加した開発者の立場になってみます。いったんすべて閉じて、何もない状態から新しい codespace を起動します。

### ⌨️ やること：今ある codespace を削除する

1. VS Code の codespace を実行しているウィンドウを閉じます。
2. 演習用のリポジトリを開きます。
3. ファイル一覧の右上にある緑色の **<> Code** ボタンをクリックします。
4. **Codespaces** タブを選び、作成済みの codespace の一覧を表示します。

   <img width="250" alt="codespace の一覧" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/codespaces-list.png" />

5. 動いているものを見つけ、三点メニュー `...` から **Delete** を選びます。

   <img width="500" alt="codespace の削除コマンド" src="https://raw.githubusercontent.com/skills/code-with-codespaces/main/.github/images/delete-codespace-command.png" />

> **ヒント**: すべてのプロジェクトの codespace は https://github.com/codespaces でまとめて管理できます。

### ⌨️ やること：codespace を起動する

1. ファイル一覧の右上にある緑色の **<> Code** ボタンをクリックします。
2. **Codespaces** タブを選び、**プラス記号** `+` または **Create codespace on main** ボタンをクリックします。

   > 三点メニュー `...` を選ぶと、マシンの種類、リージョン、設定を変えることもできます。

3. codespace の作成と VS Code の接続に数分かかるので待ちます。
4. （任意）前の Step でやったことをいくつか試して、同じように動くか確かめます。
5. テストが終わったことを Mona に知らせるため、Issue にコメントを追加します。コメント後、最終レビューが投稿されるまで少し待ちます。

   ```md
   Hey @professortocat, I've finished testing out my new Codespace.
   I'm ready to review!
   ```

6. お疲れさまでした。完了です！ 🎉

<details>
<summary>うまくいかないとき 🤷</summary>

- コメントは Issue に投稿してください。`@professortocat` の記載を消さないでください。
</details>

---

## 終わったら

- Microsoft Learn に戻り、モジュールの**知識チェック**（モジュール評価）を受けてください。
- codespace は**停止**してください。削除するかどうかは、授業終了後に各自で判断してください。
- 演習用のリポジトリは削除しないでください。後のモジュールで振り返りに使います。
