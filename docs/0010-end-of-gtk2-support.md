# GTK2版のサポート終了

- [Abstract](#Abstract)
- [Specification](#Specification)
- [Motivation](#Motivation)
- [Rationale](#Rationale)
- [Backwards Compatibility](#Backwards)
- [Rejected Ideas](#Rejected)


<a name="Abstract"></a>
## Abstract
JDimのGTK2版をサポート終了するための手続きについて定めます。  
GTK2版は廃止予定とマークされ0.4.0リリース後に対応を終了します。


<a name="Specification"></a>
## Specification
GTK2版のサポートをバージョン0.4.0のリリースをもって廃止します。

#### 廃止前のステップ
このRFCがマージされた後に実行します。

- ドキュメントの更新  
  INSTALL、マニュアル、READMEにGTK2版が廃止予定になったことを書き利用者に通知します。
- configureスクリプトに警告を追加  
  `./configure --with-gtkmm3=no` を実行したときに将来のバージョンで削除されることを通知します。

#### 廃止後のステップ
0.4.0がリリースされた後に実行します。

- ドキュメントの更新  
  INSTALL、マニュアル、READMEやリリースノートにGTK2版が廃止されたことを書き利用者に通知します。
- ./configureスクリプトの変更 part1  
  - `./configure --with-gtkmm3=no` を実行するとエラーを出して停止するように修正します。
  - `./configure --with-gtkmm3` を実行したときにオプションが不要になったことを通知します。
- GTK2対応のソースコードを削除  
  configureスクリプトの変更 part1の後にGTK2を使うソースコードを削除します。
  さらに互換性のために使用している廃止予定のAPIを更新します。
- ./configureスクリプトの変更 part2  
  0.5.0リリース後にconfigureオプション `--with-gtkmm3` を削除します。


<a name="Motivation"></a>
## Motivation

GTK3版の更新で安定性が向上したことやGTK2版の維持がメンテナンスの問題になっているため
GTK2版をサポート終了してGTK3版に集中します。

#### GTK3版の更新
- GTK3版は安定性が向上しバージョン0.3.0のリリース後から[デフォルトのオプション][pr172]になりました。
- ディストロのパッケージにGTK3版が採用され普及が進んでいます。（[Debian], [Fedora], [Ubuntu]）
- タッチスクリーン操作や書き込みビューの単語選択など[GTK3版にだけ追加された機能][gtk3feature]があります。

#### メンテナンス
- GTK2、GTK3で互換性のない箇所は条件コンパイルで分かれておりソースコードの可読性が悪くなっています。（100箇所以上）
- 両バージョンで動作確認するのは時間がかかります。
- 機能が異なるとメンテナンスが困難になるためGTK3から導入された機能を活用できない状態です。

他のプロジェクトでの例: [inkscape][] (Notice of removal of GTK+ 2 support - Inkscape Wiki)

<a name="Rationale"></a>
## Rationale

#### 変更の時期
掲示板でGTK2版利用の報告が減少していることから次期バージョン(0.4.0)から変更しても差し支えないと判断しました。

#### configureオプションの変更
./configureは存在しないオプションを指定しても実行が止まらないため明示的にエラーを出すことで利用者に知らせます。


<a name="Backwards"></a>
## Backwards Compatibility

バージョン0.4.0がリリースされた後にGTK2版が利用できなくなります。


<a name="Rejected"></a>
## Rejected Ideas

#### ブランチまたはリポジトリをGTK2版とGTK3版に分けてメンテナンスする
現状では時間や人員が不足しているため開発・保守が厳しくなります。

#### 変更の時期を遅らせてGTK2版のサポートを延ばす

[Motivation](#Motivation)の通り2つのバージョンの維持はデメリットがあります。

また、どんなに長くてもGNOME公式がGTK2のメンテナンスを終了して
ディストロのパッケージからGTK2ライブラリが削除される段階でGTK2版を終了します。

GTK4に対応する場合はGTK2サポートの維持は[不可能][migrate]と考えられます。


[pr172]: https://github.com/JDimproved/JDim/pull/172 "Set gtkmm3 as default for configure script"
[Debian]: https://packages.debian.org/unstable/source/jdim
[Fedora]: https://src.fedoraproject.org/rpms/jd
[Ubuntu]: https://packages.ubuntu.com/source/focal/jdim
[gtk3feature]: https://jdimproved.github.io/JDim/start/#gtk3
[inkscape]: https://wiki.inkscape.org/wiki/index.php?title=Notice_of_removal_of_GTK%2B_2_support
[migrate]: https://developer.gnome.org/gtk4/3.98/gtk-migrating-2-to-4.html
