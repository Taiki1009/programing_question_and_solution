# 技術試験の問題・回答管理と Ruby 実行環境

技術面接を管理するリポジトリです。
大項目ごとにディレクトリを分け、各問題フォルダに `problem.md`(問題) と `solution.rb`(回答) を配置します。
実行は最小構成の Docker 環境で行えます。

## 想定例

- `algorithms/two_sum/problem.md`
- `algorithms/two_sum/solution.rb`
- `data_structures/linked_list_cycle/problem.md`
- `data_structures/linked_list_cycle/solution.rb`

## 目的

- 問題文と回答コードを近接させて再利用・レビューを容易にする
- カテゴリ別に整理し、検索性・横展開を高める
- Docker で環境差異を排除し、すぐに実行できる状態を保つ

## ディレクトリ構成ルール

- 大項目(カテゴリ)単位のディレクトリを作成する: 例 `algorithms`, `data_structures`, `ruby_basics`, `web`, `sql`
- 各問題はカテゴリ配下にサブディレクトリを作成する: 例 `algorithms/two_sum`
- 各問題フォルダに次の基本ファイルを置く
  - `problem.md`: 問題定義
  - `solution.rb`: 回答実装 (単体で実行可能にする)
- 任意で追加可能
  - `README.md`: 補足や設計メモ
  - `input.txt`/`sample.json` などのサンプルデータ
  - `spec.rb` などの簡易テストスクリプト

## 命名規約

- ディレクトリ・ファイルは小文字スネークケース: 例 `two_sum`, `linked_list_cycle`
- 問題ファイル名は固定: `problem.md`
- 回答ファイル名は固定: `solution.rb`

## 問題テンプレート(推奨項目)

- タイトル
- 説明 / 背景
- 入力 / 出力仕様
- 制約 / 想定計算量
- 例(入出力数個)
- 実行方法のメモ(必要な引数や標準入力など)

## 新しい問題の追加手順

- カテゴリを決めてサブディレクトリを作成: 例 `algorithms/two_sum`
- `problem.md` を作成し、上記テンプレートに沿って記述
- `solution.rb` を作成し、単体実行できるように実装
- 必要ならサンプルデータや簡易テストを追加

## 実行方法(Docker)

- 前提: Docker / Docker Compose がインストール済み
- 任意の Ruby ファイルを実行
  - `docker compose run --rm ruby ruby path/to/file.rb`
- 例: ある問題の回答を実行
  - `docker compose run --rm ruby ruby algorithms/two_sum/solution.rb`
- 対話実行(IRB)
  - `docker compose run --rm ruby irb`

## Gem の利用

- `Gemfile` を用意すれば Bundler が使えます
  - 初期化: `docker compose run --rm ruby bundle init`
  - 追加/更新: `docker compose run --rm ruby bundle install`
- インストール済み gem は named volume `bundle` にキャッシュされます

## リポジトリ内の主なファイル

- `docker-compose.yml`: Ruby コンテナ定義(公式 `ruby:3.3-alpine` を利用、カレントを `/app` にマウント)
- `.dockerignore`: 不要ファイルの除外
- `main.rb`: 動作確認用サンプル(任意)。実際の問題はカテゴリ配下で管理してください

この方針に沿って、問題(md)と回答(rb)をセットで追加していってください。不明点や追加したい運用ルールがあれば相談してください。
