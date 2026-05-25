# upstream-reflection（上流反映レビュー）

下流の成果物を上流資料と突き合わせ、**上流へ反映すべき変更候補をレビュー表として抽出**する
Claude Code スキル。現バージョンの対応ペアは **基本設計 → 要件定義書**。

## できること
- 「基本設計に在るが、要件定義に無い／矛盾する／曖昧なまま」を洗い出す。
- 各候補に **対象箇所・現状・反映案・根拠・優先度・確信度・判断理由** を付けたレビュー表を出力。
- 反映の最終判断は人間が行う（自動で上流資料を書き換えない）。

## 導入（業務PCへの設置）
1. この `upstream-reflection/` フォルダを丸ごと、Claude Code のスキル置き場へコピーする。
   - 個人用: `~/.claude/skills/upstream-reflection/`（Windows: `C:\Users\<ユーザ名>\.claude\skills\upstream-reflection\`）
   - プロジェクト用: リポジトリ直下の `.claude/skills/upstream-reflection/`
2. Claude Code を再起動（または再読込）してスキルが認識されることを確認する。
3. `samples/` は配布対象外（dev検証用）。配ってもよいが本番運用には不要。

## 使い方
1. 「基本設計を要件定義に照らして、上流への反映候補を出して」のように依頼する
   （`SKILL.md` の description に合致すると自動的に使われる）。
2. 下流資料（基本設計）と上流資料（要件定義）の場所を渡す。
   - 形式が Office/Wiki の場合は `references/ingestion.md` に従い変換、または PDF/Markdown でエクスポート。
3. 出力されたレビュー表を確認し、各行に **採否（採用／修正採用／却下）** と **FB理由** を記入する。
4. 記入したログを蓄積する（`feedback/feedback-log.template.md` を利用）。

## 精度を上げ続ける（重要）
- フィードバックを溜め、定期的に**蒸留**して `references/criteria.md` と `references/examples.md` を更新する。
- 手順は `feedback/README.md`。更新は `CHANGELOG.md` で版管理し、新版を再配布する。

## 拡張（他のレベルペア）
- 「要件定義→計画書」「詳細設計→基本設計」等を増やす場合、`references/criteria.md` に
  そのペア用の判断基準セクションを追加し、`SKILL.md` の「対応ペア」に追記する。

## 注意
- 資料を外部サービスへ送信しない。変換・処理はローカルで行う。
- フィードバックログに機密本文を貼らない（資料名＋章・項＋要旨で記録）。
- 出力はレビュー表まで。要件定義への反映可否は人間が決定する。

## 同梱ファイル
- `SKILL.md` — ワークフロー本体
- `references/` — taxonomy / criteria / checklist / examples / ingestion
- `templates/review-table.md` — 出力テンプレ
- `feedback/` — 記録方法と蒸留手順
- `CHANGELOG.md` — 同梱知識の版履歴
