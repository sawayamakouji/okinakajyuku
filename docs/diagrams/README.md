# Mermaid 図の元データ

- 目的: Markdown内のMermaid図と同じ内容を、`.mmd` テキストとして保管します。
- 利点: テキストなので差分レビューが容易。必要に応じて `.svg` に書き出してスライドやPDFに貼れます。

## ファイル一覧
- `workflow.mmd` … Clone / Pull / Commit / Push / PR の全体像
- `push-pull-sequence.mmd` … Push / Pull の時系列（シーケンス図）
- `first-step-flow.mmd` … はじめてのフロー（クローン→編集→コミット→PR）
- `branch-pr.mmd` … ブランチとPRの関係

## ローカルでSVG出力
Node.js 環境で以下を実行します。

```bash
npm i -g @mermaid-js/mermaid-cli
for %f in (docs\diagrams\*.mmd) do mmdc -i "%f" -o "%~dpnf.svg"
```

PowerShell の例:

```powershell
npm i -g @mermaid-js/mermaid-cli
Get-ChildItem docs/diagrams/*.mmd | ForEach-Object { mmdc -i $_.FullName -o ($_.FullName -replace '\\.mmd$','.svg') }
```

## GitHub Actions（自動生成）
`.mmd` 変更時に `.svg` を自動生成してコミットするワークフローを `.github/workflows/mermaid-svgs.yml` に用意できます。

