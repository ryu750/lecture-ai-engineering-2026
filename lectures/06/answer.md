# 第6回 解答

## 演習

<!-- [tool call] の行は、表示された行をそのまま貼り付けてください。終わらなかった STEP は、空欄のままでかまいません。 -->

- STEP 1 のツール名：`glossary_search_glossary`
- STEP 2 の [tool call]：`glossary_search_glossary({'query': '3レベル'})`
- STEP 3 の [tool call]：`fetch_fetch({'url': 'https://modelcontextprotocol.io/'})`
- STEP 4 の [tool call]：
  - `aws_aws___search_documentation({'topics': ['general'], 'search_phrase': 'Amazon S3 バージョニング 概要'})`
  - `aws_aws___search_documentation({'search_phrase': 'Using versioning in S3 buckets', 'topics': ['general']})`
- 気づき・疑問：設定ファイルに接続先を追加するだけで、Codespaces内で起動するFetchと、AWS側で動く検索ツールの両方を同じエージェントから使えることが分かりました。STEP 4では、最初に日本語で検索し、その後、英語の検索語に変えたところ、S3のバージョニングを直接説明する節が返ってきた点が印象に残りました。モデルはどのように、最初の検索結果だけで回答できるか、検索語を変えて調べ直す必要があるかを判断しているのでしょうか。

## 宿題

<!-- 基礎・実装・発展のどれか1つに取り組めば完了です。 -->

- 取り組んだレベル：基礎
- やったこと：`app/mcp_server.py` に `server.tool()(tools.get_lecture_summary)` を1行追加し、講義概要を取得する関数をMCPツールとして公開した。
- 結果：「第2回では何を学びますか？」と質問すると、`glossary_get_lecture_summary` が第2回の概要を取得した。`uv run pytest -q` の結果は `21 passed in 4.77s` だった。
  - `[tool call]   glossary_get_lecture_summary({'lecture': 2})`
- 気づき・疑問：エージェント側のコードを書き換えずサーバー側に1行追加するだけで、既存の関数を新しいツールとして使えることが分かった。また、ログから、質問の第2回が引数の `lecture: 2` に変換されていることを確認できた。
