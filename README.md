# upstream-reflection（上流反映レビュー）

下流の成果物を上流資料と突き合わせ、**上流へ反映すべき変更候補をレビュー表として抽出**する
Claude Code スキルの開発リポジトリ。現バージョンの対応ペアは **基本設計 → 要件定義書**。

## 構成
```
upstream-reflection-project/
├─ upstream-reflection/   ← ★配布するスキル本体（このフォルダを ~/.claude/skills/ へ）
├─ samples/               ← 合成サンプル（検証用。配布は任意）
└─ PROJECT_PLAN.md        ← 開発の計画書
```

## 配布スキルの導入
配布するのは `upstream-reflection/` フォルダのみ。導入・使い方は
[upstream-reflection/README.md](upstream-reflection/README.md) を参照。

- 個人用: `~/.claude/skills/upstream-reflection/`
- プロジェクト用: リポジトリ直下の `.claude/skills/upstream-reflection/`

## 精度向上の仕組み
レビュー結果（採否＋理由）を溜め、定期的に蒸留して判断基準・事例を更新するハイブリッド型。
詳細は [upstream-reflection/feedback/README.md](upstream-reflection/feedback/README.md)。

## 検証
`samples/` の合成ペアで受け入れ確認（再現率・除外トラップ）を行える。詳細は
[samples/03_期待候補_answer-key.md](samples/03_期待候補_answer-key.md)。
