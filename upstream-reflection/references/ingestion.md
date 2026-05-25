# 読み取り・変換ガイド（混在形式対応）

両資料をテキスト化するための手順。**第一手段は Read**。変換が要る形式は
「ツールがあれば使う／無ければユーザにエクスポートを案内」というグレースフル方針。

> 機密保持: 変換は必ずローカルで行う。資料を外部サービスへアップロードしない。

## 0. 方針
1. まず形式を判定する（拡張子・中身）。
2. 直接 Read できるものはそのまま読む。
3. Office/Wiki は変換を試みる。変換ツールが無ければ、ユーザに **PDF か Markdown へのエクスポート**を依頼する。
4. 大規模資料は章・節単位に分割して読む（コンテキスト超過回避）。

## 1. 形式別の読み取り

### Markdown / テキスト / CSV
- Read で直接読む。表は Markdown/CSV のまま解釈できる。

### PDF
- Read の PDF 対応（`pages` 指定）で読む。大きい場合はページ範囲を分割。

### Word（.docx）
- 変換を試す（いずれか利用可能なもの）:
  - pandoc: `pandoc "in.docx" -t gfm -o "out.md"`
  - LibreOffice: `soffice --headless --convert-to txt:Text "in.docx"`
  - Python: `python -c "import docx"`（python-docx）で本文・表を抽出
- いずれも無ければ → ユーザに「PDF か Markdown でエクスポート」を依頼。

### Excel（.xlsx）
- 表が主役。シート単位で CSV/Markdown 化:
  - LibreOffice: `soffice --headless --convert-to csv "in.xlsx"`
  - Python: `python -c "import openpyxl"` または pandas で各シートを読み出し
- 無ければ → ユーザに「対象シートを CSV エクスポート」を依頼。

### PowerPoint（.pptx）
- pandoc / python-pptx で本文抽出、または PDF 化して Read。
- 無ければ → ユーザに「PDF でエクスポート」を依頼。

### Wiki / 課題管理（Confluence / Backlog / Redmine 等）
- ページを Markdown / HTML / PDF でエクスポートしてもらい、Read で読む。
- API 取得は環境・認証に依存するため、まずはエクスポート運用を基本とする。

## 2. 変換ツールの存在確認（実行前に）
- Windows(PowerShell): `Get-Command pandoc, soffice -ErrorAction SilentlyContinue`
- Python ライブラリ: `python -c "import docx, openpyxl"`（エラーなら未導入）
- 見つからない場合は無理に導入せず、§1 のエクスポート依頼に切り替える（ポータビリティ優先）。

## 3. 分割の目安
- 章/節見出しで分割し、上流・下流を**対応する章どうし**で突き合わせると精度が上がる。
- まず全体の目次・章立てを把握 → 章単位でレビュー表に積み上げる。
