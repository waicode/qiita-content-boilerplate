# qiita-content-boilerplate

VSCodeとDocker（devcontainer）で書くQiita執筆環境のボイラープレートです。

* Qiitaの執筆に便利なVSCode拡張機能やスニペットが自動的にインストールされます。
* VSCodeの見た目はQiitaのテーマカラーに合わせています。
* [qiita-sync](https://github.com/ryokat3/qiita-sync) を使って、マークダウンで書いた記事をQiitaへ投稿（同期）できます。
* [Qiita Markdown Preview](https://marketplace.visualstudio.com/items?itemName=ryokat3.vscode-qiita-markdown-preview)を使ってローカル環境でプレビューを確認しながら記事を書くことができます。
* 記事の内容は `markdownlint`, `textlint` でマークダウンの静的解析（lint）を行います。
* 英単語の誤字がないか `cspell`（Code Spell Checker）でチェックをします。
* `husky` と `lint-staged` でコミット時に自動でlintします。不正な形式の文章はコミットされません。
