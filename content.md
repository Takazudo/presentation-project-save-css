<h1 style="line-height:1.4;font-size:3em; letter-spacing:-.025em">プロジェクトを<br>殺さないCSS設計</h1>

<p style="margin-bottom:0;padding-bottom:0;font-size:1.3em">高津戸壮 <a href="https://twitter.com/Takazudo">@Takazudo</a></p>

----

## 自己紹介

<div style="display:table; width: 100%">
<div style="display:table-cell; vertical-align:middle; width:65%; vertical-align:top; padding:30px 0 0">
<ul>
<li>高津戸壮 (たかつど たけし)</li>
<li><a href="http://www.pxgrid.com/">株式会社ピクセルグリッド</a></li>
<li>フロントエンドエンジニア</li>
<li><a href="twitter.com/Takazudo">@Takazudo</a></li>
</ul>
</div>
<div style="display:table-cell; vertical-align:middle; width:35%"><img src="myAdditions/takazudo.jpg" width="300" alt=""></div>
</div>

---

<a href="https://www.amazon.co.jp/dp/4774169447"><img src="myAdditions/jqbook.png" alt="" width="50%"></a>

----
<p style="font-size:3em">CSSをどう書けば<br>よいのか？</p>

----

## プロジェクトを<br>殺してしまうCSS

----

<p style="font-size:3em">CSSは簡単である<br>しかし難しい</p>

----

## HTMLを書きます

```html
<div>
    hoge
</div>
```

---

## classをつけます

```html
<div class="box">
    hoge
</div>
```

---

## CSSを書きます

```css
.box {
    color: red;
}
```

---

## 基本的にはこれだけ

* セレクタは色々あるが別に全部覚えなくてもよい
* プロパティは沢山あるが書いていけば慣れる
* どう書くって、好きに書けばいいんでは？

----

## 好きに書くと発生すること

* UIを追加／調整したい
* 関係ないページでレイアウトが崩れる
* 書いたCSSが効かない

----

## なぜか？

* 書いたルールが別の所に影響する
* どこかに書かれたルールが<br>新しく書かれたHTMLに影響する

----

## その結果起こること

* 些細な変更によりサイトが壊れるので保守できない
* 何をしようにも時間がかかってしまう
* プロジェクトは緩やかに死んでゆく

----

<p style="font-size:2em">CSS設計の破綻を後から<br>解決することはできない</p>

----

## どうすればよいのか

* CSS設計をちゃんとする
* そのためのヒントがCSS設計方法論
* CSS書いてる人は知っておくべき
* CSS書いてない人も知っておけば色々スムーズ
* 概念だけでも分かっていると役に立ちそう

----

## 今日紹介すること

* OOCSS
* BEM
* SMACSS
* Atomic Design
* Enduring CSS

----

# OOCSS

----

## OOCSSとは

* [Object Oriented CSS](http://www.slideshare.net/stubbornella/object-oriented-css)
* Nicole Sullivan (当時Yahoo!)
* 2009年
* ページをレゴの集まりとして考える
* オブジェクト指向っぽい継承の概念


----

## レゴの集まり？

---

![](imgs/oocss/modules2.png)

---

![](imgs/oocss/modules3.png)

---

```css
/* heading module */

.heading {
  prop: val;
}

/* heading2 module */

.heading2 {
  prop: val;
}

/* heading3 module */

.heading3 {
  prop: val;
}
  .heading3 span {
    prop: val;
  }
```

レゴの部品: Object

---

<img src="imgs/oocss/media.png" alt="" style="width:60%">

---

<img src="imgs/oocss/media2.png" alt="" style="width:60%">

---

![](imgs/oocss/modules.png)

----

## スキン

* オブジェクト指向の継承の概念
* 似たUIパーツを効率よく書く方法
* 共通項目を一つのモジュールに定義
* バリエーションをスキンとして定義

---

![](imgs/oocss/skin.png)

---

![](imgs/oocss/button_base.png)

```html
<span class="button">Button!!</span>
```

```css
.button {
  font-size:1.5em;
  padding:.5em 2em .4em;
  border:3px solid #000;
  border-radius:10px;
}
```

---

![](imgs/oocss/button_caution.png)

```html
<span class="button caution">Caution!!</span>
```

```css
.caution {
  font-weight:bold;
  color:#fff;
  background:#FD3636;
  border-color:#BC2828;
}
```

---

![](imgs/oocss/button_pdf.png)

```html
<span class="button pdf">Download PDF!!</span>
```

```css
.pdf {
  background:#ECE4AB;
  border-color:#D9D29E;
  padding-left:1.5em;
}
.pdf:before {
  content: '';
  display:inline-block;
  width:22px;
  height:22px;
  background:url(imgs/acrobat.png);
  vertical-align:-2px;
  margin:0 6px 0 0;
}
```

---

![](imgs/oocss/button_play.png)

```html
<span class="button play">Play sound!!</span>
```

```css
.play {
  background:#C3E6EA;
  border-color:#AECDD0;
  padding-left:1.5em;
}
.play:before {
  content: '';
  display:inline-block;
  width:22px;
  height:22px;
  background:url(imgs/play.png);
  vertical-align:-2px;
  margin:0 6px 0 0;
}
```

----

## OOCSSでの設計の流れ

* レゴファーストでコーディング
* 具体的なページはレゴを組み合わせる
* 新規ページ作成時は既存のレゴを使いまわし
* 足りないレゴだけ新しく作る
* 似たレゴはスキンで表現

----

## その結果

* 何度も同じようなCSSを書かなくて良くなる
* CSSの量を最小限にできる
* コードを再利用することで<br>デザインの統一性が保たれる
* 効率的！

----

# BEM

----

## BEMとは

* [getbem.com](http://getbem.com/)
* クラス名の命名規則が特徴的で有名
* かなり知名度が高い
* 基本的にはOOCSS同様モジュール指向
* Block Element Modifier

----

<img src="imgs/bem/bemExp1.png" style="width:100%" alt="">

---

### Block

ページを構成するパーツの単位

### Element

Blockを構成するパーツの単位

### Modifier

Block・Elementを変更する追加クラス

----

<img src="imgs/bem/tab1.png" style="width:100%" alt="">

---

<img src="imgs/bem/tab2.png" style="width:100%" alt="">

---

<img src="imgs/bem/tab3.png" style="width:100%" alt="">

---

<img src="imgs/bem/tab4.png" style="width:100%" alt="">

----

<img src="imgs/bem/media1.png" style="width:100%" alt="">

---

<img src="imgs/bem/media2.png" style="width:100%" alt="">

---

<img src="imgs/bem/media3.png" style="width:100%" alt="">

---

<img src="imgs/bem/media4.png" style="width:100%" alt="">

----

## クラス名命名規則

<p style="font-size:1.3em"><code>block__element--modifier</code></p>

----

## BlockとElement

![](imgs/bem/block-exp.png)

```html
<section class="column"> ... </section>
```

---

![](imgs/bem/block-exp2.png)

---

![](imgs/bem/block-exp.png)

```html
<section class="column">
  <h3 class="column__head">About BEM</h3>
  <div class="column__body">
    <p class="column__p">The quick brown...</p>
    <p class="column__p">The quick brown...</p>
  </div>
</section>
```

---

```
.column {
  border:2px solid #000;
  border-radius:10px;
}
  .column__head {
    border-bottom:2px solid #000;
    padding:.8em 20px .7em;
    margin:0;
    font-size:1.4em;
  }
  .column__body {
    padding:1em 20px 0;
  }
    .column__p {
      margin:0;
      padding:0 0 1em;
    }
```

----

## Modifier

![](imgs/bem/block-exp.png)

```html
<section class="column"> ... </section>
```

---

![](imgs/bem/mod-exp.png)

```html
<section class="column column--disabled"> ... </section>
```

```css
.column--disabled {
  opacity:.3;
}
```

---

![](imgs/bem/mod-exp2.png)

```html
<section class="column column--caution"> ... </section>
```

```css
.column--caution {
  background:#EA3B3B;
}
```

----

## BEMの特徴

* モジュール化という点については<br>OOCSSと同じ
* モジュールの中身を定義している
* クラス名で構造を表現することで<br>コードの可読性が向上する
* あえて冗長なクラス名にすることで<br>セレクタの競合を防げる
* どこかが壊れるかもというリスク回避

----

# SMACSS

----

## SMACSSとは

* Scalable and Modular Architecture for CSS
* Jonathan Snook著
* スケールできてモジュールな<br>CSS設計について書かれた本
* CSSのルールを分類して考える

---

<img src="imgs/smacss/smacss-book.png" style="width:50%" alt="">

----

## SMACSSの考え方

CSSのルールを以下の5つに分類して考える

* Base - ベースルール
* Layout - レイアウトルール
* Module - モジュールルール
* State - 状態（ステート）ルール
* Theme - テーマ

----

## Base

* 土台となるスタイルの集合
* [reset.css](http://meyerweb.com/eric/tools/css/reset/)
* [normalize.css](https://necolas.github.io/normalize.css/)
* ＋サイトに敷きたいルール

----

## Layout

* サイトレイアウトの枠組み
* およびそれを調節するための仕組み
* 段組
* `layout-layoutName`
* `l-layoutName`

---

![](imgs/smacss/layout1.png)

---

```html
<div id="all">
  <header id="header"> ... </header>
  <div id="body">
    <div id="sidebar"> ... </div>
    <main id="main"> ... </main>
  </div>
  <footer id="footer"> ... </footer>
</div>
```

---

![](imgs/smacss/layout2ex.png)


---

```html
<html class="l-flipped">
```

```css
.l-flipped #sidebar {
  float: left;
  margin: 0 20px 0 0;
}
```

---

![](imgs/smacss/layout3ex.png)


---

```html
<html class="l-fixed">
```

```css
.l-fixed #all {
  max-width:700px;
}
```

---

![](imgs/smacss/grid.png)

---

```html
<div class="l-grid">
  <div class="l-grid-item"> ... </div>
  <div class="l-grid-item"> ... </div>
  <div class="l-grid-item"> ... </div>
</div>
```

```css
.l-grid {
  ...
}
  .l-grid-item {
    ...
  }
```

----

## Module

* レイアウトの中にモジュールを入れていく
* OOCSSのObject
* BEMのBlock

---

![](imgs/oocss/modules.png)

---

![](imgs/smacss/module.png)

```html
<section class="column">
  <h3 class="column-head">About SMACSS</h3>
  <div class="column-body">
    <p>The quick brown...</p>
    <p>The quick brown...</p>
  </div>
</section>
```

---

```css
.column {
  border:2px solid #000;
  border-radius:10px;
}
  .column-head {
    border-bottom:2px solid #000;
    padding:.8em 20px .7em;
    margin:0;
    font-size:1.4em;
  }
  .column-body {
    padding:1em 20px 0;
  }
    .column-body > p {
      margin:0;
      padding:0 0 1em;
    }
```

---

### サブクラス

![](imgs/smacss/extend.png)

```html
<span class="button">Button!!</span>
<span class="button button-caution">Caution!!</span>
<span class="button button-pdf">Download PDF!!</span>
```

* OOCSSの「スキン」は、<br>SMACSSでは「サブクラス」
* 実装方法もマルチクラス利用で同じ

----

## State

* BEMのModifier
* state（状態）の変化を表す
* JavaScriptによる変化を想定

---

![](imgs/smacss/state.png)

```html
<section class="column is-disabled"> ... </section>
```

```css
.column.is-disabled {
  opacity:.3;
}
```

追加クラスで状態を表現

----

## Theme

* グローバルなレイアウト変化
* メーラの例

---

![](imgs/smacss/theme/1.png)

---

![](imgs/smacss/theme/2.png)

---

![](imgs/smacss/theme/3.png)

---

```html
<html class="theme-A">
```

```css
/* テーマA */
.theme-A .mailInbox {
  color: ...;
  background: ...;
}

/* テーマB */
.theme-B .mailInbox {
  color: ...;
  background: ...;
}

/* テーマC */
.theme-C .mailInbox {
  color: ...;
  background: ...;
}
```

----

## SMACSSの特徴

* OOCSSもBEMもモジュールの話しかしてない
* CSSのルールを分類して整理する

----

## ここまでで紹介した<br>破綻回避のヒント

---

<ul style="font-size:1.8em">
<li>モジュール化</li>
<li>クラス名の命名規則</li>
<li>CSSルールの分類</li>
</ul>

----

## 追加で考えねば<br>ならないこと

---

<ul style="font-size:1.8em">
<li>モジュールの汎用性</li>
<li>モジュールの粒度</li>
<li>モジュールの名前</li>
<li>余白をどう扱うか</li>
</ul>

----

# もう一歩先へ<br>設計のヒント

----

<ul style="font-size:1.6em">
<li>[Atomic Design](http://bradfrost.com/blog/post/atomic-web-design/)<br>抽象化による解決</li>
<li>[Enduring CSS](http://ecss.io/)<br>分離による解決</li>
</ul>

----

# Atomic Design

----

## Atomic Designとは

* [Atomic Design](http://bradfrost.com/blog/post/atomic-web-design/)
* デザインシステムを作る方法論
* ページをデザインするのではなく、コンポーネントのシステムをデザインするという考え

----

## 5レベルで<br>デザインを考える

* Atoms: 原子
* Molecules: 分子
* Organisms: 有機体
* Templates: テンプレート
* Pages: ページ

---

![](imgs/atomic/1.png)

----

### Atoms: 原子

最も小さい粒度のコンポーネント

<img src="imgs/atomic/2.png" style="width:70%">

----

### Molecules: 分子

Atomの組み合わせで作られる

<img src="imgs/atomic/3.png" style="width:70%">

----

### Organisms: 有機体

Moleculesの組み合わせで作られる

![](imgs/atomic/4.png)

----

### Templates: テンプレート

これらの組み合わせで作られるページの雛形

<img src="imgs/atomic/5.png" style="width:70%">

----

### Pages: ページ

具体的なテキストや画像いれたもの

<img src="imgs/atomic/6.png" style="width:70%">

----

## Atomic Designの<br>もたらすもの

* 別にこれはCSS設計方法論じゃない
* 一貫したコンポーネントデザインのルール
* チーム内での設計概念共有

----

<h2 style="font-size:2.6em">Enduring CSS</h2>

----

## Enduring CSSとは

* [ecss.io](http://ecss.io/)
* Ben Frain著
* Enduring: 長続きする、永続的な、<br>不朽の、我慢強い、辛抱強い
* 規模大きくてスケールするサイト向け
* Webアプリケーション用に考えられた
* 分離することでスケールを可能にする

----

## Enduring CSSの考え

* 基本はモジュール化
* ただし、抽象化しない
* その先には複雑化が待っている
* 結果としてメンテナンスのコストがかかる
* 分離することによって解決する

---

<img src="imgs/ecss/babel.png" style="box-shadow:none">

----

## 抽象化しないとは？

* 共通の細かいUIを抜き出してモジュールにしない
* モジュールは機能のまとまり単位で考える

---

![](imgs/ecss/abstraction/1.png)

---

![](imgs/ecss/abstraction/2.png)

---

![](imgs/ecss/abstraction/3.png)

----

## 名前空間による分離

* モジュールを名前空間で分類する

---

<img src="imgs/ecss/ns/a1.png" alt="" style="width:100%">

---

<img src="imgs/ecss/ns/a2.png" alt="" style="width:100%">

---

<img src="imgs/ecss/ns/b1.png" alt="" style="width:90%">

---

<img src="imgs/ecss/ns/b3.png" alt="" style="width:100%">

TopPage, ProductDetail, ShoppingCart

---

```css
/* トップページ topPage modules */
.tp-MainVisual { ... }
.tp-Carousel { ... }
.tp-NewsList { ... }

/* 商品詳細 productDetail modules */
.pd-ItemDescription { ... }
.pd-ItemMainPhoto { ... }
.pd-Carousel { ... }

/* ショッピングカート shoppingCart modules */
.sc-ItemList { ... }
.sc-UserInfo { ... }
```

---

<img src="imgs/ecss/ns/b4.png" alt="" style="width:80%">

common

---

```css
/* 共通 common modules */
.cmn-Header { ... }
.cmn-Footer { ... }
.cmn-SideAd { ... }
```

----

## アセットの分離

* CSS／JS／画像など名前空間ごとにわける

---

<img src="imgs/ecss/assets/a1.png" alt="" style="width:100%">

---

```bash
.namespaces
  ├── common
  │  ├── common.css
  │  └── common.js
  ├── productDetail
  │  ├── productDetail.css
  │  └── productDetail.js
  └── topPage
      ├── topPage.css
      └── topPage.js
```

---

<img src="imgs/ecss/assets/a2.png" alt="" style="width:100%">

---

```bash
.namespaces
  ├── common
  │  ├── common.css
  │  └── common.js
  ├── productDetail
  │  ├── productDetail.css
  │  └── productDetail.js
  └── topPage2
      ├── topPage2.css
      └── topPage2.js
```

----

## Enduring CSSの<br>もたらすもの

* 抽象化の諦めと引き換えに得られる<br>無限のスケーラビリティ
* 抽象化することだけが<br>解決方法ではないという教え

----

# まとめ

----

<ul style="font-size:1.7em">
<li>モジュール化</li>
<li>ルールの分類</li>
<li>クラス名の命名規則</li>
<li>どうモジュールを設計するか</li>
</ul>

---

<ul style="font-size:1.4em">
<li>たくさんの設計のアプローチがある</li>
<li>プロジェクトにあった設計が<br>寿命と運用のしやすさを決定する</li>
<li>とりあえずBEMオススメ</li>
<li>抽象化と分離の狭間の<br>ベストな設計を目指す</li>
</ul>

----

# ありがとう<br>ございました

----

<a href="http://www.codegrid.net/"><img src="myAdditions/codegrid.png" alt="" style="width:100%"></a>

