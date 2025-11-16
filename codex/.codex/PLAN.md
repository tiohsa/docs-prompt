# PLAN for Requirements Definition Automation

## Task: gen-requirements

- description: |
    プロジェクト情報 (inputs/project_info.yaml) と
    要件定義テンプレート (templates/requirements_template.md) をもとに、
    要件定義書ドラフトを生成し、docs/requirements に出力する。

- agent: RequirementsDefinitionAgent

- inputs:
    - path: inputs/project_info.yaml
      as: project_info_yaml
    - path: templates/requirements_template.md
      as: requirements_template
    - path: prompts/requirements_srs_prompt.md
      as: generation_prompt

- outputs:
    - path: docs/requirements/{{project_name}}-requirements.md
      from: llm_output

- steps:
    1. `project_info_yaml` を読み込み、YAML文字列として `{{project_info_yaml}}` として扱えるようにする。
    2. `requirements_template` を読み込み、テンプレート全体を `{{requirements_template}}` として扱えるようにする。
    3. `generation_prompt` をベースに、上記2つを埋め込んだプロンプトを LLM に送信する。
    4. 返ってきた Markdown を `docs/requirements/{{project_name}}-requirements.md` に保存する。


## Task: review-requirements

- description: |
    既存の要件定義書 (docs/requirements/{{project_name}}-requirements.md) をレビューし、
    問題点・改善提案・修正版サンプルを生成する。

- agent: RequirementsReviewAgent

- inputs:
    - path: docs/requirements/{{project_name}}-requirements.md
      as: requirements_doc
    - path: prompts/requirements_review_prompt.md
      as: review_prompt

- outputs:
    - path: docs/requirements/{{project_name}}-requirements-review.md
      from: llm_output

- steps:
    1. `requirements_doc` を読み込み、LLM が参照できるプレーンテキストとして保持する。
    2. `review_prompt` に `{{requirements_doc}}` を埋め込み、LLM に送信する。
    3. 返ってきたレビュー結果を `docs/requirements/{{project_name}}-requirements-review.md` に保存する.
