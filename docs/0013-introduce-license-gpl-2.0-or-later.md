<!--
このファイルはRFC文書のテンプレートです。
新しい文書を作成する際にコピーしてお使いください。
ファイルは MIT or Apache-2.0 のデュアルライセンスで取り込まれます。

# ファイルの構成
RFC文書のファイル形式はMarkdownを使用します。
文書の構成はテンプレートに従わなくても良いです。
不要な項目の省略などフォーマットの変更は自由に行ってください。

# ファイルの編集
アンダースコアで囲われた部分は文書作成者が趣旨にあった内容に置き換えてください。
このコメントは削除して構いません。
-->

# ライセンス GPL-2.0-or-later を導入する
_ファイル冒頭にタイトルを書きます。タイトルにRFC番号を含める必要はありません。_

- [Abstract](#Abstract)
- [Specification](#Specification)
- [Examples](#Examples)
- [Motivation](#Motivation)
- [Rationale](#Rationale)
- [Backwards Compatibility](#Backwards)
- [Rejected Ideas](#Rejected)
- [Open Issues](#Issues)


<a name="Abstract"></a>
## Abstract
_文書の内容をまとめた概要を書きます。_

JDimのライセンスを **GPL2** から **GPL-2.0-or-later** に変更するためソースコードや文書の修正に新たなルールを設けます。

ライセンス変更は新しく GPL-2.0-or-later のファイルを作成・追加して
既存の GPL2 のファイルをすべて削除することで実現します。

<a name="Specification"></a>
## Specification
_機能の追加や変更を提案するときは仕様を書きます。_

GPL2 はコピーレフト型ライセンスであるためファイルを編集したすべての貢献者(著作者)が承諾しないとライセンス変更ができません。
承諾を得るのが困難な部分もあるため一挙に変更するのではなく継続的な取り組みで変えていきます。

新しい修正(パッチやコミット)を GPL-2.0-or-later のライセンスで取り込むことで
既存のファイル(GPL2)とライセンス互換性を持たせます。

#### ライセンス変更の方法

変更のために以下の手続きを進めていきます。

* RFCが承認された後に新しく作成するファイルは GPL-2.0-or-later のライセンスにする
* 既存のGPL2ファイルはファイルを編集した貢献者からライセンス変更の承諾を得て GPL-2.0-or-later に変更する
* 承諾を得るのが難しい GPL2 でライセンスされたファイルは削除する

#### ライセンス変更の賛否確認

GitHub issueにてJDimproved projectに参加・貢献した貢献者の方々へライセンス変更の賛否確認を行ないます。
確認のissueはこのRFCが承認された後に開きます。

確認すること
* これまで提供した修正(パッチやコミット)のライセンスを GPL-2.0-or-later に変更することについて承諾するか否か

#### ファイルの内容を移動、コピーするときの取り扱い

コピー元 | コピー先 | 可否
--- | --- | ---
GPL2 | GPL-2.0-or-later | :x: ライセンスがGPL2に変わるためコピーは避ける &#8251;
GPL-2.0-or-later | GPL2 | :heavy_check_mark: コピーしてよい

&#8251; ライセンス変更に承諾した貢献者が書いた修正であり既存の改変ではなく新しく追加したコードブロックであるならコピーしてもよい

#### GPL-2.0-or-later でライセンスされたファイルの識別

ファイルの冒頭にライセンスを識別するコメントを追加します。
```cpp
// SPDX-License-Identifier: GPL-2.0-or-later
```
コメントが書けないファイル形式であっても新しく作成されたファイルは GPL-2.0-or-later として扱います。

<https://spdx.org/licenses/GPL-2.0-or-later.html>


<a name="Examples"></a>
## Examples
_ユーザーが提案された機能をどのように使うのか例を書きます。_

READMEのライセンスを表示するセクションに GPL-2.0-or-later を導入することとライセンス変更の確認について書きます。

> ## ライセンス
> 
> JDim は GPLv2 の下で公開されています。
> [GNU General Public License, version 2][lisence]
> 
> (COMMIT-HASH) (YYYY-MM-DD) より後に取り込まれた修正(パッチやコミット)は GPL-2.0-or-later でライセンスされます。
>
> #### JDimproved projectに参加・貢献した皆様へお願い
> 既存のファイルのライセンスを GPL-2.0-or-later に変更するためファイルを編集した貢献者の皆様に確認を行っています。
> (ISSUE-NUMBER) でライセンス変更の賛否を表明していただけると幸いです。
 
[lisence]: https://github.com/JDimproved/JDim/blob/master/COPYING

CONTRIBUTING.md や pull request template を編集して
新しくファイルを作成するときはファイルの冒頭に GPL-2.0-or-later と示すコメントを追加するよう案内します。
また、 GPL-2.0-or-later のファイルに GPL2 の内容をコピーしないように案内します。

#### ファイルのライセンスを調べる
どのファイルがライセンス変更されたか確認するにはgrepコマンドなどでファイルを検索します。
```sh
git grep --files-with-matches 'SPDX-License-Identifier: GPL-2.0-or-later'
```

ファイルが作成された日時を調べるときはgit logコマンドなどでコミットログを見ます。
```sh
# --follow はファイル名の変更を追跡する
git log --follow src/main.cpp
```


<a name="Motivation"></a>
## Motivation
_提案が必要になった背景や動機を書きます。_

#### OpenSSL とのライセンス互換性
JDimは通信を暗号化(TLS)するライブラリとして [GnuTLS] と [OpenSSL] に対応しています。
OpenSSL のライセンスは GPL2 と互換性がないため OpenSSL を利用する実行ファイルの配布は制限されています。

<https://www.openssl.org/source/license.html>

OpenSSLのバージョン | ライセンス | GPL2との互換性 | GPL3との互換性
--- | --- | --- | ---
3.0 未満 | OpenSSL と SSLeay のデュアルライセンス | :x: なし | :x: なし
3.0 以上 | Apache v2.0 ライセンス | :x: なし | :heavy_check_mark: Apache2 → GPL3

OpenSSL の新しいバージョン(3.0)は Apache-2.0 にライセンスが変更されたため
[GPL3のソフトに含める][compat]ことができるようになりました。
このためJDimのライセンスを GPL2 or later または GPL3 に変更すると OpenSSL 3.0 とのライセンス互換性が解決できます。

[GnuTLS]: https://www.gnutls.org/
[OpenSSL]: https://www.openssl.org/
[compat]: https://www.apache.org/licenses/GPL-compatibility.html

#### OpenSSL 以外への影響
OpenSSL のライセンス問題は他の部分に影響する可能性があります。

* HTTP/2 による通信のサポート  
  人手や時間の問題から複雑な HTTP/2 プロトコルを自前で実装して保守していくのは現実的ではありません。
  サードパーティ製のHTTPライブラリを使う場合はHTTP通信の暗号化に使われるTLSライブラリのライセンスまで考慮した選択が必要です。

GitHub Discussions: <https://github.com/JDimproved/JDim/discussions/980>


<a name="Rationale"></a>
## Rationale
_Specificationに書かれた解決策を選んだ理由を書きます。_

派生元のJD projectで開発メンバーの方とお話しをしましたがJDのライセンス変更は難しい状況のようです。
<https://osdn.net/projects/jd4linux/ticket/45205>

#### GPL2ファイルの削除
GPL2 は GPL2 のソースファイルを改変して公開する場合は GPL2 で公開するように条件を課しています。
ライセンスを変更するにはファイルを編集した貢献者全員 (編集した部分が残っていなくても) から承諾を得る必要があります。
そのため貢献者に確認が取れない、あるいは賛成を得られなかったファイルは削除します。

#### パッチやコミットを対象にライセンス変更する
ライセンス変更に承諾した貢献者が書いた修正であり既存の改変ではなく新しく追加したコードブロックをコピー可能にするため
個々のパッチやコミットをライセンス変更する形にします。(ファイル内容ではなく修正の差分を利用する形)

#### ライセンス変更の賛否確認
JDimのREADMEには "パッチやファイルを取り込んだ場合、それらのコピーライトは「JDimproved project」に統一します。"
と書いてありますが、ライセンス変更について決まりがないため貢献者に賛否確認を行ないます。


<a name="Backwards"></a>
## Backwards Compatibility
_後方互換性への影響を書きます。_

GPL-2.0-or-later は GPL2(GPL-2.0-only) と互換性があるライセンスです。


<a name="Rejected"></a>
## Rejected Ideas
_採用しなかった他のアイデアと却下の理由を書きます。_

#### GPL-2.0-or-later 以外のライセンスを導入する
* GPL2 に OpenSSL 例外の条項を追加するのはオリジナルの GPL2 と互換性がなく混ぜて使うことができません。
* コピーレフトでないライセンスへの変更はオリジナルJDからライセンスの目的や意図が大きく変わってしまうため避けます。

#### ライセンスは現状維持で GPL2 から変更しない
JDimはサードパーティ製ライブラリの利用が不可欠であるため
コピーレフトを尊重した上で選択肢の幅を広げより良いソフトウェアにしたいと考えています。

#### ライセンス変更の作業を一挙に行う
取り組むための人手や時間が不足しているためファイルを少しずつ置き換えていく方法を取ります。


<a name="Issues"></a>
## Open Issues
_未解決の問題を書きます。_

* 達成の目処が立たない。2023年現在でもオリジナルJDのソースコードが大部分であり今のペースだとさらに10年続けても達成できない。

  2017年から2023年までの編集によってコードの割合が全体の20%ほどになった程度です。
  これは既存の部分の書き換えを含むため純粋な割合はもっと下がります。 ([git-of-theseus]を使ってグラフ生成)
  ![stack_plot](https://user-images.githubusercontent.com/15698961/257050601-abd47de4-7faf-4038-9da6-2264831ea08c.png)

[git-of-theseus]: https://github.com/erikbern/git-of-theseus
