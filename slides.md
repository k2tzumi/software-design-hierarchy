---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: 設計原則、アーキテクチャパターン、アーキテクチャスタイルの違いって何？いつどう向き合ったらいいの？を考えてみる
highlighter: shiki
lineNumbers: false
info: |
  PHPカンファレンス名古屋2025
  https://phpcon.nagoya/2025/
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
addons:
  - '@katzumi/slidev-addon-qrcode'
  - slidev-addon-components
  - slidev-addon-rabbit
---

# 設計原則、アーキテクチャパターン、アーキテクチャスタイルの違いって何？いつどう向き合ったらいいの？を考えてみる

PHP カンファレンス名古屋 2025　Feb 22, 2025.  
v0.0.2  
@katzumi(かつみ)

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/k2tzumi/software-design-hierarchy" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
layout: two-cols-header
---

# 自己紹介

katzumi（かつみ）と申します。

「障害のない社会をつくる」をビジョンに掲げている「LITALICO」という会社に所属しています
<a href="https://litalico.co.jp/">
<img src="https://litalico.co.jp/ogp.png" class="w-40" />
</a>

以下のアカウントで活動しています。

::left::

<div class="float-left">
<img src="https://pbs.twimg.com/profile_images/1768978237210935296/idy9J4l6_400x400.jpg" class="rounded-full w-40 mr"/>  
<simple-icons-x /> <a href="https://twitter.com/katzchum">katzchum</a></div>  
<QRCode :width="180" :height="180" value="https://twitter.com/katzchum" color="4329B9" image="Logo_of_X.svg" />

::right::

<img src="https://avatars.githubusercontent.com/u/1182787?v=4" class="rounded-full w-40 mr-12"/>

<logos-github-octocat /> [k2tzumi](https://github.com/k2tzumi)  
<simple-icons-zenn /> [katzumi](https://zenn.dev/katzumi)  

<br />

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
layout: two-cols-header
transition: fade-out
---


# お願い

写真撮影、SNS での実況について

登壇者の励みになるので是非ともご意見やご感想など、フィードバック頂けると助かります mm  
あとでスライドを公開します

::left::

<Transform :scale="2.5">
　　　🙆‍♀📷<ph-projector-screen-chart-light /><br />
　　　🙅‍♂📹💸<br />
　　　🙅📸👨‍👦‍👦<br />
</Transform>

::right::

<br />
<Transform :scale="2">
<fa6-brands-square-x-twitter />
</Transform>
<br />
<a href="https://x.com/search?q=%23phpcon_nagoya%20%23q&f=live">#phpcon_nagoya #s</a>


<!-- 本セッションでは、撮影やSNS拡散を歓迎しています。ご自由に写真を撮影して、XなどのSNSでシェアしてください。 　　
ただし、以下の点にご注意ください。　　

著作権などの法的な問題を避けるために、スライドや登壇者の写真や動画を無断で商用利用しないでください。　　
他の参加者のプライバシーや迷惑にならないように、撮影や投稿する際には配慮してください。　　
SNSでシェアする際には、ハッシュタグ「#phpcon_nagoya #s」をつけてください。　　
これにより、本セッションの関連情報を簡単に検索できるようになります。 -->

---
layout: default
transition: slide-up
---

# 開発者が直面する「設計に関する情報過多」
この Post を見て「それな」と思ったのが、本セッションをしようと思い立ったきっかけになっています

<Tweet id="1836904526269514233" />

---
layout: two-cols-header
transition: fade-out
---

# 今日お話すること・話さないこと
狙いは「設計概念を体系的に理解し、個々のパターンを把握するための助けとする」です

::left::

# 🚫セッションでは扱わないこと

- 個々の設計パターンの詳細な解説
- 具体的な実装方法やコード例の紹介
- 特定のアーキテクチャの採用判断基準

<div class="speech-bubble">
個別の設計パターンやアーキテクチャの詳細は、巻末の参考資料参照📚
</div>

::right::

# ✨セッションで得られること

- 設計に関する概念を体系的に理解する視点
- 各設計概念の位置づけと相互の関係性
- 設計概念の発展背景と解決してきた課題の理解

---

# 見慣れた風景
設計に関する用語が飛び交う日々...

- "このプロジェクトは Clean Architecture で..."
- "ここは ServiceLayer パターンを使って..."
- "SOLID の原則に従って設計しましょう"
- "マイクロサービスアーキテクチャに移行して..."

ドキュメントやブログで目にする  
アーキテクチャやパターンの数々

---
transition: fade
---

# 開発者の本音
分かった気になっているけど...

- 具体的に何をすればいいの？
- この規模のプロジェクトに必要？
- いつ何を考えればいいの？  
  - 設計の検討は早すぎ？遅すぎ？
  - どの段階で決めるべき？
- 既存のコードにどう適用する？
- トレードオフは何だろう？

<br />
<v-click>

<div class="speech-bubble">
知識はあるのに、実践での判断に迷う
</div>

</v-click>

---
layout: fact
transition: fade
---

# ぜんぜんわからない 🤔

---
layout: fact
---

# 俺達は雰囲気で（ry

---

# 「雰囲気」の真意
「雰囲気で設計」の現実

* ソフトウェア開発に正解はない
  - 要件は常に変化する
  - チームごとに異なる制約がある
  - ビジネスの不確実性と向き合う

* 時には直感や経験に基づく判断も必要
  - 完璧な情報収集は現実的でない
  - スピードと質のバランス
  - チームの力量と成長

---
transition: slide-up
---

# 基礎となる原則を理解する
なぜ体系的な理解が必要なのか？

* 個別に学習・実践するには難易度が高すぎる
  * 新しい設計手法や考え方を次々と学ぶが、実践する機会がない
  * 表面的な理解に留まり、本質的な価値が掴めていない
  * 理想的な設計パターンやアーキテクチャの例を見ても、既存のプロジェクトにどう適用するか分からない
  * 様々な設計手法の中から、どれを選択すべきか判断できない
  * 各設計手法が生まれた背景や解決しようとした問題の理解が浅い
* 概念は互いに関連しており、体系的に理解することで、より効果的に活用することができる
* 概念の適用範囲や限界を理解し、状況に応じて適切な選択を行う為

<br />
<v-click>

<div class="speech-bubble">
近道はない
</div>

</v-click>


---
layout: center
---

# ＿人人人人人＿
# ＞　救世主　＜
# ￣Y^Y^Y^Y^Y^￣

---
layout: image-left
image: https://m.media-amazon.com/images/I/81Dt6RdccgL._SL1500_.jpg
---

# [「TECHNICAL MASTER はじめてのPHP エンジニア入門編」](https://www.shuwasystem.co.jp/book/9784798073224.html)
2024 年 12 月発刊！

豪華執筆陣！

---

# 「[TECHNICAL MASTER はじめてのPHP エンジニア入門編](https://www.shuwasystem.co.jp/book/9784798073224.html)」のおすすめ章
本セッションとも関連が高くて気に入るはずです

Chapter09: 設計原則とパターン

<blockquote>
<p>この章では、ソフトウェア開発における設計原則の重要性とアーキテクチャパターンの具体的な適用方法について詳しく解説します。</p>
<p>まず、アーキテクチャの定義とその必要性を説明し、SOLID原則を通じて設計の基本概念を理解します。その後、さまざまなアーキテクチャパターン（MVC、 レイヤードアーキテクチャ、クリーンアーキテクチャ、ヘキサゴナルアーキテクチャ）を紹介します。</p>
<p>また、設計パターンとアンチパターンをとりあげ、実際の開発における適用例や回避すべき設計の落とし穴についても解説します。</p>
</blockquote>

---
layout: center
---

# 超絶オススメなので是非！
きちんと学びたい＝学び直しにも

---
layout: image-right
image: section2.png
class: mt-45
backgroundSize: 20em 60%
transition: slide-up
---

# 設計概念の階層構造

---

# 設計に関する用語の3つのカテゴリ
数多の用語がどういうカテゴリになるのか？

* 〇〇の原則・法則  
SOLID, KISS, YAGNI, DRY, コマンドクエリ分離原則(CQS) , デメテルの法則（最小知識の原則）,驚き最小の原則 ^[UNIX哲学 "[Basics of the Unix Philosophy](http://www.catb.org/esr/writings/taoup/html/ch01s06.html)" の基本原則の一つ]  
→　設計の原則
* 〇〇パターン  
MVC, ActiveRecord, Value Object, Server Session State, Domain Model, CQRS  
→　アーキテクチャパターン
* 〇〇アーキテクチャ  
Layered, Clean, Hexagonal, Event Driven, Pipeline, Service Oriented  
→　アーキテクチャスタイル

---

# 設計原則
SOLID, DRY 等

- 設計における普遍的な指針
- 個々の判断の基準となる考え方
- 文脈に依存しない基礎的なルール

<br />
<v-click>

<div class="speech-bubble">
最も具象的で個々のクラスやメソッドレベルの直接的な設計指針となる
</div>

</v-click>

---

# アーキテクチャパターン
MVC, ActiveRecord 等

- 特定の問題に対する定型的な解決策
- 複数の原則を組み合わせた実践的な手法
- 文脈に応じて選択・適用する

<br />
<v-click>

<div class="speech-bubble">
抽象度が中程度なモジュールやコンポーネントレベルの設計パターン
</div>

</v-click>

---

# デザインパターンとの違い
パターンにも色々ある

| 項目                   | デザインパターン（GoF）         | アーキテクチャパターン          |
|----------------------|------------------------------|------------------------------|
| 設計レベル             | クラス/オブジェクトの設計レベル | システム構造レベル             |
| パターン数             | 23個のパターンで完結           | POSA ^[[Pattern-Oriented Software Architecture](https://www.amazon.co.jp/Pattern-Oriented-Software-Architecture-System-Patterns/dp/0471958697)]、PoEAA ^[[Patterns of Enterprise Application Architecture](https://www.amazon.co.jp/-/en/Martin-Fowler/dp/0321127420)]、EIPで体系化 ^[[Enterprise Integration Patterns: Designing, Building, and Deploying Messaging Solutions](https://www.amazon.co.jp/Enterprise-Integration-Patterns-Designing-Addison-Wesley/dp/0321200683)]           |
| 適用範囲               | 言語非依存の解決策             | エンタープライズアプリケーション特有 |

---

# アーキテクチャスタイル
Layered, Event-Driven, Microservices 等

- システム全体の構造を定義する設計思想
- 複数のパターンを包含する包括的な方針
- ビジネス要件と技術要件を橋渡しする

<br />
<v-click>

<div class="speech-bubble">
最も抽象度が高く、システム全体の構造を決定する
</div>

</v-click>

---
transition: fade
---

# 設計に関する3つの概念カテゴリ比較
抽象度が低→高、影響度も小→大となる

| 項目                  | 適用範囲                      | 抽象度                     | 決定の影響           |
|----------------------|------------------------------|---------------------------|----------------------|
| 設計原則              | メソッド/クラスレベルがメイン          | 具象的（直接的な指針）      | 局所的な影響          |
| アーキテクチャパターン | モジュール/コンポーネントレベル | 中間（再利用可能な解決策）  | 中規模な影響          |
| アーキテクチャスタイル | システム/アプリケーションレベル | 抽象的（全体的な方針）      | 全体的な影響          |

---

# 抽象度レベルピラミッド

<img src="./architecture_pyramid_diagram.svg" class="h-85" />

<v-click>

<div class="speech-bubble">
抽象度の上昇に伴い、影響範囲が広がっていく<br />
スタイルは変更コストが高く、決定の重要度も高い
</div>

</v-click>

---
layout: image-right
image: section3.png
class: mt-45
backgroundSize: 20em 60%
transition: slide-up
---

# 設計課題の解決領域

---
layout: two-cols-header
---

# 設計原則の役割
ソフトウェア開発の品質向上と効率化を目指す

::left::

<Transform :origin="middle">

### 解決しようとした課題

- コードの重複等による保守性の低下
- 変更の影響範囲が予測できない
- テストが困難
- チーム間での品質にばらつきがある

</Transform>

::right::

<Transform :origin="middle">

### 目指すゴール

- 一貫した設計基準を提供し、コードの品質を均一に保つ
- 保守性を向上させ、長期的な維持管理を容易にする
- 技術的負債を削減する
- チーム内のコミュニケーションを円滑にする

</Transform>

---
layout: two-cols-header
---

# 設計原則の役割
ソフトウェア開発の品質向上と効率化を目指す

::left::

<Transform :scale="0.8">

###  解決しようとした課題

1. コードの複雑性  
大規模なソフトウェアシステムの複雑さを管理し、理解しやすく保守しやすいコードを作成する。
2. 変更への対応  
ビジネス要件の変更や技術の進歩に柔軟に対応できるシステムを設計する。
3. 品質の向上  
バグの少ない、信頼性の高いソフトウェアを開発するための指針が求められた。
4. 開発効率の改善  
開発時間の短縮と、チーム間のコミュニケーション改善が必要。
5. 再利用性の促進  
コードの再利用を促進し、開発コストを削減する必要。

</Transform>


::right::

<Transform :origin="middle">

## 主な目的

1. コードの保守性向上
2. 再利用性の促進
3. 拡張性の確保
4. バグの減少
5. 開発効率の向上


<v-click>

<div class="speech-bubble">
変更に強く理解しやすいコードにする<br />
変更容易性と理解容易性を高くする
</div>

</v-click>

</Transform>

---

# 設計原則による課題解決マトリクス
SOLID 原則での課題解決事例

| 課題 | 単一責任原則（SRP） | オープン/クローズド原則（OCP） | リスコフの置換原則（LSP） | インターフェース分離原則（ISP） | 依存性逆転原則（DIP） |
|------|---------------------|--------------------------------|---------------------------|--------------------------------|----------------------|
| コードの複雑性 | クラスの目的を明確化 | 継承やポリモーフィズムを活用 | 一貫した振る舞いの提供 | 必要な機能だけを提供 | 抽象化と依存関係の最小化 |
| 変更への対応 | 変更理由の一つに限定 | 新機能追加時に既存コードを変更しない | クライアントコードの変更を最小限に | インターフェースの分離 | 依存関係の逆転による柔軟性 |
| 品質向上 | 高凝集を実現 | 変更影響範囲の最小化 | クライアントコードとの結合を維持 | 高凝集のインターフェース | モジュール間の独立性向上 |


---
layout: two-cols-header
---

# アーキテクチャパターンの役割
複雑化するエンタープライズアプリケーションの設計と統合における共通課題に対処するための体系化

::left::

<Transform :scale="1.0">

###  解決しようとした課題

- 似たような問題を何度も解決している
- 設計ノウハウが共有されない
- 実装方法の選択に時間がかかる
- チーム間で実装方法がバラバラ

</Transform>


::right::

<Transform :scale="1.0" :origin="middle">

### 目指すゴール

- 再利用可能な設計手法を提供し、効率的な開発を実現する
- 設計の標準化と一貫性を確保する
- チーム間のコミュニケーションを促進する

</Transform>

---
layout: two-cols-header
---

# アーキテクチャパターンの役割
複雑化するエンタープライズアプリケーションの設計と統合における共通課題に対処するための体系化

::left::

<Transform :scale="0.6">

###  解決しようとした課題

1. 複雑性の管理  
大規模エンタープライズアプリケーションの複雑さを管理し、理解しやすく保守しやすいシステムを設計する必要。
2. 再利用性の向上  
共通のパターンを識別し、再利用可能なソリューションを提供することで、開発効率を向上させる必要。
3. システム統合の複雑さ  
異なるシステム間の統合が複雑化し、標準化されたアプローチが必要。
4. スケーラビリティとパフォーマンス  
増大するデータ量とユーザー数に対応できる、スケーラブルで高性能なシステムの設計が求められた。
5. 分散システムの課題  
分散システムにおける一貫性、可用性、パーティション耐性（CAP 定理）などの課題に対処する必要。
6. 技術の進化への対応  
急速に進化する技術環境に適応できる柔軟なアーキテクチャの設計が必要。

</Transform>

::right::

<Transform :scale="0.7" :origin="middle">

### 主な目的

* PoEAA（Patterns of Enterprise Application Architecture）  
  1. エンタープライズアプリケーションの設計に関する知識の体系化
  2. 複雑なビジネスロジックとデータ処理の効率的な実装方法の提供
  3. スケーラブルで保守性の高いアプリケーション構築のための指針提供
* EIP（Enterprise Integration Patterns）  
  1. 分散システム間の統合パターンの標準化
  2. メッセージングシステムを使用した効果的な統合方法の提供
  3. 複雑な統合シナリオに対する共通語彙の確立

<br />
<v-click>

<div class="speech-bubble">
共通言語としての機能<br />
設計意図の明確な伝達
</div>

</v-click>
</Transform>

---
layout: two-cols-header
---

# アーキテクチャスタイルの役割
ソフトウェアシステムの複雑化と多様化が大きく影響して発展

::left::

<Transform :scale="1.0">

###  解決しようとした課題

- システム全体の一貫性が保てない
- スケーラビリティの要件に対応できない
- チーム間の連携が困難
- 長期的な進化が難しい

</Transform>

::right::

<Transform :scale="0.9" :origin="middle">

### 目指すゴール

- システム全体の構造を決定し、一貫した設計を提供する
- スケーラビリティを確保し、システムの成長に対応する
- チーム間の協調とコミュニケーションを促進する
- 長期的なシステムの進化を支援する

</Transform>

---
layout: two-cols-header
---

# アーキテクチャスタイルの役割
ソフトウェアシステムの複雑化と多様化が大きく影響して発展

::left::

<Transform :scale="0.6">

###  解決しようとした課題

1. システム全体の複雑性管理  
大規模システムの全体構造を簡素化し、理解しやすくする必要。
2. スケーラビリティとパフォーマンスの最適化  
システム全体のスケーラビリティを向上させ、大規模なデータ処理や高負荷に対応する必要。
3. 分散システムの課題への対応  
ネットワーク遅延、部分的な障害、データの一貫性など、分散システム特有の問題に対処する必要。
4. 異種システム間の統合  
異なる技術や標準を使用するシステム間の効果的な統合方法が求められた。
5. 変更への適応性  
ビジネス要件や技術の変化に迅速に対応できる柔軟なアーキテクチャが必要。
6. 開発・運用の効率化  
システムの開発、デプロイ、運用を効率化し、継続的なデリバリーを可能にする必要。

<v-click>
<div class="speech-bubble">
いっぱいあり、抽象的
</div>
</v-click>

</Transform>

::right::

<Transform :scale="0.9" :origin="middle">

### 主な目的

1. システムの全体的な構造を定義
2. コンポーネント間の関係を明確にする
3. アーキテクチャ特性をカバーする
4. 経験豊富なアーキテクト間の共通言語として機能する
5. システムの品質属性（パフォーマンス、スケーラビリティ、セキュリティなど）を達成する
6. コンポーネントや機能の再利用性を向上させる
7. システム内のコンポーネントや外部システムとの統合を容易にする
8. 将来的な変更や拡張に対する柔軟性を確保する
9. パフォーマンス、保守性、信頼性などのシステム品質を設計段階で担保する

</Transform>

---

# 相互補完の効果
各概念は独立ではなく、相互に補完

| 役割・効果 | 設計原則 | アーキテクチャパターン | アーキテクチャスタイル |
|----------------|----------|------------------------|------------------------|
| 品質の確保     | - コードの品質基準<br>- 変更容易性の確保 | - モジュール構造の一貫性<br>- 再利用性の向上 | - システム全体の整合性<br>- 長期的な保守性 |
| 実装の指針     | - 具体的な実装の判断基準<br>- コードレベルの品質確保 | - コンポーネントの実装方針<br>- インターフェースの定義 | - システム構造の大枠決定<br>- 主要コンポーネントの特定 |
| 変更への対応   | - 局所的な変更の容易さ<br>- テスタビリティの確保 | - モジュール単位の変更管理<br>- 依存関係の制御 | - 大規模な変更の制御<br>- 進化の方向性の提供 |

<br />
<v-click>

<div class="speech-bubble">
協調して機能することで、より堅牢で適応性の高いソフトウェア設計が可能
</div>

</v-click>


---

# ボトムアップの重要性
下位の概念が上位の品質を支える

補完関係により以下を実現

- 一貫性のある設計判断が可能に
- 各レベルでの品質確保
- 変更に強いシステムの実現
- 長期的な保守性の向上

<br />
<v-click>

<div class="speech-bubble">
組み合わせにより実用的な設計を実現
</div>

</v-click>

---
layout: image-right
image: section4.png
class: mt-45
backgroundSize: 20em 60%
transition: slide-up
---

# 設計概念の歴史的発展
なぜこれらの設計概念が生まれて来たのか？

---

# 1960-1970年代: ハードウェア依存時代
設計原則の萌芽

* 構造化プログラミングの登場
* モジュール化、カプセル化の概念確立
* ソフトウェアの複雑性に対する初期の対応

---

# 1980-1990年代: パッケージソフトウェアの台頭
原則の体系化とパターンの出現

【設計原則の確立】
- 1988: CRC（Class-Responsibility-Collaboration）
- 1995: SOLID 原則（Robert C. Martin）
- 1999: DRY, YAGNI 等の原則

【デザインパターンの体系化】
- 1987: Kent Beck & Ward Cunningham がパターン言語を提唱
- 1994: GoF 本「Design Patterns」出版
- オブジェクト指向設計の知見を集約

---

# 2000年代：SaaS/Webサービスの時代
エンタープライズパターンの体系化  

【アーキテクチャパターンの整理】
- 1996〜2009: Pattern-Oriented Software Architecture（POSA）シリーズ  
  - 広範なシステムアーキテクチャパターン ^[基本的なアーキテクチャパターンから始まり、分散コンピューティングからリソース管理、パターン言語まで幅広いトピックをカバーしています]を扱う
- 2002: Patterns of Enterprise Application Architecture (PoEAA)
  - エンタープライズアプリケーションの知見集約 ^[アーキテクチャパターンのカタログとしてまとめられています]
- 2004: Enterprise Integration Patterns(EIP)
  - システム統合のパターン化

---

# 2010年代以降：クラウドネイティブ時代
アーキテクチャスタイルの進化  

- マイクロサービス
- イベント駆動アーキテクチャ
- サーバーレスアーキテクチャ

<br />
<v-click>

<div class="speech-bubble">
クラウド時代の新たな課題に対応<br />  
続々とXXXアーキテクチャが出現してくる
</div>

</v-click>

---
layout: image-right
image: section5.png
class: mt-45
backgroundSize: 20em 60%
transition: slide-up
---

# ソフトウェアの形態と開発スタイルの変遷

---

# 1960-1970年代：ハードウェア依存時代  
専用ハードウェアでのみ動作する組み込み型システムを、少人数でウォーターフォール型の開発で作り上げる時代

【ソフトウェアの形態】
- メインフレーム専用のソフトウェア
- 顧客固有のカスタムシステム
- ハードウェアの付属品的な位置づけ

【開発スタイル】
- ウォーターフォール型
- 少人数での開発
- ハードウェア仕様に強く依存

<br />
<v-click>

<div class="speech-bubble">
利用形態が限定的。ワンオフで作りきり、修正ができない
</div>

</v-click>

---

# 1980年代：パッケージソフトウェアの台頭
各 PC にインストールして利用するパッケージを、バージョン管理とリリース計画に基づくチーム開発で進める時代

【ソフトウェアの形態】
- パッケージソフトウェア
- クライアント/サーバーシステム
- 汎用的な業務アプリケーション

【開発スタイル】
- 複数バージョンの管理
- チーム開発の一般化
- 品質管理プロセスの確立

<br />
<v-click>

<div class="speech-bubble">
利用形態が多様化。ソフトウェアも大規模化する。開発スタイルも複雑化。
</div>

</v-click>

---

# 1990年代：エンタープライズ化
大規模な業務システムをコンポーネント単位で開発・カスタマイズし、組織全体に展開する反復型開発の時代

【ソフトウェアの形態】
- エンタープライズパッケージ
- Web ベースの ERP/CRM
- カスタマイズ可能なプラットフォーム

【開発スタイル】
- コンポーネントベース開発
- 反復型開発の導入
- グローバル開発チーム

<br />
<v-click>

<div class="speech-bubble">
パッケージソフトウェア時代からSaaS時代への重要な過渡期<br />  
カスタイマイズも入り、システムに求められる要件も高度化
</div>

</v-click>

---

# 2000年代：SaaS/Webサービスの時代
ブラウザを通じて継続的に進化するサービスを、アジャイル開発による迅速な機能改善で実現する時代

【ソフトウェアの形態】
- SaaS モデル
- Web アプリケーション
- サブスクリプションベース

【開発スタイル】
- アジャイル開発
- 継続的デリバリー
- フィーチャー単位の開発

<v-click>

<div class="speech-bubble">
Ruby on Railsの普及<br />  
新興のWebアプリケーションフレームワークがたくさん生まれた
</div>

</v-click>

---

# 2010年代以降：クラウドネイティブ時代
クラウド上のサービス群を組み合わせて利用するシステムを、DevOps による自動化と分散開発で構築する時代

【ソフトウェアの形態】
- クラウドネイティブアプリケーション
- マイクロサービス
- API エコノミー

【開発スタイル】
- DevOps
- コンテナベース開発
- インフラのコード化

<v-click>

<div class="speech-bubble">
インフラのコード化<br />  
モバイルアプリ化や、Single Page Applicationも台頭してきた
</div>

</v-click>

---
transition: fade
---


# 変化の本質
変化のまとめ

| 変化の方向性               | パッケージソフトウェア時代   | SaaS/Webサービス時代     | クラウドネイティブ時代          |
|--------------------|-----------------------------|----------------------------|------------------------------|
| 提供形態       | パッケージ販売                | サブスクリプション          | 従量課金/サービス連携           |
| 開発スタイル   | ウォーターフォール            | 反復型/アジャイル           | 継続的デリバリー                |
| チーム構造    | 少人数チーム                  | 大規模チーム               | 分散自律チーム                  |
| アーキテクチャ | モノリシック                  | コンポーネントベース        | マイクロサービス               |

---

# ソフトウェア開発の進化

<img src="./software_development_evolution.svg" class="h-85" />

<v-click>

<div class="speech-bubble">
ソフトウェアはよりリッチで大規模化する<br />  
考慮する要素も増え、複雑さが増し、開発の難易度も高まり続けている
</div>

</v-click>

---

# 変化の方向性
これらの変化に対応するため、設計概念も領域が拡大する

1. ビジネスモデルの変化  
  - 一時販売 → 継続的な収益
  - カスタマイズ → セルフサービス
  - クローズド → オープン連携

2. 開発プロセスの変化  
  - 長期計画 → 短期サイクル
  - 品質保証 → 継続的改善
  - 固定要件 → 柔軟な適応

3. 技術的な変化  
  - 密結合 → 疎結合
  - 単一障害点 → 分散システム
  - 手動運用 → 自動化

---
layout: fact
transition: fade
---

# なんで変化していったの？🤔

---
layout: fact
transition: fade
---

# ビジネスや環境の変化に追従するため📈
現在のソフトウェア開発と似ていませんか？

---
layout: fact
transition: fade
---

# 変化し続けるものを作り続けている🛠️
設計概念もその中で生み出された

---
layout: fact
transition: fade
---

# 目的も同じ🎯
ビジネスの変化に追従できるソフトウェア設計が求められる

---
layout: cover
background: big-ball-of-mud.png
transition: fade
---

# 大きな泥団子を作っている場合ではない
茹でガエルになってはいけない

---

# 大きな泥団子
Big ball of mud

明確なアーキテクチャや設計思想がなく、場当たり的に継ぎ足し修正を繰り返した結果、まるで泥団子のように内部構造が複雑に入り組んでしまったソフトウェアシステムのこと

【特徴】  
* 理解困難: システム全体の構造が把握しにくく、一部を修正するだけでも全体に影響が及ぶため、変更や機能追加が困難
* 保守性の低下: コードが整理されておらず、可読性が低いため、バグが発生しやすく、修正にも時間がかかる
* 技術的負債の蓄積: 場当たり的な修正を繰り返すことで、システムの内部構造がますます複雑化し、長期的な開発効率を著しく低下させる「技術的負債」が蓄積する

---
layout: image-right
image: section6.png
class: mt-45
backgroundSize: 20em 60%
transition: slide-up
---

# 実践的なアプローチ

---
layout: center
---

# いつ、何を考えるか？💭

---
layout: section
transition: fade
---

# 設計原則

---
layout: fact
---

# <span v-mark="{ at: 1, color: 'orange', type: 'circle', strokeWidth: 5 }">常に意識</span>し続けるもの🧠

---

# 設計原則
常に意識し続けるもの

- コーディング時の判断基準
- レビュー時の評価基準
- リファクタリングの指針
- 新規コード作成時のガイドライン

---
layout: section
transition: fade
---

# アーキテクチャパターン

---
layout: fact
transition: fade
---

# フレームワーク全盛時代にイチから考えることは少ない🧩

---
layout: fact
transition: fade
---

# アーキテクチャパターンは<span v-mark="{ at: 1, color: '#FCAF17', type: 'highlight', iterations: 3 }">戦術的</span>に扱う🏗️
既に誰かが通ってきた道

---
layout: fact
transition: fade
---

# フレームワーク選定時に概ね決まる☑️

---

# アーキテクチャパターン
フレームワーク選定時に概ね決まる

- 問題解決のためのツールボックスとして捉える  
過去の経験から得られた成功事例に基づいて体系化されている。実践的な知識として活用
- MVC パターンはフルスタックフレームワークなら大体ある
- Laravel なら ActiveRecord パターン（Eloquent）
- Symfony なら Data Mapper パターン（Doctrine）
- 必要に応じて取捨選択  
フレームワークを薄く使う

---
layout: section
transition: fade
---

# アーキテクチャスタイル

---
layout: fact
transition: fade
---

# アーキテクチャスタイルは<span v-mark="{ at: 1, color: '#FCAF17', type: 'highlight', iterations: 3 }">戦略的</span>に扱う💡
戦略は各システム・ビジネスの事情から生まれるもの

---
layout: fact
transition: fade
---

# 判断が一番むずかしい😵‍💫
なぜなら最も抽象度が高い設計判断になる。決定の影響が全体に及ぶ為

---
layout: fact
transition: fade
---

# 理想は「僕が考えた最強のアーキテクチャ」を考え抜いて作り込むこと💪
オレオレアーキテクチャを熟成したものがスタイルになる

---
layout: fact
transition: fade
---

# 但し、プロジェクト初期は過度に目指さない！⚖️
コアドメインの見極めが重要

---
layout: fact
transition: fade
---

# 原則ベースの継続的改善していくのがいいのでは？🧭

---
layout: full
transition: slide-up
---

<Tweet id="1882578423094419522" />

---
layout: section
transition: fade
---

# 一つの事例

---
transition: fade
---

# 段階的にリアーキテクチャしたお話
サービス間でも DIP が適用できる！

<a href="https://zenn.dev/litalico/articles/domain-distillation">
<img src="/hatena-bookmark.png" class="w-200"/>
</a>

---

# 記事を通して伝えたいこと
今回は時間の都合ですべてはお話できません

- <span v-mark.circle.red="1">アーキテクチャはフラクタル構造</span>を持つ  
同じパターンが異なる粒度で繰り返し現れる
- システムは階層的に構成される  
アプリケーション、パッケージ、コンポーネント、クラス、関数、式、文
- 各レイヤーには構造とアーキテクチャがあり、SOLID 原則が適用可能  
設計原則という基礎から、必然的にアーキテクチャが導かれる

---
layout: two-cols-header
---

# アーキテクチャスタイルはいつ考えるべきか？
組織/ビジネスの転換点で検討する

::left::

【タイミング】
- チーム規模の拡大時  
チーム間の責務分離が必要に  
独立したデプロイの必要性
- ビジネス要件の変化時  
スケーラビリティ要件の変化  
新規ドメインの追加（新規プロジェクト立ち上げ時も）
- リファクタリングの契機  
技術的負債の蓄積。保守性の課題  

::right::


【アプローチ方法】  
- 小規模な時は設計原則に集中
- 必要なタイミングで戦略的に判断
- ビジネスの成長に合わせた漸進的な改善

<v-click>

<div class="speech-bubble">
オーバーエンジニアリングを避け、必要なタイミングで適切な投資判断<br />  
チームの成長を考慮した判断を行う
</div>

</v-click>


---
layout: default
transition: fade-out
---

# 設計概念の向き合い方
今回一番伝えたいこと

【ボトムアップの重要性】
- 設計原則という最も具象的な概念が基礎
- 原則の理解と実践が、より大きな設計の質を支える
- 基礎なしには、上位の概念も形骸化する

【アーキテクチャはフラクタル構造】
- 同じ設計原則が異なる粒度で現れる
- システムの規模に関係なく、同じ原則が品質を支える

<v-click>

<div class="speech-bubble">
原則の深い理解がパターンやスタイルの適切な選択につながる<br />  
アーキテクチャスタイルを自然な帰結として捉える
</div>

</v-click>

---
layout: image-right
image: section7.png
class: mt-45
backgroundSize: 20em 60%
transition: slide-up
---

# まとめ

---

# 設計概念を実践で活かすために
相互関係性を理解し、バランスよく組み合わせる

設計原則を基礎として

- 日々のコーディングやレビューでの判断基準として活用
- チーム内での共通言語として定着させる
- 継続的な改善の指針として活用

アーキテクチャは段階的に

- 小規模なうちは原則に集中
- ビジネスの成長に合わせて発展
- 必要なタイミングで戦略的に判断

---
layout: default
transition: fade-out
---

# 継続的な進化のために
アーキテクチャスタイルはシステム全体の構造やコード配置の設計指針となる

実践のポイント

- 完璧な設計を目指すのではなく、変化に強い設計を目指す
- オーバーエンジニアリングを避け、必要に応じて段階的に改善
- チームの理解度とビジネスの要件をバランス

Key Message

- 設計原則という基礎が、より大きな設計の質を支える
- アーキテクチャは自然な帰結として導かれるもの
- 実践を通じた継続的な学びと改善を心がける

---
layout: default
transition: fade-out
---

# 進化的アーキテクチャとなる
変化を前提としたシステム設計のアプローチ

<img src="./architecture_levels_cone_diagram.svg" class="h-85" />

<v-click>

<div class="speech-bubble">
らせん状に進化するイメージ
</div>

</v-click>

---
layout: image-right
image: section8.png
class: mt-45
backgroundSize: 20em 60%
transition: slide-up
---

# 付録

---

# 参考資料 & 書籍
紹介した書籍や、学習に使えるページ

【書籍】
- [「TECHNICAL MASTER はじめてのPHP エンジニア入門編」](https://www.shuwasystem.co.jp/book/9784798073224.html)
- [Pattern-Oriented Software Architecture](https://www.amazon.co.jp/Pattern-Oriented-Software-Architecture-System-Patterns/dp/0471958697)
- [Patterns of Enterprise Application Architecture](https://www.amazon.co.jp/-/en/Martin-Fowler/dp/0321127420)
- [Enterprise Integration Patterns: Designing, Building, and Deploying Messaging Solutions](https://www.amazon.co.jp/Enterprise-Integration-Patterns-Designing-Addison-Wesley/dp/0321200683)

【資料】
- [Patterns of Enterprise Application Architecture - Martin Fowler's Bliki (ja)](https://bliki-ja.github.io/pofeaa/)
- [Table of Contents - Enterprise Integration Patterns](https://www.enterpriseintegrationpatterns.com/patterns/messaging/toc.html)  


---
layout: end
---

ご清聴ありがとうございました