# リリースサイクル

- [Abstract](#Abstract)
- [Specification](#Specification)
- [Examples](#Examples)
- [Motivation](#Motivation)
- [Rationale](#Rationale)
- [Rejected Ideas](#Rejected)
- [Open Issues](#Issues)


<a name="Abstract"></a>
## Abstract
JDimの新しいバージョンをリリースするための開発サイクルについて定めます。
リリースは後述するLinuxディストリビューション（ディストロ）のリリースに合わせて約6ヶ月ごとに新しいバージョンを出します。

NOTE: リリースの具体的な作業やJDimのバージョン間の互換性についてはこのRFCでは定めません。


<a name="Specification"></a>
## Specification
JDimのリリースは以下のディストロのリリース前の期間を目処に行います。

- [Debian](https://www.debian.org/)
- [Fedora](https://getfedora.org/)
- [Ubuntu](https://ubuntu.com/)

この内FedoraとUbuntuは春と秋の6ヶ月ごとにリリースされていますのでJDimは約6ヶ月ごとにリリースされる計画になります。

#### リリース日の決定方法

1. ディストロのリリース計画を参照しソフトウェアパッケージの更新が凍結されるフリーズ日をリストする
2. リリース計画を決めるissueをJDimで開く
3. ディストロのフリーズ日を参考に以下の表に当てはめてスケジュールを決める &#x203B;1

   | 課題                         | 次の課題までの期間 | ディストロのフリーズから逆算した週数
   | ---                          | ---                | ---
   | リリース計画の決定           | 4週間以上          | 11週間前〜
   | JDimの機能フリーズ &#x203B;2 | 2週間以上          | 7週間前〜
   | JDimのリリース               | 5週間以上          | 5週間前〜
   | ディストロのフリーズ         | 0                  | 0

4. 決定した計画に従ってリリース作業を行う

- &#x203B;1 -- スケジュールはディストロとの調整により変わることがあります。
- &#x203B;2 -- 機能フリーズからリリースまでの期間は機能の追加・削除を停止します。（廃止予定の指定・解除を除く）


<a name="Examples"></a>
## Examples
詳細は[バージョン0.3.0のリリース計画](https://github.com/JDimproved/JDim/issues/146)を参照してください。

| 課題                 | 日付       | 次の課題までの期間
| ---                  | ---        | ---
| リリース計画の決定   | 2019-11-30 | 4週間
| JDimの機能フリーズ   | 2019-12-28 | 3週間
| JDimのリリース       | 2020-01-18 | 約6週間
| ディストロのフリーズ | 2020-02-27 | 0


<a name="Motivation"></a>
## Motivation
リリースに関する方針が公開されていなかったため現状の慣習を文書化します。


<a name="Rationale"></a>
## Rationale
参考にする[Debian][deb]、[Fedora][fed]、[Ubuntu][ubu]はソフトウェアパッケージにJDimが入っていますので
これらのディストロになるべく新しいバージョンが入るようにします。

また、FedoraやUbuntuが採用しているカレンダーや期間に基づいたリリースを参考にすることでリリース間隔を安定化します。

カレンダーや期間に基づいたリリースにする理由は

- 開発者も利用者もリリーススケジュールが予想しやすい
- 機能追加を区切りにすると追加されないor安定しない機能があった場合リリースが遅れる

機能フリーズ期間を導入する理由は

- 動作の確認やリリース作業を行う時間が必要
- リリース直前に入れた機能に不具合があった場合リリースまで見逃したり修正が間に合わない


<a name="Rejected"></a>
## Rejected Ideas

#### リリース間隔を6ヶ月より短くする
現状の開発速度では6ヶ月より短い期間になると変化が乏しくなりリリース作業が増えるため人手が厳しくなります。

#### 参考にするディストロを追加、または取り替える
ディストロを増やすとリリースが増える可能性があり上述の理由により開発速度に影響があります。
加えてDebianとUbuntuは長期サポート版(LTS)があるためツールチェーンやライブラリの要件の参考に適しています。
（Fedoraは派生にCentOSがある）


<a name="Issues"></a>
## Open Issues
- スケジュールの基準として参照しているディストロがカレンダーベースのリリースを止めたらどうするか？
- FedoraとUbuntuのリリースは同時期（春と秋）だがもし合わなくなったらどうするか？
- 現状はカレンダーに基づいたバージョン番号（[CalVar]）を使用していないが採用するか？


[deb]: https://tracker.debian.org/pkg/jdim
[ubu]: https://launchpad.net/ubuntu/+source/jdim
[fed]: https://src.fedoraproject.org/rpms/jd
[CalVar]: https://calver.org/ "Calendar Versioning"
