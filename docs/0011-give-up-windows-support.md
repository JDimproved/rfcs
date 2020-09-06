# Windows(MinGW)版のサポート終了

- [Abstract](#Abstract)
- [Specification](#Specification)
- [Motivation](#Motivation)
- [Rationale](#Rationale)
- [Backwards Compatibility](#Backwards)
- [Rejected Ideas](#Rejected)


<a name="Abstract"></a>
## Abstract
JDimのWindows(MinGW)版をサポート終了するための手続きについて定めます。  
Windows対応のソースコードはメンテナンスされていないため削除します。


<a name="Specification"></a>
## Specification
このRFCが承認された後、Windows(MinGW)対応のソースコードを削除します。
また、ドキュメントも更新します。


<a name="Motivation"></a>
## Motivation
Windows版のサポートを終了してメンテナンス性を改善します。

#### 動作環境の更新
- JDimは[動作環境が更新][rfc6]されていますがWindows対応のソースコードは修正されていません。

#### メンテナンスの状態
- Windows版はリポジトリの継続的インテグレーションで検証されておらずビルドや起動が可能なのか不明です。
- ソースコードのうちWindows対応のため条件コンパイルで分かれている部分は100箇所近くあり機能追加・削除が困難です。

#### 利用者の数
- JDim v0.1.0リリース以降でWindows版利用者からの[動作やエラーの報告はありませんでした][1]。


<a name="Rationale"></a>
## Rationale

#### コードの削除
ビルド・実行されていない対応コードを削除してメンテナンス性を改善します。
利用者報告がないためリリースを待たずに削除しても差し支えないと判断しました。


<a name="Backwards"></a>
## Backwards Compatibility
対応のソースコードが削除されるとWindows版のビルドができなくなります。


<a name="Rejected"></a>
## Rejected Ideas
#### Windows版のメンテナンス作業を行ってサポートを維持する
- メンテナンスに必要な環境や時間、人手が増えるため現状では開発・保守が厳しくなります。

#### Windows版を別のブランチに分けてメンテナンスする
- 上記と同じく開発・保守が厳しくなります。

#### Windows対応ソースコードは削除せずそのまま放置する
- [Motivation](#Motivation)で挙げたとおりテスト・動作確認されていないソースコードは周辺の更新を困難にします。


[rfc6]: https://github.com/JDimproved/rfcs/tree/master/docs/0006-platform-support.md
[1]: https://mao.5ch.net/test/read.cgi/linux/1540656394/614 "JDで最後にあった報告は2019-02-12"
