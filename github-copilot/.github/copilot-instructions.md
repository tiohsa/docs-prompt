# GitHub Copilot Repository Instructions

このリポジトリでは GitHub Copilot を使って  
**ソフトウェア開発の要件定義書を自動生成・レビュー**します。

---

## 共通ポリシー

- ドキュメントは **日本語 / Markdown形式** とする
- 生成先は `docs/requirements/` 配下とする
- `templates/requirements_template.md` の章立ては絶対に崩さないこと
- 不足情報は推測せず、次のいずれかに列挙する
  - 「前提条件」
  - 「未確定事項」
  - 「要確認事項（質問リスト）」

---

## 要件定義書生成ルール

- 入力は必ず以下を使用する  
  - `inputs/project_info.yaml`  
  - `templates/requirements_template.md`
- 出力ファイル名  
  - `docs/requirements/{{project_name}}-requirements.md`
- 生成物には Mermeid、表、箇条書きを適宜使用する

---

## 要件定義書レビューのルール

- レビュー対象：  
  `docs/requirements/*-requirements.md`
- 出力先：  
  `docs/requirements/*-requirements-review.md`

- レビュー観点：
  - 背景・目的
  - スコープ・機能/非機能
  - 制約条件
  - リスク
  - 整合性・一貫性
  - 曖昧表現の有無

- レビュー結果の構成：
  1. 総評  
  2. 指摘事項一覧（テーブル）  
  3. 改善後のサンプル抜粋  
  4. 追加で確認すべき質問リスト

---

## Plan / Agent モードガイドライン

- Plan モードでは、次の 3 ステップを基本とする：
  1. プロジェクト情報とテンプレートの読込  
  2. 要件定義書の生成 or レビュー  
  3. docs 配下へのファイル保存  

- Agent モードでは、**章立てと構成を壊さず安全に編集**する