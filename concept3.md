## variablesを使う

さて、ここまではCSSと全く同じ書き方をしてきたわけですが、ここからはSass流の書き方を学んでいきましょう。まず最初に`variables`の使い方から学びます。variablesは例えばサイト全体での基本となる色やフォントサイズなどを指定したい場合に利用します。例えば上記の例ではbodyに`color: #ddd;`と指定しました。これをvariablesを使って書き直すと以下のようになります。

```scss
/* app.scss */

$base-color: #ddd;
...
```

```scss
/* _base.scss */

body {
  font-size: 12px;
  line-height: 1.4;
  color: $base-color; /* variablesを利用 */
}
```

このようにvariablesを設定しておけば、CSSスタイリングの様々な場面で色などを統一しやすくなります。また、「基本のフォントカラー」という意味合いを与えることが出来るので、他の開発者が見た時にスタイリングの意味が伝わりやすくなります。

## ネストを使う

オブジェクト指向CSSの項目では、インスタグラム風のカードを試しに作ってみました。この時、投稿に対するコメント欄のCSSを以下のように書いていました。

```css
.card-comments {
  margin-bottom: 4px;
}
.card-comments a {
  margin-right: .3em;
}
```

この例では、.card-commentsにネストされているセレクタのスタイルは一つだけですが、これがもっと増えるとどうでしょう。

```css
.card-comments {...}
.card-comments a {...}
.card-comments img {...}
.card-comments .user-comment {...}
.card-comments .poster-comment {...}
```

そうすると、上の例のように文字数が多く分かりづらくなります。これをSassでは次のように書き換えることが出来ます。

```scss
.card-comments {
  ...
  a {...}
  img {...}
  .user-comment {...}
  .poster-comment {...}
}
```

いかがでしょう。`.card-comments`を書くのが一度だけで済むのでスッキリして分かりやすくなったはずです。

## extendを使う

グリッドレイアウトの例では以下のようなCSSスタイルを定義しました。

```css
.col-1, .col-2, .col-3, .col-lg-1, .col-lg-2, .col-lg-3 {
  padding: 0 15px;
}
```

このように、`padding:0 15px;`を定義する時に全てのセレクタを書くのもいいですが`extend`を使う書き方もあります。extendを使うと一つのセレクタのスタイルを他のセレクタで`@extend セレクタ名`で利用することが出来ます。例えば上記のCSSは以下のように書き換えられます。

```scss
.col-padding {
  padding: 0 15px;
}

.col-1 {
  @extend .col-padding;
  ...
}
.col-2 {
  @extend .col-padding;
  ...
}
.col-3 {
  @extend .col-padding;
  ...
}
以下続く
```

これをコンパイルすると次のようになります。

```scss
.col-padding, .col-1, .col-2, .col-3, .col-lg-1, .col-lg-2, .col-lg-3 {
  padding: 0 15px;
}
.col-1 {...}
.col-2 {...}
以下続く
```

`extend`を使うことでカラムの一つ一つが決まった`Padding`を持つことが分かりやすくなりました。


## オペレーター(計算式)を使う

同様にグリッドレイアウトの例では、何％の割合となるのかを一つ一つ計算して入力してました。

```css
.col-1 {
  flex-basis: 33.33%;
}

.col-2 {
  flex-basis: 66.67%;
}

.col-3 {
  flex-basis: 100%;
}
```

このやり方でも良いのですが、Sassのオペレーターを使うともっと簡単にすることが出来ます。

```scss
.col-1 {
  flex-basis: 1 / 3 * 100%;
}

.col-2 {
  flex-basis: 2 / 3 * 100%;
}

.col-3 {
  flex-basis: 100%;
}
```

コンパイルすると以下のようになります。

```css
.col-1 {
  flex-basis: 33.3333333333%; }

.col-2 {
  flex-basis: 66.6666666667%; }

.col-3 {
  flex-basis: 100%; }
```

毎回計算しなくていいので非常に楽ですね。

## mixinを使う

mixinを使うとベンダープレフィックスのように重要だけど一個一個書くのが冗長になりがちな部分を簡単にすることが出来ます。たとえば、以下の例をご覧下さい。

```css
.card-wrapper {
  border-radius: 5px;
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
}
```

このようにborder-radiusを定義する度にベンダープレフィックスを含めて3行書く必要があります。mixinを使うとこれを以下のように書き換えられます。

```scss
@mixin border-radius($radius) {
  border-radius: $radius;
  -webkit-border-radius: $radius;
  -moz-border-radius: $radius;
}

.card-wrapper {
  @include border-radius(5px);
}
```

ここで注目してもらいたいのが@mixinの中の($radius)という部分です。この部分を引数と呼び、ここに入れた値はその後、`border-radius: $radius;`のように再利用されています。

例えば、上の例ではこの引数の部分に`5px`が入っていますが、5pxだけではなく他の数字を入れることで全ての`border-radius`をmixinで簡単に書くことが出来ます。

```scss
@include border-radius(1em); /* 1emのborder-radius */
@include border-radius(10px); /* 10pxのborder-radius */
@include border-radius(50%); /* 50%のborder-radius */
```

## まとめ

Sassを使いこなすとスタイルをより分かりやすく少ない行数で定義することが出来ます。今回のレッスンだけではまだ理解がすぐ出来なかった箇所もあるかもしれないですが今後、自分のプロジェクトなどで使っていくことでSassの便利さが分かってくるはずです。まずはVarialblesやネストといったところからスタートして徐々に`Mixin`や`extend`も使いこなせるようになっていきましょう。

## 更に学ぼう

### 記事で学ぶ

[Sass Basics - Sass公式サイト](http://sass-lang.com/guide)

### 動画で学ぶ

[Sass/SCSS入門 - ドットインストール](https://dotinstall.com/lessons/basic_sass)