# gh-aw-compile-action

GitHub Agentic Workflows の `.md` ファイルに変更があった際に `gh aw compile` を実行する GitHub Action です。

## 使い方

`.github/workflows/aw-compile.yml` に以下のワークフローを追加します。

```yaml
name: Compile Agentic Workflows

on:
  push:
    paths:
      - '**/*.md'
  pull_request:
    paths:
      - '**/*.md'

jobs:
  compile:
    runs-on: ubuntu-latest
    permissions:
      contents: read
    steps:
      - uses: actions/checkout@v4
      - uses: 7474/gh-aw-compile-action@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
```

## Inputs

| 名前    | 必須 | デフォルト | 説明                        |
|---------|------|------------|-----------------------------|
| `token` | Yes  | -          | `gh` CLI が使用する GitHub トークン |

## 動作

1. `gh extension install github/gh-aw` で `gh aw` 拡張をインストールします。
2. `gh aw compile` を実行して Agentic Workflows の `.md` ファイルをコンパイルし、`.lock.yml` を生成します。
