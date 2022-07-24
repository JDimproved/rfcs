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

# Autotoolsのサポート終了
_ファイル冒頭にタイトルを書きます。タイトルにRFC番号を含める必要はありません。_

- [Abstract](#Abstract)
- [Specification](#Specification)
- [Motivation](#Motivation)
- [Rationale](#Rationale)
- [Backwards Compatibility](#Backwards)
- [Rejected Ideas](#Rejected)
- [Open Issues](#Issues)


<a name="Abstract"></a>
## Abstract
_文書の内容をまとめた概要を書きます。_

Autotools(configure)によるJDimのビルドをサポート終了するための手続きについて定めます。  
Autotoolsのスクリプトは廃止予定とマークされv0.10.0リリース後に対応を終了します。


<a name="Specification"></a>
## Specification
_機能の追加や変更を提案するときは仕様を書きます。_

Autotoolsのサポートをバージョン0.10.0のリリースをもって終了します。

ディストロのパッケージングに関して問題が報告されて解決が難しいときは作業の中断や変更の差し戻しを行います。

#### 廃止前のステップ
このRFCがマージされた後に実行します。

**v0.8.0の間**
- ドキュメントの更新その1  
  INSTALL、マニュアル、READMEにAutotoolsのサポートが廃止予定になったことを書き利用者に通知します。

**v0.9.0がリリースされた後**
- ドキュメントの更新その2  
  INSTALL、マニュアル、READMEにあるAutotoolsの例をMesonに置き換えます。
- configureスクリプトに警告を追加  
  `./configure` を実行したときに将来のバージョンで削除されることを通知します。

#### 廃止後のステップ
v0.10.0がリリースされた後に実行します。

- ドキュメントの更新その3  
  INSTALL、マニュアル、READMEやリリースノートにAutotoolsのサポートが廃止されたことを書き利用者に通知します。
- ./configureスクリプトの削除  
  - `configure.ac` や `Makefile.am` を削除します。

#### 予定表
日付 | バージョン | 状態
--- | --- | ---
2023-01 | v0.9.0 | Autotoolsのサポートを廃止予定にする
2023-07 | v0.10.0 | ドキュメントをMesonに書き換える
2024-01 | v0.11.0 | Autotoolsのサポートを削除する


<a name="Motivation"></a>
## Motivation
_提案が必要になった背景や動機を書きます。_

Meson構成ファイルの更新で安定性が向上したのでメンテナンスのハードルが高いAutotoolsをサポート終了してMesonに集中します。

#### メンテナンス
JD/JDimをビルドするツールとしてAutotoolsが使われてきましたが
スクリプトのメンテナンスには習熟が必要なため触りにくい部分となっています。

- スクリプトファイルは[autoconf]、[automake]を中心にmakeやシェルスクリプトなどが混ざっている
- シェルスクリプトに近い構文であり数値、文字列、配列の区別がゆるい
- ファイルの書き方を間違えたときエラーが分かりにくい・エラーとならない場合がある

[Meson]はAutotoolsの難しいところを変更してありメンテナンスがより容易になっています。

- 構成ファイルは主に一種類[^1]でCLIツールや別のスクリプト言語を使う箇所が少なくなっている
- AutotoolsよりC/C++言語に近い構文なのでC++経験者なら未経験でも構成や動作の検討がつきやすい
- 構成に使われる変数値は数値、文字列、配列などデータ型が明確に分かれており型が合わない操作はエラーになる
- Autotoolsと比べるとファイルの書き方を間違えたとき表示されるエラーが分かりやすい

[^1]: クロスコンパイルで追加の設定ファイルが必要

[autoconf]: https://www.gnu.org/software/autoconf/
[automake]: https://www.gnu.org/software/automake/automake.html
[Meson]: https://mesonbuild.com/

#### Mesonの動作環境
Mesonを動かすにはpython3と[ninja]が必要になります。
GTKのビルドは2017年にAutotoolsから[Mesonに移行][gnome-mail]しておりGTKが更新されている環境ではMesonも使えるはずです。
(ただしGTK3ではオプション)

2022年現在、JDimのMeson構成ファイルはバージョン0.49が必要で
[Debian buster]からディストロに入っているMesonを利用できるようになります。

##### Mesonのパッケージが利用できるディストロ/OSの一覧
<https://repology.org/project/meson/versions>

[ninja]: https://ninja-build.org/
[Ubuntu 18.04]: https://launchpad.net/ubuntu/+source/meson
[Debian buster]: https://packages.debian.org/source/oldstable/meson
[gnome-mail]: https://mail.gnome.org/archives/gtk-devel-list/2017-August/msg00028.html
[gtk-meson]: https://gitlab.gnome.org/GNOME/gtk/-/blob/gtk-3-24/gtk/meson.build


<a name="Rationale"></a>
## Rationale
_Specificationに書かれた解決策を選んだ理由を書きます。_

#### 変更の中断
パッケージ構築するとき外部サイトから追加ダウンロードを許可しないディストロで
Mesonが利用不能だった場合、Autotoolsを削除するとパッケージングができなくなります。
そのときは状況が変わるまでAutotoolsを維持します。

#### 最終的なAutotoolsのサポート削除がバージョン0.11.0
Mesonへ移行に余裕を持たせるため１バージョンだけ削除を延ばします。
また、バージョン0.10.0では動作環境の更新を予定していないため、なるべくインパクトのある変更を避けます。


<a name="Backwards"></a>
## Backwards Compatibility
_後方互換性への影響を書きます。_

v0.10.0リリース後のバージョンからAutotoolsを使ったビルドができなくなります。


<a name="Rejected"></a>
## Rejected Ideas
_採用しなかった他のアイデアと却下の理由を書きます。_

#### Autotoolsのサポートを続ける
上記のとおりメンテナンスが簡単でないため構成の調整や変更がやりにくい状態が続きます。

#### Autotoolsを廃止予定にするが削除せず残しておく
サポートを続ける場合と同様に構成の調整や変更が問題になります。

#### 他のビルドツールを採用する
ディストロのパッケージングシステムがサポートしてないツールはメインにできません。
Java製ツールなどツール自体が大きいものはインストールのハードルが高くなります。

C++をサポートしUnix系OSで利用できるツールとしては[CMake]があります。
CMakeは広く使われていますが、Mesonと比べるとメンテナンスやりにくいです。
(ファイルの構文にAutotoolsで挙げた点と同様の問題がある)

[CMake]: https://cmake.org


<a name="Issues"></a>
## Open Issues
_未解決の問題を書きます。_

#### Mesonの動作に必要なpython3が利用できない環境ではどうするか？
python3がない環境ではビルドできません。
C99で書かれたmeson互換のツール([muon])があるようですが一部を除き拡張的な機能が未実装であるようです。

[muon]: https://sr.ht/~lattis/muon/
