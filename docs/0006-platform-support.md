# プラットフォームのサポート

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
JDim最新版がビルド・動作可能なプラットフォーム（動作環境）についてサポートの基準を定めます。
動作環境は約5年前までにリリースされたLinuxディストリビューション（ディストロ）を基準にします。

NOTE: ツールチェーンやライブラリの具体的な要件についてはこのRFCでは定めません。


<a name="Specification"></a>
## Specification

現在から約5年前までにリリースされたディストロを基準にJDim最新版（masterブランチ）
のビルドができるようにメンテナンスします。

#### ディストロのリリースとサポートの基本方針

| リリースからの年数 | JDim最新版のビルド
| ---                | ---
| 1〜4年目           | :heavy_check_mark: サポートする
| 5年目              | :warning: 時期を決めてサポート終了する
| 6年目以降          | :x: サポートしない

#### サポート状況の通知

サポート状況の目安として以下のディストロからサポート終了が近いバージョンをドキュメントに表示して利用者に通知します。

- [Debian](https://www.debian.org/) ([サポート期間](https://wiki.debian.org/LTS))
- [Ubuntu LTS](https://ubuntu.com/) ([サポート期間](https://wiki.ubuntu.com/Releases))

#### 動作環境の更新

- 自動的には更新せず[JDim]のissueでメンテナーと話し合って決定する。
- 動作環境の変更はJDimリリースのタイミングで行う。
- 少なくとも[JDimの機能フリーズ期間][0005-spec]に入る前には変更の計画を決定するのが望ましい。
- ツールチェーンやライブラリに非互換があり基本方針通りにサポートできないときは必要に応じて補足説明を付ける。
- 動作環境変更の計画を決定したらREADMEなどドキュメントを編集してサポート状況を更新する。


<a name="Examples"></a>
## Examples

利用者へサポート状況の通知例

> ##### サポートの最新情報
> gtkmmのバージョンが2.24未満のプラットフォームはサポートを終了しました。
> CentOS 7(2014年)より前にリリースされたディストリビューションを利用されている場合は更新をお願いいたします。


<a name="Motivation"></a>
## Motivation
JDimが利用するC++やGTKは更新で互換性のない変更が入る可能性があり
古い環境をサポートし続けるとメンテナンスの負担が増えるためある程度の時間で区切ります。


<a name="Rationale"></a>
## Rationale
2020年現在の慣行では過去5年の間にリリースされたディストロでmasterブランチのビルドが可能であるため、
現状を維持できるように年数を設定します。

サポート状況の通知にDebian、Ubuntu LTSを利用する理由は

- 単に年だけ書くより把握しやすくする
- 5年間のセキュリティサポートがありサポートの基準に合う
- 2年に1回ずつ交互にリリースされているため更新が容易


<a name="Backwards"></a>
## Backwards Compatibility
6年以上前にリリースされたディストロは基本的にサポートから外れます。


<a name="Rejected"></a>
## Rejected Ideas

#### サポートの基準を5年より長くする
5年以上サポートしているディストロは少なくテスト環境の消失や最新環境との違いでメンテナンスが難しくなります。

#### サポートの基準を5年より短くする
現在は5年くらい前のディストロでJDim最新版がビルドできるため長期サポート版ディストロのサポートを打ち切ることになります。

#### JDimのリリースを最新版(masterブランチ)と長期サポート版(LTSブランチ)に分ける
ブランチが増えるとメンテナンスに必要な時間や人員が増えるため現状では開発・保守が厳しくなります。

#### サポート状況の表示に利用するディストロを追加、または取り替える
5年以上のサポート期間があるディストロは[CentOS][cent]、[Red Hat Enterprise Linux][red]や
[SUSE Linux Enterprise Server][suse]などありますがサーバー向けや有償サポートであり参考にし難いです。

Debian、Ubuntuは派生ディストロが多くカバーできる範囲が広いです。


<a name="Issues"></a>
## Open Issues

- サポート状況の参照にするディストロが長期サポート版を止めたらどうするか？
- ディストロのリリース周期がずれてサポート状況の通知に表示するバージョンを選べなくなったらどうするか？


[JDim]: https://github.com/JDimproved/JDim
[0005-spec]: https://github.com/JDimproved/rfcs/blob/master/docs/0005-release-cycle.md#Specification
[cent]: https://www.centos.org
[red]: https://www.redhat.com/ja
[suse]: https://www.suse.com/ja-jp/
