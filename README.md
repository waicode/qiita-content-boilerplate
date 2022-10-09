# qiita-content-boilerplate

<img width="1624" alt="qiita-content-boilerplate_vscode_screenshot" src="https://user-images.githubusercontent.com/3455992/194735077-de194f7f-6f71-41ae-813e-b8a715bcd86d.png">

VSCodeとDocker（devcontainer）で書く**Qiita執筆環境のボイラープレート**です。このテンプレートを複製して、すぐに記事を書きはじめることができます。

* Qiitaの執筆に便利なVSCode拡張機能やスニペットが自動的にインストールされます。
* VSCodeの見た目はQiitaのテーマカラーに合わせています。
* [Qiita Sync](https://github.com/ryokat3/qiita-sync)を使って、マークダウンで書いた記事をQiitaへ投稿（同期）できます。
* [Qiita Markdown Preview](https://marketplace.visualstudio.com/items?itemName=ryokat3.vscode-qiita-markdown-preview)を使ってローカル環境でプレビューを確認しながら記事を書くことができます。
* 記事の内容は `markdownlint`, `textlint` でマークダウンの静的解析（lint）を行います。
* 英単語の誤字がないか `cspell`（Code Spell Checker）でチェックをします。
* `husky` と `lint-staged` でコミット時に自動でlintします。不正な形式の文章はコミットされません。

## 前提

記事を編集するエディタはVSCode（[Visual Studio Code](https://azure.microsoft.com/ja-jp/products/visual-studio-code/)）を使います。Qiitaの執筆に最適化されたVSCodeの拡張機能やスニペットが入ります。

また、Dockerで専用コンテナを準備して環境をつくります。そのため、ローカル環境にDockerのインストールが必要です。特にこだわりが無ければ、GUIで簡単にDockerコンテナを導入できる[Docker Desktop](https://www.docker.com/products/docker-desktop/)が（個人利用であれば）無料で使えて便利です。

VSCodeからコンテナにアクセスして執筆するため、[Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)のVSCode拡張機能も必要です。

利用にあたって、**ローカル環境にVSCodeとDockerが準備されていること**を前提としています。

## 使い方

まずは右上の **"Use this template"** をクリックして、このボイラープレートからリポジトリを複製します。

<div align="center">
<kbd>
<img width="1512" alt="qiita-content-boilerplate_use_this_template_screenshot" src="https://user-images.githubusercontent.com/3455992/194735757-4f848f85-0eb5-404e-8c00-796745f32e49.png" style="width:80%;"></kbd>
</div>

<br />

VSCodeで複製したリポジトリをクローンして **"Reopen in Container"** でコンテナを立ち上げます。

![qiita-template_devcontainerの起動](https://user-images.githubusercontent.com/3455992/194735782-bbaf9790-1b5c-4f79-baae-0cb2b7401ae4.gif)

<br />

コンテナを立ち上げると `docker/Dockerfile` の内容に基づきコンテナ環境を構築します。`package.json` に書かれたライブラリがインストールされます。また `devcontainer.json` に書かれた設定によって、VSCode拡張機能がインストールされます。

ローカルのエディタでQiitaの記事が執筆できるように[Qiita Sync](https://github.com/ryokat3/qiita-sync)のGithubアクションを設定しています。

Qiita SyncはQiita APIを活用した非公式の連携ツールです。Githubリポジトリにプッシュして同期アクションを実行すれば、連携したアカウントのQiita記事と同期されます。

詳しくはツール製作者の[@ryokat3](https://github.com/ryokat3)さんが書いている使い方の記事を確認してください。ご利用にあたって、連携対象のQiitaアカウントでQiita Access Tokenを発行し、記事を管理するGithubリポジトリへ登録する必要があります。

[GitHub連携でQiita記事を素敵な執筆環境で！](https://qiita.com/ryokat3/items/d054b95f68810f70b136)

なお、このボイラープレートでは誤った操作で意図しない同期が起こる事故を防ぐためにプッシュ時の自動同期はコメントアウトしています。

```yml:qiita_sync_check.yml
name: Qiita Sync

on:
  # push:
  #   branches:
  #     - main
  workflow_dispatch:

# 以下略
```

同期する際はブラウザ操作でGithubリポジトリのアクションから同期対象ブランチを選んで実行します。

また[Qiita Markdown Preview](https://marketplace.visualstudio.com/items?itemName=ryokat3.vscode-qiita-markdown-preview)の拡張機能を入れています。VSCodeのプレビュー機能で、実際にQiitaに記事が表示される際の見た目で確認できます。この拡張機能もQiita Syncと同じ方が製作しています。

記事を書く際は、**Qiitaに最適化されたVSCode拡張機能やスニペットを使う**と便利です。また、**コミット時に静的解析（lint）が実行**されます。文章が不正な場合、警告メッセージが表示されてコミットできません。

詳しい設定について、後述していきます。

## 設定内容

### 書くための設定

#### VSCode拡張機能でマークダウンを効率よく書く

マークダウンの文章を書く効率を上げる目的で以下の拡張機能を入れています。

| 拡張機能 | 説明 |
| ---- | ---- |
| [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) | ショートカットや便利なコマンド|
| [:emojisense:](https://marketplace.visualstudio.com/items?itemName=bierner.emojisense) | 絵文字入力の補助 |
| [Insert Date String](https://marketplace.visualstudio.com/items?itemName=jsynowiec.vscode-insertdatestring) | 現在時刻をショートカット入力|
| [Copy file name](https://marketplace.visualstudio.com/items?itemName=nemesv.copy-file-name) | ファイル名を右クリックメニューからコピー|
| [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense) | パスを入力補完 |

拡張機能の使い方は以下の記事で動画付きで詳しく解説しています。よければ参考にしてください。

[**Markdown（マークダウン）をVSCodeの拡張機能とスニペットで効率良く書く**](https://qiita.com/waicode/items/1310d3f0aeb24f393b88)

#### 独自のマークダウン記法はVSCodeスニペットで

`.vscode/markdown.code-snippets` にQiita独自の記法を含むマークダウン記法のスニペットを登録しています。

Qiitaで使えるマークダウン記法はQiita公式が書いた以下の記事を参考にしてください。

[Markdown記法 チートシート](https://qiita.com/Qiita/items/c686397e4a0f4f11683d)

### 静的解析（lint）の設定

このボイラープレートには、以下に対してlintする設定が入っています。

* マークダウンの形式（`markdownlint`）
* 文章の校正（`textlint`）
* 英単語の誤字（`cspell`）

また、マークダウンファイル以外はコードフォーマット（自動整形）を `prettier` を使って実施します。マークダウンファイルはmarkdownlintと設定が競合するため、意図的に対象から外しています。

#### VSCodeエディタ上で問題があればリアルタイムで確認

静的解析（lint）はVSCodeの拡張機能も入れているので、問題があればエディタ上で常に確認できます。

| 拡張機能 | 説明 |
| ---- | ---- |
| [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint) | VSCodeのエディタ上でマークダウン構造を解析 |
| [vscode-textlint](https://marketplace.visualstudio.com/items?itemName=taichi.vscode-textlint) | VSCodeのエディタ上でテキストを解析 |
| [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) | VSCodeのエディタ上で英単語の誤字をチェック |
| [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) | VSCodeでコードフォーマット（自動整形） |

#### コミット時にも確認して不正な形式のマークダウンを警告

`husky` と `lint-staged` でコミット時に自動でlintします。そのため、不正な形式の文章はコミットされません。

#### lintの詳細設定

ボイラープレートなので、特に設定を変更せずそのまま使えます。使っていきながら、好みの設定に書き換えてください。

##### markdownlint

デフォルトの構文チェックは厳しめに設定されています。

そのため  `.vscode/settings.json` と `.markdownlint-cli2.jsonc` で一部ルールを調整しています。

```jsonc
"markdownlint.config": {
  "line-length": false, // MD013: Disable the maximum number of characters per sentence
  "no-duplicate-heading": false, // MD024: Allow duplicate heading text
  "no-trailing-punctuation": false, // MD026: Allow headings with . ,;:
  "no-inline-html": false, // MD033: Allow HTML description
  "no-bare-urls": false // MD034: Allow URLs to be written as is
}
```

##### textlint

ベースとして以下の2つのプリセットを適用しています。

| プリセット名 | 説明 |
| ---- | ---- |
| [textlint-rule-preset-ja-spacing](https://github.com/textlint-ja/textlint-rule-preset-ja-spacing) | 日本語のスペース有無を決定するtextlintルールプリセット |
| [textlint-rule-preset-ja-technical-writing](https://github.com/textlint-ja/textlint-rule-preset-ja-technical-writing) | 技術文書向けのtextlintルールプリセット |

プリセットのままだと厳し過ぎる箇所があるため `.textlintrc` で設定を一部上書きしています。

```json
{
  "plugins": {
    "@textlint/markdown": {
      "extensions": [
        ".md"
      ]
    }
  },
  "filters": {
    "comments": true
  },
  "rules": {
    "prh": {
      "rulePaths": [
        "./prh/index.yml"
      ]
    },
    "preset-ja-technical-writing": {
      "sentence-length": {
        "max": 150
      },
      "no-exclamation-question-mark": {
        "allowFullWidthExclamation": true,
        "allowFullWidthQuestion": true
      },
      "ja-no-successive-word": false,
      "ja-no-mixed-period": {
        "allowPeriodMarks": [
          ":",
          "："
        ]
      },
      "no-doubled-joshi": {
        "strict": false,
        "allow": [
          "も",
          "や",
          "か"
        ],
        "separatorCharacters": [
          ",",
          "，",
          "、",
          ".",
          "．",
          "。",
          "?",
          "!",
          "？",
          "！",
          "「",
          "」",
          "\"",
          "”",
          "“"
        ]
      }
    },
    "preset-ja-spacing": {
      "ja-space-around-code": {
        "before": true,
        "after": true
      }
    }
  }
}
```

また、校正用辞書を `/prh/rules` へ追加できるようにしています。初期設定では `/prh/rules/tech.yml` に技術用語の校正辞書をいくつか登録しています。必要に応じて用語を追加してください。

```yml
meta:
  - title: 技術用語の固有名詞ルール
rules:
  - expected: インターフェース
    patterns:
      - インターフェイス
      - インタフェース
      - インタフェイス
    prh: 技術用語
  - expected: ソフトウェア
    pattern: ソフトウェアー
    prh: 技術用語
  - expected: ハードウェア
    pattern: ハードウェアー
    prh: 技術用語
  - expected: デフォルト
    pattern: ディフォルト
    prh: 技術用語
```

##### cspell

許可する言葉は `.cspell.json` の `words` に追加します。対象の文字列にカーソルを合わせてVSCodeのクイックフィックスで登録するのが便利です。

##### Prettier

`.prettierignore` に `*.md` 記載して、マークダウンファイルをコードフォーマットの対象外にしています。その他の設定は特に入れていません。自動整形時はデフォルト設定が適用されます。
