# Gemini Meeting Assistant

音声ファイルをアップロードし、Google Gemini API を利用して文字起こし、要約、キーワード抽出、アクションアイテム抽出を行うことができるWebアプリケーションです。文字起こし結果は編集可能で、複数の形式でダウンロードできます。

![スクリーンショット](/screenshot.png)

## ✨ 主な機能

*   **音声ファイルアップロード**: ドラッグ＆ドロップまたはファイル選択ダイアログで音声ファイル (audio/*) をアップロードします。
*   **Geminiモデル選択**: 文字起こしや各種抽出に使用するGeminiモデルを選択できます (Gemini 1.5 Pro, Gemini 1.5 Flash, Gemini 2.5 Pro Experimental)。
*   **話者数の指定 (任意)**: 事前に話者数を指定することで、話者分離の精度向上を試みることができます。
*   **音声文字起こし**: Gemini APIを利用して音声ファイルをテキストに変換し、話者ごとに発言を分離します。
*   **結果の編集**:
    *   表形式で表示された文字起こし結果の各行（話者名、発言内容）を直接編集できます。
    *   任意の位置に行を追加したり、不要な行を削除したりできます。
    *   検出された話者名を一括で任意の名前に変更できます。
*   **AIによる追加処理**:
    *   **要約生成**: 文字起こし結果全体を要約し、Markdown形式で表示・ダウンロードできます。
    *   **キーワード抽出**: 会話の中から重要なキーワードやトピックを抽出し、チップ形式で表示します。
    *   **アクションアイテム抽出**: 会話の中から担当者、タスク内容、期限（検出可能な場合）を含むアクションアイテムを抽出し、リスト形式で表示します。
*   **結果のダウンロード**:
    *   文字起こし結果を CSV (.csv)、Markdown (.md)、テキスト (.txt) 形式でダウンロードできます。
    *   生成された要約を Markdown (.md) 形式でダウンロードできます。
*   **進捗表示とエラーハンドリング**: APIリクエスト中の進捗状況や、APIキーエラー、クォータ超過、ファイル形式エラーなどの問題発生時に分かりやすいメッセージを表示します。
*   **レスポンシブデザイン**: Material UI Grid V2 を使用し、デスクトップとモバイルデバイスの両方で利用しやすいように考慮されています。

## 🛠️ 技術スタック

*   **フロントエンド**: React (Hooks API)
*   **UIライブラリ**: Material UI (MUI) v5
*   **AI**: Google Gemini API (@google/generative-ai)
*   **ファイル処理**:
    *   react-dropzone (ファイルアップロード)
    *   papaparse (CSV生成)
*   **Markdown**:
    *   react-markdown (表示)
    *   remark-gfm (GitHub Flavored Markdown プラグイン)

## ⚙️ セットアップと実行方法

### 前提条件

*   Node.js (v18以上推奨) と npm (または yarn)（[公式サイト](https://nodejs.org/ja)から取得）
*   Google Gemini API キー ([Google AI Studio](https://aistudio.google.com/app/apikey) から取得)
*   対応するWebブラウザ (Chrome, Firefox, Safari, Edgeなど)

### 手順

1.  **リポジトリをクローン**:
    ```bash
    git clone https://github.com/あなたのユーザー名/リポジトリ名.git
    cd リポジトリ名
    ```

2.  **依存関係をインストール**:
    ```bash
    npm install
    # または
    # yarn install
    ```

3.  **開発サーバーを起動**:
    ```bash
    npm start
    # または
    # yarn start
    ```

4.  **ブラウザでアクセス**:
    Webブラウザで `http://localhost:3000` (またはターミナルに表示されたアドレス) を開きます。

## 🚀 使い方

1.  **APIキーを入力**: 画面上部の「Gemini API Key」フィールドにあなたのAPIキーを入力します。
2.  **モデルを選択**: ドロップダウンメニューから使用したいGeminiモデルを選択します。
3.  **話者数を指定 (任意)**: 会話に参加している話者の人数が分かっている場合、入力すると精度が向上する可能性があります。
4.  **音声ファイルをアップロード**:
    *   指定エリアに音声ファイルをドラッグ＆ドロップします。
    *   または、「ファイルを選択」ボタンをクリックしてファイルを選択します。
5.  **文字起こしを開始**: 「文字起こし開始」ボタンをクリックします。処理中は進捗が表示されます。
6.  **結果を確認・編集**:
    *   文字起こし結果が表形式で表示されます。
    *   セルをクリックすると内容を編集できます。Enterキー (テキストエリアではShift+Enterで改行、Enterで保存) または他の場所をクリックすると保存されます。Escキーでキャンセルできます。
    *   「話者名の一括編集」セクションで、デフォルトの話者名（話者Aなど）を実際の名前に一括変更できます。
    *   各行の右側にあるゴミ箱アイコンで行を削除できます。
    *   各行の右下（およびテーブルヘッダーの右下）にある「+」アイコンで行を追加できます。
7.  **追加処理を実行**:
    *   「要約を作成」ボタンで会話の要約を生成します。
    *   「キーワードを抽出」ボタンでキーワードを抽出します。
    *   「アクションアイテムを抽出」ボタンでアクションアイテムを抽出します。
    *   各処理の結果はカード形式で表示され、エラーが発生した場合はエラーメッセージが表示されます。
8.  **結果をダウンロード**:
    *   文字起こし結果表の上にある「ダウンロード」ボタンから、CSV, Markdown, TXT形式でダウンロードできます。
    *   要約カード内の「Markdownで保存」ボタンから、要約をダウンロードできます。

## ⚠️ 注意点・制限事項

*   **APIキー**: このアプリケーションを使用するには、有効なGoogle Gemini APIキーが必要です。APIキーは安全に管理してください。
*   **API利用料・制限**: Google Gemini API の利用には、料金が発生する場合や、無料利用枠、リクエスト数などの制限がある場合があります。詳細は[Google AIの料金体系](https://ai.google.dev/pricing)を確認してください。特に、無料枠の上限 (Quota) に達するとエラーが発生します。
*   **処理時間**: 音声ファイルの長さやサイズ、選択したモデルによって、文字起こしや他のAI処理にかかる時間が変動します。
*   **精度**: 文字起こし、話者分離、要約、キーワード抽出、アクションアイテム抽出の精度は、入力される音声の品質（ノイズ、話者の明瞭さなど）、会話の内容、選択したGeminiモデルの性能に依存します。常に完璧な結果が得られるとは限りません。
*   **ファイルサイズ**: ブラウザやAPIの制約により、非常に大きな音声ファイルの処理は失敗する可能性があります。
*   **実験的モデル**: `gemini-2.5-pro-exp-03-25` は実験的なモデルであり、予告なく変更または利用できなくなる可能性があります。

##🤝 貢献

バグ報告、機能提案、プルリクエストは大歓迎です。Issueを作成するか、プルリクエストを送ってください。

##📜 ライセンス

このプロジェクトは [MITライセンス](LICENSE) の下で公開されています。