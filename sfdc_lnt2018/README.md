# Lightning Now Tour Japan @ SFDC 2018/10/26 Memo

## Opening

lightning 利用状況アプリケーション：本番環境のみ

ligntning usage app

## Trailhead

Trailhead Project: Build Flexible Apps with Lightning Components

(ja) Lightning コンポーネントを使用した柔軟なアプリケーションの構築

<http://bit.ly/LNT2018DEV>

<https://trailhead.salesforce.com/content/learn/projects/workshop-lightning-programmatic>

*(FYI) [Memo](#Memo_of_Trailhead_Project) is at the bottom

## tool and tips

- 一覧 Components - Salesforce Lightning Component Library

  <https://developer.salesforce.com/docs/component-library>

-> Link to Org

self components -> namespace c

Salesforce 組織で使用できる Lightning コンポーネントの完全なコレクションを表示するには、ログインしてコンポーネントライブラリに移動します。

 `https://\<myDomain\>.lightning.force.com/componentReference/suite.app`

> Salesforce にログインすることなくコンポーネントライブラリを使用することもできます。

<https://developer.salesforce.com/docs/component-library>

- tool: Lightning Inspector

  最終的に画面をどのcomponentが出力しているのかなどを確認可能

### Lightning component testing : Lightning Testing Service (LTS)

- Jestなどをサポート（Winter '19-）

  Replaced Chai and Mocha by Jest!!

- lightning component : coverage 75% up という制約はないためツールを使って。を推奨

### IDE

Force.com IDE support was expired. -> VS code with Salesforce extension

### 既存のJS library -> Lightning component for ISV

- Lightning基本component

React 37 + google html 43 + Visualforce component 90 + alpha (as of 2016) -> Lightning componentとして利用可能に

@Lightning namespace

## visualforce vs lightning

- VF: パフォーマンスの問題：クライアント側での変更がわずかであっても、都度、viewstate でページのレンダリングデータをすべてサーバに送っている

  *background - Java (JVM)

- lightning msg : 変更内容のjsonのみ、ただし最初のページロードでAstro+スノボの待ち時間でbase component、rendering engine読み込みのため時間がかかる

### 最低限必要なlinghtningコード

- Conponent コンポーネント：HTMLとXMLマークアップ

- Controller コントローラ

  ↑以上2つが最低限

- Helper ヘルパー : common JS

- Style : CSS

- ...

- SVG:アプリケーションビルダーのアイコン

### interface

record Id読み込み後に初期化するなど、ライフサイクル管理などを独自に実装するのを省くため、どこで使用するかを定義するため
implement {CONTEXT  such as Page}

### design system

- blueprint - Salesforce Lightning Design System

標準のタグ、マークアップであれば、特にCSSを書かなくても、Lightning のデザインで実装可能

- BEM命名規則

bootstrap (by Twitter), etc. と共通のものを採用

  e.g.
  
  .house
  
  .house__door
  
  .house_red  : modifier, variation
  
  .house__door_red

## lightning basic component

lightning:..... are smart!

meta data -> Apexでデータを読み込まなくてもMETAデータを認識可能

-> なるべく基本コンポーネントを使っていくことを推奨

winter'19 -  lightning:map (google map)など随時追加

## lightning controller 2 types

client side, server side : MVCC

(FYI) see lightning component basics - lightning component の使用開始 trail

- <aura:handler name="init" value="{! this}" action="{!c.doInit}"/>

  handler ... イベント処理
  
  名前を「init」にした場合には、特別に、初回表示時のアクションの定義になる

## lex URL change on Summer'18

lightning application を作成した際のURLが変わった、ということ

one.app以外にカスタムapp (=lightning application ) を作成した場合のこと

## controller .js

function を連想配列で定義する、というのが決まり、SF lexの制約

---

## Memo_of_Trailhead_Project

### unit 1

- ptrparation

create new (if not exist) record page of property object as API name 'Property_Record_Page'
 in any edit page , such as lightning app builder in setup

- note

  最終的にcontroller (HelloWorldController.js)は使用していないが、これは、OnClick()イベントなどを処理できるということのサンプルとして参照

- <aura:attribute > タグで変数名を保存

  \<div class="slds-card"\>
   -> 組み込みのクラスを使用、余白ありのカード； デザイン済みで使用推奨

  \<lightning:input\> で入力、そしてバインディング
  
  -> ! {!v.greeting} でバインディング

### unit 3,4 summary

$Aはフレームワークへのショートカット

Component, Controller

- Controllerを補完するHelperで、標準的なlightning componentを実装可能

  *note: Helperはあくまで、該当component内での複数のcontroller間での共通処理の実装方法
  複数componentで共通の処理を実装したい場合には、別のcomponentとして実装して、子componentとして読み込ませる。
  そして、auraメソッドで他のコンポーネントから読み出す

  \[copy (source: trail) \]
ヘルパー関数はコンポーネントに対してローカルであり、コードの再利用を促進し、クライアント側コントローラの JavaScript ロジックの複雑な作業を軽減します。

### data service

Apex : field level securityが無視されてしまう
⇒Lightning data serviceでは考慮される
  -> force:recordData など対象のコンポーネントを利用推奨

現在のバージョン44では、1件のみレコードを取得する場合に利用可能

### design parameter

検索条件の項目、値を設定可能なUIを管理者、ユーザーに提供

⇒コーディングなしでカスタマイズ可能な範囲を拡大し、再利用率を上げられる

### unit 5 typo

- パート 1: Lightning データサービスを使用する

  1. 開発者コンソールで、SimilarProperty コンポーネントマークアップを開きます。
  
    X SimilarProperty  -> (fixed) SimilarProperties

- パート 7: 条件付きでコンテンツを表示する

  1.開発者コンソールで、SimilarProperty コンポーネントマークアップに切り替えます。
  
    X SimilarProperty  -> (fixed) SimilarProperties

## Tips

- developer console

right click -> new tab でタブで開くことが可能 (*chrome)

/