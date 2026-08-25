# 演習 4 日本語版：CodeQL でコードスキャン（Introduction to CodeQL）

演習 4 は**任意実施**です。授業内は講師デモで進めます。手を動かしたい場合は、休憩時間または授業後に
自分のリポジトリで実施できます。

GitHub Skills「Introduction to CodeQL」の日本語版です。開始リンクは日本語化したテンプレート
（`mamezou/skills-ja-introduction-to-codeql`）を指しており、自分のリポジトリの **Issues** に
Step 1 から順に**日本語で**表示されます。Issue と同じ内容を、手元で読み返す用に載せています。

- ボタン名、タブ名、設定項目名、ファイル名、ブランチ名、入力する文字列は、画面と一致させるため英語のままにしています。
  **指定された名前や文字列は変えずに入力してください。** 自動チェックは入力内容を見ています。
- 各 Step を終えると、bot（Mona）が同じ Issue に進捗と次の Step をコメントします。表示されるまで少し待って、
  ページを再読み込みしてください。
- 時間の目安：30 分（スキャンの待ち時間を含む）。ブラウザーだけで実施できます。

**演習の開始**: [自分用のリポジトリを作成する](https://github.com/new?template_owner=mamezou&template_name=skills-ja-introduction-to-codeql&owner=%40me&name=skills-introduction-to-codeql&description=GitHub+Skills:+Introduction+to+CodeQL&visibility=public)

> **注意**: このページは手順の全体像です。実施するときは、まず上の開始リンクから自分のリポジトリを作り、
> リポジトリの **Issues** に届く手順に沿って進めてください。このページは読み返し用です。
→ **Create repository** を押し、20 秒待ってから再読み込み → **Issues** タブに Step 1 が出ます。

---

## Step 1: コードスキャンを有効にする

[CodeQL](https://codeql.github.com/) によるコードスキャンの概要と、コードの保護にどのように役立つかを学びます。

### GitHub のコードスキャンとは

[コードスキャン](https://docs.github.com/en/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/about-code-scanning)は、
[GitHub Advanced Security（GHAS）](https://docs.github.com/en/get-started/learning-about-github/about-github-advanced-security)製品群の一部です。
開発チームがコードをリリースする既存のプロセスに、セキュリティテストツールを直接組み込めます。
静的アプリケーションセキュリティテスト（SAST）、コンテナー、Infrastructure as Code など、多くの種類に対応しています。
分析結果はコードと並べて GitHub 上に表示できます。作業画面を切り替える必要はありません！ 🎉

> [!TIP]
> GitHub Advanced Security の全機能は、public リポジトリでは無料です。ただし、private リポジトリでは対応する
> [有料アカウント](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-advanced-security/about-billing-for-github-advanced-security)が必要です。

### CodeQL とは

[CodeQL](https://docs.github.com/en/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/about-code-scanning-with-codeql)は、
SQL インジェクション、クロスサイトスクリプティング、コードインジェクションなどのセキュリティ上の弱点を特定する静的解析テストツールです。

通常、CodeQL の[クエリ](https://codeql.github.com/docs/writing-codeql-queries/about-codeql-queries/)は、複数のパターンを検出できるように
[クエリスイート](https://docs.github.com/en/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/about-code-scanning-with-codeql#about-codeql-queries)にまとめられます。
クエリを適切に組み合わせると、強力な分析が可能です。セキュリティ専門家のチームが、一般的な利用場面とプログラミング言語に対応する
クエリスイートをあらかじめ用意しています。

多くの場合、既定のクエリスイートを選ぶだけで CodeQL を利用できます。拡張クエリスイートを選んだり、
[GitHub Actions]() を使って独自のクエリスイートを設定したりすることもできます。

<img width="250" align="right" alt="CodeQL の既定の設定画面" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/codeql-default-configuration-box.png"/>

既定の設定には、次の選択肢があります。

- **Languages:** 対応する言語をリポジトリから自動的に検出し、スキャンを有効にします。

- **Query suites:** 使用する検出パターンのスイート一覧です。**Default** または **Extended** が自動的に用意されます。

- **Runner type:** CodeQL 分析を実行する GitHub Actions ランナーの種類です。既定では標準の GitHub-hosted runner を使用しますが、
  [self-hosted runner](https://docs.github.com/en/enterprise-cloud@latest/code-security/how-tos/secure-at-scale/configure-enterprise-security/configure-specific-tools/configuring-code-scanning-for-your-appliance)を使用するように変更できます。

- **Events:** CodeQL スキャンを実行するトリガーです。本番コードでは、マージ前と定期スケジュールで実行するのが一般的です。

### ⌨️ やること: CodeQL でコードスキャンを有効にする

1. ブラウザーで別のタブを開き、演習用リポジトリを表示します。**Code** タブを開いていることを確認します。

1. 上部のナビゲーションで **Settings** タブを選びます。

1. 左側のナビゲーションのセキュリティ設定で **Advanced Security** を選びます。
   アカウントによっては **Code security** と表示されます。

1. 下へスクロールして **Code scanning** の領域を探します。

1. **CodeQL** の設定で **Set up** ドロップダウンメニューをクリックし、**Default** を選びます。

   <img width="400" alt="コードスキャンを有効にする画面" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/enable-code-scanning.png"/>

1. **Enable CodeQL** をクリックします。

   > 💡 ヒント: CodeQL の最初の実行が開始されます。進行状況は **Actions** タブで確認できます。

1. CodeQL を有効にしたので、Mona が作業を確認しています。少し待って、コメントを見てください。進捗と次の Step が投稿されます。

---

## Step 2: pull request で脆弱性を検出する

コードスキャンの動作を確認するため、`routes.py` ファイルに脆弱性を作り、アラートを発生させます。

### ⌨️ やること: 脆弱性を作る

1. 上部のナビゲーションで **Code** タブを選びます。

1. `server` フォルダーに移動し、`routes.py` ファイルを選びます。

1. プレビューの右上にある **Edit** ボタンをクリックします。

   <img width="500" alt="Edit ボタン" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/edit-button.png"/>

1. **16 行目**付近に移動し、次の内容に変更します。

   ```py
   "SELECT * FROM books WHERE name LIKE '%" + name + "%'"
   ```

1. エディター右上の **Commit changes...** ボタンをクリックします。表示された画面で **Create a new branch** のラジオボタンを選びます。
   **main ブランチにはコミットしないでください。**

1. **Propose changes** を選び、**Create pull request** をクリックします。ブランチ名には次の文字列を使用します。

   ```txt
   learning-codeql
   ```

1. 新しく表示されたページで、pull request の説明の下にある **Create pull request** ボタンを押します。

### ⌨️ やること: pull request を確認する

1. 必要に応じて、前の操作で作成した pull request を開きます。

1. pull request の一番下までスクロールし、`CodeQL` という名前のチェックを探します。pull request で提案されたコードの変更をスキャンする分析ジョブです。

   <img width="500" alt="実行中の CodeQL チェック" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/codeql-check-in-progress.png" />

1. ジョブがまだ実行中の場合は、完了するまで数分待ちます。

1. コメントの中から分析結果を探します。
   - SQL インジェクションの脆弱性が検出され、修正案も示されていることを確認します。
   - 現時点では、コメントへの対応や問題の解決は必要ありません。

   <img width="500" alt="コードスキャンの結果" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/code-scan-results.png" />

   > 💡 ヒント: **Show paths** リンクをクリックすると、ユーザー入力（source）からアプリケーション内を通り、
   > 処理される場所（sink）まで、アラートに関係するデータの流れを詳しく確認できます。

### ⌨️ やること: CodeQL のスキャンログを表示する

1. 上部のナビゲーションで **Actions** タブを選びます。

1. 左側のナビゲーションで **CodeQL** を選び、ワークフローの実行を絞り込みます。

   <img width="500" alt="CodeQL の絞り込み" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/codeql-filter.png"/>

1. **PR #2** という名前のワークフロー実行をクリックし、詳細ページを開きます。

   <img width="500" alt="CodeQL の設定" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/codeql-pr2.png"/>

1. **Show all jobs** をクリックして実行ジョブを展開し、**Analyze (python)** をクリックします。ワークフローの全 Step が表示されます。

   <img height="250" alt="マトリックスジョブ" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/matrix-jobs.png" />

   <img height="250" alt="CodeQL ジョブの一覧" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/list-of-codeql-jobs.png" />

1. 分析の項目を探し、必要に応じてログを確認します。

   <img width="500" alt="Python 分析のログ" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/python-analysis-logs.png" />

1. pull request を作成して CodeQL スキャンが完了したので、Mona が作業を確認しています。少し待って、コメントを見てください。
   進捗と次の Step が投稿されます。

> [!TIP]
> コードスキャンを pull request に組み込む方法について詳しくは、
> [pull request のコードスキャンアラートをトリアージする](https://docs.github.com/en/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/triaging-code-scanning-alerts-in-pull-requests)ページを参照してください。

---

## Step 3: CodeQL アラートを確認して対応を決める

pull request の変更を CodeQL で確認し、分析結果を表示できるようになりました。アラートの管理方法を学びます。

GitHub には、セキュリティに関係する問題を安全に管理する **Security and quality** タブがあります。
CodeQL は、多くの分析ツールと同じ標準形式でアラートを保存し、結果は **Code scanning** の領域に表示されます。

<img width="600" alt="Security and quality タブの概要" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/security-tab-overview.png" />

### アラートにはどのような情報が表示されるか

アラートの主要部分には、対応状況、影響を受けるブランチ、コード上の場所、重大度や
[CVE 識別番号](https://docs.github.com/en/code-security/security-advisories/working-with-repository-security-advisories/about-repository-security-advisories#cve-identification-numbers)などの分類情報が表示されます。

状況に関する情報の後には、問題の詳しい説明、推奨される解決策、変更案のコードが表示されます。

<img width="600" alt="アラートの追加情報" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/additional-information.png"/>

### CWE とは

CodeQL がスキャンするパターンの多くは、既存の脆弱性データベースに基づいており、理解しやすいように分類されています。

**Common Weakness Enumeration（CWE）**は、ハードウェアとソフトウェアの弱点や脆弱性を分類する仕組みです。
アプリケーションのソースコードに含まれるセキュリティ問題を説明し、分類するために使用します。
CWE について詳しくは、Wikipedia の「[Common Weakness Enumeration](https://en.wikipedia.org/wiki/Common_Weakness_Enumeration)」を参照してください。

### ⌨️ やること: 既存のアラートを表示する

1. 上部のナビゲーションで **Security and quality** タブを選びます。

1. 左側のナビゲーションで **Findings** の領域を探し、**Code scanning** を選びます。
   - アラートがないことを確認します。脆弱性を含む pull request のコードはまだマージされていないため、想定どおりの結果です。

1. 作成した pull request に戻ります。失敗したチェックは無視し、**Merge pull request** ボタンをクリックします。

   <img width="300" alt="Merge pull request ボタン" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/merge-button.png" />

1. **Delete branch** をクリックします。マージ後のブランチは不要です。

1. CodeQL が `main` ブランチへの新しい変更を分析するまで、少し待ちます。

1. **Security and quality** タブに戻ります。

1. 左側のナビゲーションで、**Code Scanning** の横に `1` と表示されていることを確認します。未対応のアラートが 1 件あることを示しています。

   <img width="250" alt="コードスキャンアラートの件数" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/code-scanning-alerts-count.png" />

### ⌨️ やること: アラートを確認する

1. 左側のナビゲーションで **Code scanning** を選びます。

1. 未対応のアラートをクリックします。

1. 概要、脆弱性の説明、推奨される解決策を確認します。

   <img width="600" alt="アラートの概要" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/alert-overview.png" />

1. 監査証跡に脆弱性の発生元が記録され、pull request から取り込まれたことが示されている点を確認します。

### ⌨️ やること: アラートを却下して再度開く

1. 右上にある **Dismiss alert** ドロップダウンをクリックします。

1. `Used in tests` を選び、次の説明を入力します。

   ```md
   This is a playground repository for learning about CodeQL alerts.
   ```

   <img width="300" alt="アラートを却下する選択肢" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/dismiss-alert-options.png" />

1. **Dismiss** ボタンをクリックします。
   - アラートの状態が `Dismissed` に変わります。
   - アラートを閉じた人と入力した説明を示す読み取り専用の項目が、監査証跡に追加されます。

   <img width="300" alt="アラートの却下を示す監査ログの項目" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/audit-log-alert-dismissed.png" />

1. 右上にある **Reopen alert** ボタンをクリックします。
   - アラートの状態が `Open` に戻ります。
   - アラートを開いた人を示す読み取り専用の項目が、監査証跡に追加されます。

1. アラートを閉じて再度開いたら、次のコメントを Issue に追加し、Mona に作業の確認と次の Step の投稿を依頼します。

   ```md
   Hey @professortocat, I've closed an reopened an alert. What is the next step?
   ```

---

## Step 4: セキュリティ脆弱性を修正する

最後に、CodeQL が提供する情報を使って脆弱性を詳しく理解し、修正します。

### ⌨️ やること: 未対応のアラートを解決する

1. 未対応のアラートを確認し、推奨される変更内容を把握します。

1. 上部のナビゲーションで **Code** タブを選びます。

1. `main` ブランチを開いていることを確認します。次に `server` フォルダーへ移動し、`routes.py` ファイルを選びます。

1. プレビューの右上にある **Edit** ボタンをクリックします。

   <img width="500" alt="Edit ボタン" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/edit-button.png"/>

1. **16 行目**付近に移動し、次の内容に変更します。

   ```py
   "SELECT * FROM books WHERE name LIKE %s", name
   ```

1. エディター右上の **Commit changes...** ボタンをクリックします。既定の選択肢を使い、`main` ブランチに直接コミットします。
   - CodeQL による新しいスキャンが開始されます。

1. **CodeQL** ワークフローが完了するまで少し待ちます。

1. **Security and quality** タブの **Code Scanning** 領域に戻ります。
   - 未対応のアラートがなく、解決済みのアラートが 1 件あることを確認します。よくできました！ 🎉
   - 解決済みのアラート、特に監査証跡を確認してもかまいません。

1. **Closed** をクリックし、解決したアラートを表示します。

   <img width="350" alt="Closed アラートを表示するボタン" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/closed-alerts-button.png" />

1. アラートを開き、アラートの修正方法が監査証跡に追加されていることを確認します。

   <img width="350" alt="修正内容を示すアラートの監査証跡" src="https://raw.githubusercontent.com/skills/introduction-to-codeql/main/.github/images/audit-trail-fixed-alert.png" />

1. アラートを修正したので、Mona が作業を確認しています。少し待って、コメントを見てください。進捗と次の Step が投稿されます。

---

## まとめ

演習を最後まで進めました！ 演習では次の操作を行いました。

- リポジトリで CodeQL によるコードスキャンを有効にしました。
- pull request を使って脆弱性を作り、検出しました。
- CodeQL アラートを確認して対応を決めました。
- セキュリティ脆弱性を修正し、アラートが解決されたことを確認しました。

演習を通して、GitHub のセキュリティ機能を使い、コードベースを安全に保つ方法を学びました。
健全なプロジェクトを維持するには、セキュリティアラートを定期的に確認して対応することが重要です。

### 次に学ぶこと

- [別の Skills 演習に取り組む。](https://github.com/skills)
- [CodeQL ドキュメント](https://codeql.github.com/docs/)でコードスキャンのカスタマイズ方法を学ぶ。
- [コードスキャンのドキュメント](https://docs.github.com/en/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/about-code-scanning)で外部のスキャンツールを接続する方法を学ぶ。
- [CodeQL CLI と VS Code 拡張機能](https://codeql.github.com/docs/codeql-cli/)を使い、ローカルで独自のクエリを実行、作成する。
- [コードスキャンアラートのトリアージガイド](https://docs.github.com/en/code-security/code-scanning/managing-code-scanning-alerts/triaging-code-scanning-alerts-in-pull-requests)でアラートを調査するときの推奨事項を確認する。
- [CodeQL クエリの高度な機能](https://docs.github.com/en/code-security/codeql-for-vs-code/using-the-advanced-functionality-of-the-codeql-for-vs-code-extension/creating-a-custom-query)を学び、複雑な独自分析を作成する。

---

## 終わったら

- 作成したリポジトリは残してかまいません。
- 質問は翌日の授業で受け付けます。
