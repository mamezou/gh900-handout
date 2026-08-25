# 演習 16 日本語訳：GitHub Copilot で Python Web API を更新する

Microsoft Learn「GitHub Copilot を使用して Python Web API を更新する」の日本語手順です。Learn の日本語ページには
**演習を開始する Codespace のリンクが表示されません**（英語ページには表示されます）。下の開始リンクから始めてください。

- コメント、変数名、エンドポイント名は英語のままにしています。**指定された文字列は変えずに入力してください。**
- VS Code の画面が日本語表示の場合、Copilot の候補を確定するボタンは「保持」（英語表示では **Keep**）です。
- 時間の目安：15〜20 分。ブラウザーの Codespace で完結します。
- 開始前に https://github.com/settings/copilot で Copilot Free の使用状況を確認してください。

**演習の開始**: [Codespace を作成する](https://codespaces.new/MicrosoftDocs/mslearn-copilot-codespaces-python)
→ 構成を確認して **Create codespace** を押します。1〜3 分でブラウザーに VS Code が開きます。

> **注意**: このページは手順の全体像です。実際の操作は Codespace の VS Code で行います。

---

## 事前確認

1. Codespace が開いたら、下部の **Terminal** で初期化の完了を待ちます。Web API が自動で起動します。
2. ポート 8000 の転送 URL、または同じ URL の `/docs` を開き、変更前の API を一度実行します。

## 手順 1: Pydantic モデルを追加する

1. **Explorer** で `main.py` を開きます。
2. `text` という文字列フィールドを持つ Pydantic モデルを作るよう、コメントで指示します。
3. Copilot の候補が次の形になっていることを確認してから採用します。

    ```python
    class Text(BaseModel):
        text: str
    ```

## 手順 2: 新しいエンドポイントを生成する

1. `main.py` に次のコメントをそのまま入力します。

    ```python
    # Create a FastAPI endpoint that accepts a POST request with a JSON body containing a single field called "text" and returns a checksum of the text
    ```

2. Copilot が生成したエンドポイントを読み、HTTP メソッドとパス、受け取る本文の形を確認してから採用します。

## 手順 3: 不足している import を追加して動作を確認する

1. 生成されたコードは `base64` と `os` を使います。import が無いとアプリケーションが停止するため、Copilot Chat に
   不足している import を尋ねるか、ファイルの先頭に次の 2 行を追加します。

    ```python
    import base64
    import os
    ```

2. アプリケーションを再実行し、`/docs` を開いて新しいエンドポイントが表示されることを確認します。
3. 正常な入力と、空文字列などの不正な入力の両方を試します。

## 終わったら

- ターミナルで `git diff` を実行し、Copilot が生成した範囲を自分の言葉で説明できるか確認します。
- 作業を残す場合はコミットして push し、https://github.com/codespaces で Codespace を停止します。

## 原本（英語）

- [Microsoft Learn（英語ページ、開始リンクあり）](https://learn.microsoft.com/en-us/training/modules/introduction-copilot-python/5-exercise-python-web-api)
- [知識チェック](https://learn.microsoft.com/ja-jp/training/modules/introduction-copilot-python/6-knowledge-check)
