# JDim RFCs

[JDim]を開発するために共有するべき事項を文書にまとめ管理するリポジトリです。
RFCプロセスはプロジェクトのメンバーだけでなくJDimの開発に参加したい方に開かれています。

RFCのリストは[Wiki][rfc-index]を参照してください。

## RFCプロセスで扱う事項
開発・保守に関すること、開発・保守に影響を与える変更について扱います。
バグ修正や互換性に影響のない変更はRFCプロセスを経ずに変更しても大丈夫です。

例:

- RFCプロセスについて
- RFC文書の書式（テンプレート）
- リリースサイクル
- サポートするプラットフォーム
- ツールチェーンやライブラリの要件
- ソースコードのスタイルガイド
- 設定ファイルの仕様
- 互換性の無い変更

## RFCプロセスの流れ
1. 文書の新規作成または更新案を作りPull request(PR)を開く
2. PRはRFCメンテナーにレビューされ必要に応じて修正をしていく
3. 変更のマージまたは却下が決定される
4. 取り入れられた提案に基づいて開発していく

## RFC文書の書式
Markdown形式を使います。詳細は[テンプレート]を見てください。

## RFCプロセスに参加する方法

#### 新しい提案をする
新しい提案を行う場合は文書を新規作成します。
`docs/`内にファイル名 `<4桁のRFC番号>-<半角英数字のタイトル>.md` で[テンプレート]を参考にMarkdownファイルを作成してください。
RFC番号が重複した場合や予約済の番号は変更をお願いすることがあります。

例: `0404-not-found.md`

NOTE: RFC番号の内0000〜0009、0404、9999は予約されています。

#### 既存の文書を変更する
タイプミスの修正、文面の調整、項目の更新や追加などは既存の文書を変更してください。
大部分を書き換える場合はかわりに新しい文書を作成してください。

#### ~~既存の文書を削除する~~
既存の文書は削除しないでください。廃止や無効にするには置き換える内容で新しい文書を作ります。

## ライセンス
JDim RFCs は [MIT] と [Apache-2.0] のデュアルライセンスで公開されています。
RFCのコピーを受け取った方は両方またはどちらかのライセンスを選んで利用してください。


[rfc-index]: https://github.com/JDimproved/rfcs/wiki/rfc-index
[JDim]: https://github.com/JDimproved/JDim/ "2ch browser for linux"
[テンプレート]: https://github.com/JDimproved/rfcs/tree/master/0000-template.md

[MIT]: https://github.com/JDimproved/rfcs/tree/master/LICENSE-MIT
[Apache-2.0]: https://github.com/JDimproved/rfcs/tree/master/LICENSE-APACHE
