class: center, middle

<style>
.two-column-left{
  float: left;
  width: 40%;
  text-align: left;
}
.two-column-right{
  float: right;
  width: 55%;
  text-align: left;
}
</style>

<style>
.column-left{
  float: left;
  width: 50%;
  text-align: left;
}
.column-right{
  float: right;
  width: 50%;
  text-align: left;
}
</style>

# 運用と保守の狭間で

2020/04/20 @msfukui

---

# 自己紹介

<img src="slides/msfukui.jpg" alt="ふくい（ま）" width="15%">

* 名前: ふくい（ま）

* 家族: 4児の父（うち三人は先週末から疎開中）←僕が耐えられなかったので..

* 好きな言語: Ruby, TypeScript, Golang, OCaml

* 最近思わず二度見したパワーワード:

  ```
  ＿人人人人人人人人人人人人人人人人人人人人人人人人人人人＿
  ＞　エディタの選定：OS添付のエディタ（メモ帳）を[推奨]　＜
  ￣Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y￣
  ```

---

# 三行で

* 運用と保守のことなんもわからんので調べてみた

* クラウドになっても運用や保守の本質はなくならなさそう

* 運用保守の業務の多くは今後、開発構築の業務に飲み込まれそう

<img src="slides/unyo_cover.jpg" alt="運用でカバー" width="55%">

> https://next.rikunabi.com/journal/20180524_t12_iq/

---

# 4月から仕事が変わりました

4/1 にとりあえず自社に出社してみたところ..

* 上司:「とある共通基盤の**システム運用**と監視業務を請け負っていて、」

* 上司: 「新しく**インフラ保守**の全体管理も支援することになったから、」

* 上司:「セットアップ終わったら、明日から PC 持ってｘｘビルに常駐して。」

* ふくい（ま）:「えっ、あ、は、はい。。」

## システム運用? インフラ保守?

なんもわからん..。

---

# 運用と保守の違い

* 開発とか構築とかとも区別せずにやっているとあまり考えたことがない

* （めんどい、全部一緒でいいんじゃないの?）

とりあえずえらい人の作られた定義などを眺めてみる

## JIS X 0170:2020 システムライフサイクルプロセス

c.f. https://kikakurui.com/x0/X0170-2020-01.html ※ちょっと微妙なサイトですが..

* ISO/IEC/IEEE 15288 の日本版規格

  https://www.iso.org/standard/63711.html

* システムの要求から廃棄されるまでの全体のライフサイクルのプロセスを規定した標準規格

---

### 運用（プロセス） - operation

* 目的: システムを利用してサービスを提供する。

* やること:

  * 要員がシステムを運用操作するための要求事項を確立して，

  * 要員をシステムの運用操作を担当するよう割り当て，

  * サービス及び運用操作者によって運用されるシステムの遂行能力・性能・運用時の実績を監視する。

  * サービスを持続させるために，運用操作上の不具合を，

  * 合意，利害関係者の要求事項，及び組織面の制約に関して識別し分析する。

---

### 運用（プロセス） - operation

問い合わせを受け付けるコールセンターのお姉さんが思い浮かぶ。

<img src="slides/job_call_center.png" alt="コールセンター" width="30%">

---

###  保守（プロセス） - maintenance

* 目的: サービスを提供するシステムの能力を維持する。

* やること:

  * サービスを提供するシステムの能力を監視し，

  * 分析のためにインシデントを記録し，

  * 是正処置，適応処置，完全化処置及び予防処置の作業を実施し，

  * 修復された能力を確認する。

---

###  保守（プロセス） - maintenance

橋とか高速道路とかプリンターを点検・補修・維持するおじさんが思い浮かぶ。

（僕の業務はこっちらしい。）

<img src="slides/job_kukakusen_kouji.png" alt="区画線工事" width="30%">

---

## 役割を分けることに意味はありそう

* 効率性

* スケーラビリティ

* 人材

## なぜ一緒くたにされることが多いのか?

システムのライフサイクルフェーズの区分けから?

* 開発・構築(Dev) vs 運用・保守(Ops)

* 被っているところもありそう

  * システムの能力を「監視」

---

# パブリッククラウドでの運用と保守

* 提供するサービス毎に責任分界点は異なる

  * 責任共有モデル、共同責任モデル

* クラウドベンダーは境界線で「手段」（API、画面）を提供する

* いつどう設定・適用するかは利用者の責任

* **オンプレミスの場合と考え方は変わらない**

* 異なるところ

  * スケールする、確立された、効率的な手段が提供されることを期待できる

  * マネージドなサービスを利用することで責任分界点を押し上げることができる

      分野によっては時間と人的リソースを買える

---

## AWS: 責任共有モデル

https://aws.amazon.com/jp/compliance/shared-responsibility-model/

<img src="slides/Shared_Responsibility_Model_V2_JP.jpeg" alt="AWS Shared responsibility model" width="75%">

---

## Azure: 共同責任モデル

https://docs.microsoft.com/ja-jp/azure/security/fundamentals/shared-responsibility

<img src="slides/shared-responsibility.png" alt="Azure Shared responsibility model" width="75%">

---

## 例えば OS パッチを適用する保守の場合

1. インシデントオープン

1. サービス影響範囲を調査

1. ステークホルダーとのスケジュール調整、実施確定

1. 構成管理の変更を準備

1. 手順書作成・レビュー・承認

1. 作業・正常性確認実施

1. 構成管理の変更を確定

1. インシデントクローズ

4 〜 7 は効率化できる、かもしれない..

---

# 運用と保守の今後

* ところてんさんの資料

  DXとかDevOpsとかのなんかいい感じのやつ

  https://www.slideshare.net/TokorotenNakayama/dxdevopstechlive

  * ソフトウェアが全てを飲み込む

  * DevOps の本質: Ops の仕事を Dev がプログラミングで奪い取る

* もっと低コストで、もっと少人数で、予算は限界まで減らされ続け、人は増えない

  * 仕事をスケールできないと死ぬ

* やれることがいっぱいありそう、変われる余地がたくさんありそう！

  * Dev になれる人を見つけて一緒に Ops から Dev に越境したい！（逆張り）

  * まずはエディタを変えるところから

---
class: center, middle

# 「越境」

普段の業務を超える、会社の枠を超える、エンジニアの枠を超える。

<img src="slides/three-border.jpg" alt="三県境" width="50%">

---
class: center, middle

# Enjoy, DevOps!

---

# 参考

* ITスキル標準V3

  https://www.ipa.go.jp/jinzai/itss/download_V3_2011.html

  「カスタマーサービス」「ITサービスマネジメント」の説明や区分が参考になる

* システム・リファリンスマニュアル（SRM) （2004年）

  https://www.ipa.go.jp/about/jigyoseika/04fy-pro/chosa03.html

  第4章 保守・運用

  https://www.ipa.go.jp/about/jigyoseika/04fy-pro/chosa/srm/srm4.pdf

  古い資料だけど指標とか分類がシンプルで参考になる

---

* ITIL

  https://ja.wikipedia.org/wiki/Information_Technology_Infrastructure_Library

  https://www.idearu.info/article/system/itil-4-overview

  「ITサービスマネジメントにおけるベストプラクティス」

  2019年に v4 が発行されたらしい（まだ未見）

---

## システムの規模と範囲とサービスレベル

* サーバインフラは一システム当たり数百台×7～8システム

* オンプレ（複数DC）+複数のパブリッククラウドの組み合わせ

* Windows, Linux混在

* PostgreSQL、SQLServer、OracleDB、クラウド固有DB

* 複数のミドルウェア製品（統制・アップグレード・ライセンス管理、クラスタリング、監視、ウイルス対策、多層防御、証跡管理など）

* 複数のアプライアンス製品（ロードバランサ、NASなど）

* 複数の外部連携先（お客さま拠点、配送業者、決済、機器など）

* ミッションクリティカル、自主・受託環境混在

* 24H, 365D の運用・保守

---

## 他の視点

* アプリケーションとインフラ

* マネジメントとオペレーション

* SRE（サイト・リライアビリティ・エンジニアリング）

* 依存関係の管理

* セキュリティ

* プロジェクトへの参画タイミング
