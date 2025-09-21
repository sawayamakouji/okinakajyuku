---
title: Excel議事録 → Markdown 変換ガイド
description: 25年度議事録フォルダ内の .xlsx をまとめてMarkdown化する方法（非エンジニア向け）。
---

# Excel議事録 → Markdown 変換ガイド

## できること
- 指定フォルダ（例: 25年度議事録）内のExcelファイル（.xlsx）をまとめて読み取り、GitHubで読みやすいMarkdownに変換します。
- 1つのファイルに集約、またはファイルごとに個別のMarkdownを出力できます。

## 事前準備
- Python（3.9+ 目安）
- パッケージのインストール
  - `pip install openpyxl`

## ファイルの場所
- 例: `C:\Users\saway\okinakajyuku\okinakajyuku\25年度議事録`
- フォルダ名に日本語が含まれていてもOKです。

## 使い方（例）
PowerShellでリポジトリ直下に移動して実行します。

1) 1つのMarkdownに集約する（おすすめの最初の一歩）
```
python .\scripts\read_excel_minutes.py \
  --base-dir "C:\\Users\\saway\\okinakajyuku\\okinakajyuku\\25年度議事録" \
  --output minutes_summary.md
```
- 実行後、`minutes_summary.md` が作成されます。

2) ファイルごとに個別のMarkdownを出力する
```
python .\scripts\read_excel_minutes.py \
  --base-dir "C:\\Users\\saway\\okinakajyuku\\okinakajyuku\\25年度議事録" \
  --per-file --output-dir docs\minutes
```
- 実行後、`docs/minutes/` に `元Excel名.md` が複数生成されます。

## よくある質問（FAQ）
- 表が崩れる / 長文がある
  - セル内の改行は `<br>` に置換しています。表幅が広い場合は、後から箇条書きへ整形してください。
- 一時ファイルが混じる
  - `~$` で始まる一時ファイルは除外しています。
- シートが空の場合
  - そのシートはスキップします。

## 参考
- スクリプト本体: `scripts/read_excel_minutes.py`
- 生成結果をチームでレビューしたい場合は、ブランチを切ってPRを作成すると安全です。

