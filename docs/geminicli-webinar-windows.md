---
title: Windows向けGEMINICLI入門ウェビナー（非エンジニア向け・約40分）
description: Node.jsとGEMINICLIのセットアップから基本操作、Codespacesでの利用まで。非エンジニアでも自分で入れて今日から使える。
---

# Windows向けGEMINICLI入門ウェビナー（非エンジニア向け・約40分）

## 概要
- 目的: 非エンジニアでもWindowsでGEMINICLIを“自分で入れて、すぐ使える”ようにする
- 対象: Windowsユーザー（Macは手順の解説のみ）、GitHub Codespaces利用者
- ゴール: Node.jsとGEMINICLIのセットアップ完了・シンプルな使い方を体験

## アジェンダ（タイムライン）
- 0–5分: オリエンテーション（できること・準備物）
- 5–12分: Node.jsのインストール（Windows）
- 12–20分: GEMINICLIのインストール＆APIキー設定（Windows）
- 20–30分: 基本の使い方デモ（質問/要約/翻訳/テンプレ）
- 30–36分: GitHub Codespacesでの利用（クラウド環境）
- 36–39分: よくあるトラブル解決
- 39–40分: まとめと次の一歩

## 事前準備（参加者への案内）
- アカウント: Google AI Studio等でAPIキーを発行（使用するCLIに合わせて名称は読み替え）
- PC: Windows 10/11、管理者権限（推奨）
- ネット環境: 安定した回線
- 注意: APIは従量課金や日次上限あり。機密情報は入れない

## 想定するGEMINICLIについて
- npm（Node.js）からインストールできる“Gemini向けCLI”を前提に説明
- 実際のパッケージ名/コマンド名は環境で異なる場合あり
  - 例: `npm install -g gemini-cli` で `gemini` コマンドが使えるタイプ
  - 組織内配布や別名（例: `gmn`, `gemi`）なら、その名称に置き換える
- 当日: `gemini --help`（または手元のCLIの`--help`）でコマンド一覧を確認しつつ進行

---

## 0–5分｜オリエンテーション
- できること: 文章要約、翻訳、メール文面作成、アイデア出し、CSVの簡易説明など
- 今日のゴール: インストール→APIキー設定→3つの基本操作
- セキュリティ: APIキーはパスワード同等。絶対に共有しない

## 5–12分｜Node.jsインストール（Windows）
- ダウンロード: https://nodejs.org/ から LTS を選択してインストール
- インストーラのポイント: “Automatically install the necessary tools”は基本オフでOK
- 動作確認（PowerShellを開く）
  - `node -v`（バージョン表示でOK）
  - `npm -v`
- トラブル時
  - コマンドが見つからない → PowerShellを再起動 / 再ログイン
  - 会社PCで制限 → 管理者に相談、もしくはCodespacesを使う

## 12–20分｜GEMINICLIインストール＆APIキー設定（Windows）
- GEMINICLIのインストール（例）
  - `npm install -g gemini-cli`
  - 成功確認: `gemini --version` または `gemini --help`
- APIキーを環境変数に設定（PowerShell・ユーザー環境）
  - 永続設定: `setx GEMINI_API_KEY "ここにあなたのAPIキー"`
  - 反映: 新しいPowerShellを開く（またはPC再起動）
  - 確認: `echo $env:GEMINI_API_KEY`（表示されればOK）
- 代替（より確実）
  - `[Environment]::SetEnvironmentVariable("GEMINI_API_KEY","<キー>","User")` → 新しいPowerShellで反映
- トラブル時
  - `gemini`が見つからない → `npm config get prefix` のパスがPATHに含まれているか確認。PowerShell再起動
  - プロキシ環境 → `npm config set proxy <URL>`（必要な場合）

## 20–30分｜基本の使い方デモ
- 単発の質問（プロンプト）
  - 例: `gemini prompt "会議の要点を5行でまとめて"`
  - コツ: 具体・制約・出力形式（箇条書き/JSON）を先に伝える
- 翻訳・言い換え
  - 例: `gemini prompt "次の文をやさしい日本語に: <貼り付け文>"`
  - 長文はテキストファイルで渡す例: `type .\input.txt | gemini prompt --stdin "これを300文字以内で要約して"`
- 定型文テンプレ（メール/お礼/依頼）
  - 例: `gemini prompt "社内向けの依頼メールを、丁寧で簡潔に。要素: 納期=金曜、資料添付あり"`
- モデル切り替え（CLIが対応していれば）
  - `--model gemini-1.5-flash`（速さ・安さ重視）
  - `--model gemini-1.5-pro`（精度重視）
- 便利オプション（CLI依存）
  - `--output markdown` や `--format json` など出力整形がある場合は活用
  - `--system` で役割指示（例: “あなたは広報担当。口調は丁寧で簡潔に。”）
- 注意
  - 機密情報は入れない
  - 生成結果は必ず目視確認（事実誤りに注意）

## 30–36分｜GitHub Codespacesで使う（クラウド環境）
- 使う場面
  - 会社PCに入れにくい/権限がない、どこからでも同じ環境を使いたい
- 手順（概略）
  - GitHubで任意のリポジトリ → “Code” → “Create codespace on main”
  - ターミナルでNode確認: `node -v`（なければ）`nvm install --lts && nvm use --lts`
  - GEMINICLIインストール: `npm install -g gemini-cli`
  - APIキーの安全な渡し方
    - GitHub “Settings” → “Codespaces” → “Secrets” → `GEMINI_API_KEY` を作成
    - 新しいCodespaceでは自動で環境変数として利用可能
  - 使い方はローカルと同じ: `gemini prompt "～～～"`
- メリット
  - ローカルに入れなくてもOK、すぐ試せる
  - 環境差異が少なくトラブルが起きにくい

## 36–39分｜よくあるトラブルと対処
- `gemini`が見つからない
  - PowerShellを再起動
  - `npm config get prefix` をPATHに追加（例: ユーザーの`AppData\Roaming\npm`）
- APIキー関連のエラー
  - 環境変数名のスペル確認（例: `GEMINI_API_KEY`）
  - キーの有効性・利用上限（Quota）を確認
- 文字化け/日本語が崩れる
  - PowerShellのフォント/文字コード設定、必要なら `chcp 65001`（UTF-8）
- 社内プロキシ
  - `npm config set proxy/https-proxy`、社内ドキュメントを参照
- 実行が遅い/高コスト
  - 軽量モデル（例: `gemini-1.5-flash`）を優先
  - 出力を短く指示、不要な情報は省く

## 39–40分｜まとめ・次の一歩
- 今日の達成
  - Node.jsとGEMINICLIのセットアップ（Windows）
  - 3つの基本操作（要約・翻訳・定型文作成）
  - Codespacesでの代替手段
- 次の一歩
  - 自分の業務テンプレを3つ作成
  - よく使うプロンプトを`.txt`で保存し再利用
  - モデル切替や出力形式オプションを試す

---

## 配布用チートシート（抜粋）
- 確認: `node -v` / `npm -v` / `gemini --help`
- インストール（例）: `npm install -g gemini-cli`
- APIキー（Windows・永続）: `setx GEMINI_API_KEY "<キー>"` → 新しいPowerShellで有効
- 単発質問: `gemini prompt "要約して（200文字/箇条書き3点）"`
- ファイル要約（例）: `type .\input.txt | gemini prompt --stdin "箇条書き5点で要約"`
- モデル切替（CLIが対応時）: `--model gemini-1.5-flash` / `--model gemini-1.5-pro`

## スピーカーノート（進行のコツ）
- まず“できること”を具体例で見せる → 次に入れ方
- コマンドはゆっくり入力し、キーワードを口頭で復唱
- エラー時は「焦らない・順番に確認」を実演
- Macの方へは代替手順だけ軽く（Homebrew例: `brew install node` → `npm i -g gemini-cli` → `export GEMINI_API_KEY=...`）

