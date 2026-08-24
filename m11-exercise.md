# 演習 11 日本語訳：リポジトリのサプライチェーンを保護する（Secure your repository supply chain）

GitHub Skills「Secure your Repository Supply Chain」の日本語版です。開始リンクは日本語化したテンプレート（`mamezou/skills-ja-secure-repository-supply-chain`）を指しており、自分のリポジトリの **Issues** に Step 1 から順に**日本語で**表示されます。画面と同じ内容を、手元で読み返す用に載せています。

- ボタン名、タブ名、設定項目名、ファイル名は、画面と一致させるため英語のままにしています。**指定された名前は変えずに入力してください。** 自動チェックは名前を見ています。
- 各 Step を終えると、bot（Mona）が進捗と次の Step をコメントします。出るまで少し待って、ページを再読み込みしてください。
- 時間の目安：20 分（Step 1〜4）。ブラウザーだけで完結します。Dependabot の処理を待つ場面があります。

**演習の開始**: [自分用のリポジトリを作成する](https://github.com/new?template_owner=mamezou&template_name=skills-ja-secure-repository-supply-chain&owner=%40me&name=skills-secure-repository-supply-chain&description=Exercise:+Secure+your+Repository+Supply+Chain&visibility=public)
→ **Create repository** を押し、20 秒待ってから再読み込み → Step 1 が出ます。

> **注意**: このページは手順の全体像です。実施するときは、まず上の開始リンクから自分のリポジトリを作り、
> リポジトリの **Issues** に届く手順に沿って進めてください。このページは読み返し用です。

---

## Step 1: dependency graph で依存関係を確認して追加する（Review and add dependencies using dependency graph）

**リポジトリのサプライチェーンを保護することが、なぜ重要なのか**: オープンソースの利用が加速し、ほとんどのプロジェクトが数百のオープンソース依存関係に頼っています。問題はセキュリティです。使っている依存関係に脆弱性があったらどうなるでしょうか。利用者をサプライチェーン攻撃の危険にさらすことになります。サプライチェーンを守るために最も大切なことの 1 つが、脆弱な依存関係にパッチを当て、マルウェアを置き換えることです。

GitHub には、環境内の依存関係を把握し、脆弱性を知り、パッチを当てるための機能がそろっています。GitHub のサプライチェーン機能は次のとおりです。

- Dependency graph
- Dependency review
- Dependabot alerts
- Dependabot updates
  - Dependabot security updates
  - Dependabot version updates

**dependency graph とは**: リポジトリに保存されたマニフェストファイルとロックファイル、および dependency submission API（ベータ）で登録された依存関係をまとめたものです。リポジトリごとに次を表示します。

- Dependencies（依存先）: リポジトリが依存しているエコシステムとパッケージ
- Dependents（依存元）: リポジトリに依存しているリポジトリとパッケージ

### ⌨️ やること 1.1：dependency graph が有効か確認する（Verify that dependency graph is enabled）

**説明を開いたまま作業できるよう、ブラウザーで別のタブを開いて以下の操作を行うことをおすすめします。**

> **注**: dependency graph は、新しいパブリックリポジトリでは既定で有効です。

1. **Settings** タブを開きます。
2. **Advanced Security** をクリックします。
3. **Dependency Graph** が **Enabled** になっていることを確認します。

### ⌨️ やること 1.2：新しい依存関係を追加して dependency graph を見る（Add a new dependency and view your dependency graph）

1. **Code** タブを開き、`code/src/AttendeeSite` フォルダーを探します。
2. 次の内容を、`package-lock.json` の `dependencies` マップの最後の項目として `main` ブランチにコミットします（末尾から 3 番目の `}` の後ろ、最後の 2 つの括弧の前）。

    > 🪧 **注**: ファイルは github.com 上で直接編集してコミットできます。`.` キーを押して軽量エディターを開いて編集・コミットすることもできます。

    ```json
    ,
    "follow-redirects": {
      "version": "1.14.1",
      "resolved": "https://registry.npmjs.org/follow-redirects/-/follow-redirects-1.14.1.tgz",
      "integrity": "sha512-HWqDgT7ZEkqRzBvc2s64vSZ/hfOceEol3ac/7tKwzuvEyWx3/4UegXh5oBOIotkGsObyk3xznnSRVADBgWSQVg=="
    }
    ```

3. **Insights** タブを開きます。
4. サイドナビゲーションから **Dependency graph** を選びます。
5. **Dependencies** タブですべての依存関係を確認します。
6. `follow-redirects` を検索し、いま追加した依存関係を確認します。

   ![「follow-redirects」依存関係のスクリーンショット](https://user-images.githubusercontent.com/6351798/196288729-734e3319-c5d7-4f35-a19c-676c12f0e27d.png)

7. 依存関係を追加したので、Mona が作業を確認しています。少し待って、コメントを見てください。進捗と次の Step が投稿されます。

---

## Step 2: Dependabot alerts を有効にして確認する（Enable and view Dependabot alerts）

_よくできました！ 🎉 Dependency graph を使って依存関係を追加し、確認できました。_

リポジトリが使う依存関係の数を考えると、管理は自動化する必要があります。コードを安全に保つことは最優先なので、まずやるべきは、使っている依存関係が脆弱だったりマルウェアだったりしたときに通知を受け取る仕組みを作ることです。Dependabot alerts を有効にすれば実現できます。

**Dependabot alerts とは**

Dependabot alerts は、コードが安全でないパッケージに依存していることを知らせます。Dependabot alerts は [GitHub Advisory Database](https://github.com/advisories) を参照しています。データベースには既知のセキュリティ脆弱性とマルウェアの一覧が、**GitHub reviewed advisories** と **unreviewed advisories** の 2 種類に分けて収録されています。

セキュリティ脆弱性のあるパッケージにコードが依存していると、プロジェクトや利用者にさまざまな問題を引き起こす可能性があります。できるだけ早く安全なバージョンにアップグレードしてください。コードがマルウェアを使っている場合は、安全な代替パッケージに置き換える必要があります。

いま追加した `follow-redirects` 依存関係で試してみましょう。

### ⌨️ やること 2.1：GitHub Advisory Database でセキュリティアドバイザリを見る（View security advisories in the GitHub Advisory Database）

1. [GitHub Advisory Database](https://github.com/advisories) を開きます。
2. アドバイザリの検索ボックスに `follow-redirects` と入力または貼り付けます。
3. 見つかったアドバイザリのどれかをクリックして、詳しい情報を見ます。
4. アドバイザリの packages、impact、patches、workaround、references が表示されます。

`follow-redirects` にアドバイザリが長く並んでいることに気づいたでしょうか。怖く見えますが、実はよいことです。活発にメンテナンスされ、脆弱性を取り除くパッチが公開されているということだからです。Dependabot alerts を有効にしておけば、依存関係を更新すべきときにアラートを受け取り、すぐに対応できます。

では、リポジトリで Dependabot alerts を有効にしましょう。

### ⌨️ やること 2.2：Dependabot alerts を有効にする（Enable Dependabot alerts）

1. **Settings** タブを開きます。
2. **Advanced Security** の設定を表示します。
3. Dependabot alerts を **Enable** にします。
4. **Dependabot がアラートを確認するまで 60 秒ほど待ちます。**
5. **Security** タブを開きます。
6. サイドバーの「Vulnerability alerts」の下で **Dependabot** を選び、既定ブランチの Dependabot alerts の一覧を表示します。

Dependabot が、使っている依存関係の脆弱性を知らせてくれました。さらに Dependabot には、依存関係を安全なバージョンに更新する pull request を作らせて、脆弱性への対処を助けてもらうこともできます。

アラートの 1 つについて、Dependabot に pull request を作らせて動きを見てみましょう。

### ⌨️ やること 2.3：Dependabot alert から pull request を作る（Create a pull request based on a Dependabot alert）

1. Dependabot alerts の一覧で「Prototype Pollution in minimist」をクリックし、詳しい情報を表示します。
2. **Create Dependabot security update** ボタンをクリックして、依存関係を更新する pull request を作ります。作成には最大 2 分ほどかかることがあります。
3. pull request が作られると、アラートのページに **Review security update** ボタンが表示されます。
4. **Review security update** ボタンをクリックして pull request を表示します。
   - pull request と **Files changed** タブで更新内容を確認できます。
5. **Conversation** タブに戻り、pull request をマージします。
6. pull request をマージしたので、Mona が作業を確認しています。少し待って、コメントを見てください。進捗と次の Step が投稿されます。

---

## Step 3: Dependabot security updates を有効にして動かす（Enable and trigger Dependabot security updates）

_Dependabot alerts の有効化・確認・作成、よくできました ✨_

リポジトリで Dependabot alerts を有効にしたのは、コードのセキュリティを高める大きな一歩でした。とはいえ、アラートを自分で選び、pull request を作る操作も自分で行う必要がありました。依存関係の更新と管理を、もっと自動化できるとよいですね。Dependabot security updates を使えば自動化できます。

**Dependabot security updates とは**

機能を有効にすると、Dependabot が脆弱な依存関係を検出するだけでなく、Dependabot alerts を解決する pull request を自動で作成して修正します。

「Prototype Pollution in minimist」のアラートは手動で pull request を作って直しましたが、今後のアラートに向けて Dependabot security updates を有効にし、同じ流れを自動化しましょう。

### ⌨️ やること 3.1：Dependabot security updates を有効にして動かす（Enable and trigger Dependabot security updates）

1. **Settings** タブを開き、**Advanced Security** を選びます。
2. **Dependabot security updates** を有効にします。新しい pull request が現れるまで 30〜60 秒待つ必要があるかもしれません。
3. リポジトリの **Pull requests** タブを開き、Dependabot が見つけたものを確認します。
4. **axios** 依存関係にパッチを当てる新しい pull request を探します。
5. pull request を確認してマージします。
6. pull request をマージしたので、Mona が作業を確認しています。少し待って、コメントを見てください。進捗と次の Step が投稿されます。

---

## Step 4: Dependabot version updates を有効にして動かす（Enable and trigger Dependabot version updates）

_お見事です！_ 🥳

依存関係の脆弱性を Dependabot が知らせ、安全なバージョンに更新する pull request を作るところまで自動化できました。あとは pull request を確認してマージするだけで、依存関係のセキュリティ問題に遅れず対応できます。

> **注**: Dependabot が提案した pull request が複数あったことに気づきましたか。マージしたのは **axios** 依存関係の pull request 1 件ですが、他のものは **Pull requests** の一覧から消えています。axios 依存関係のアップグレードによって他の推移的依存関係にも変更が生じ、削除されたり別のバージョンに更新されたりしたためです。dependency graph に変化があるたびに、Dependabot は既存の pull request を自動で見直し、不要になったものを閉じます。まとめて全部マージせず、Dependabot に任せましょう。

<img width="955" alt="axios の PR がマージされ、他の 2 件が閉じられたことを示すスクリーンショット" src="https://raw.githubusercontent.com/skills/secure-repository-supply-chain/main/.github/images/axios-pr-merged-others-closed.png" />

security updates はアラートの解決を自動化してくれますが、単にバージョンを最新に保ちたい場合はどうでしょうか。Dependabot version updates を使えば、依存関係の新しいバージョンに対する pull request の生成も自動化できます。

**Dependabot version updates とは**: セキュリティアラートに加えて、Dependabot は依存関係の維持にかかる手間も減らせます。依存しているパッケージやアプリケーションの最新リリースに、リポジトリが自動で追随するようにできます。セキュリティアラートと同じように、Dependabot が古くなった依存関係を見つけ、マニフェストを最新バージョンに更新する pull request を作成します。

どう動くか見てみましょう。

### ⌨️ やること 4.1：Dependabot version updates を有効にして動かす（Enable and trigger Dependabot version updates）

1. **Settings** タブを開き、**Advanced Security** を選びます。
2. **Dependabot version updates** を探して **Configure** をクリックすると、内容があらかじめ入ったファイルエディターが開きます。ファイル名は `dependabot.yml` です。
3. `dependabot.yml` には、リポジトリ内の GitHub Actions（`github-actions` パッケージエコシステム）を更新する設定があらかじめ入っています。
4. `dependabot.yml` 設定ファイルを編集して、もう 1 つエントリを追加します。次のようになります。

   ```yaml
   version: 2
   updates:
     - package-ecosystem: "github-actions"
       directory: "/"
       schedule:
         interval: "monthly"
     - package-ecosystem: "nuget"
       directory: "/code/"
       schedule:
         interval: "weekly"
   ```

   > 💡 **ヒント**: ファイルは github.com 上で直接編集してコミットできますが、ピリオドキー `.` を押して、ブラウザー内で軽量な VS Code エディターを開くこともできます。

5. 変更を `main` ブランチに直接コミットします。
6. 設定ファイルを更新したので、Mona が作業を確認しています。少し待って、コメントを見てください。進捗と次の Step が投稿されます。

Dependabot version updates が次のように更新を確認するよう設定できました。

- GitHub Actions の更新を月に 1 回確認し、古いものがあれば更新する pull request を作成する。
- .NET パッケージの更新を週に 1 回確認し、古いものがあれば更新する pull request を作成する。既定では月曜日に実行されます。別の曜日に実行するには [schedule.day](https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file#scheduleday) を参照してください。

---

## 終わったら

- Microsoft Learn に戻り、モジュールの**知識チェック**（モジュール評価）を受けてください。
- 作成したリポジトリは削除しないでください。後のモジュールで振り返りに使います。
