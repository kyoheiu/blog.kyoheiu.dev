+++
title = "Rust入門ルート"
date = 2021-02-13
math = false
[taxonomies]
categories = ["code"]
tags = ["Rust"]
+++
３、４回の挫折を経てようやく「なんとなくRustわかってきたかな」というところまで来れたので、個人的に効率的と考える入門ルートを紹介してみたい。

結論から書くと、

1. 『プログラミング言語Rust入門』を読む
2. とりあえず書いてみる
3. 実践Rustプログラミング入門』を読む

これで実践のじの字まではたどり着ける。

### 公式ドキュメントについて

もちろん充実しているし、丁寧な書きぶり・カバーぶりなのでいろいろなところでおすすめされている。でも、前知識なしに＆おおまかな全体像を持たず読もうとするとだいたいトレイトあたりで力尽きる。実際にプログラムを組むためにはそのあとの.iter()やクロージャを形式的にでも分かっていないと厳しい。Rustの場合は、公式ドキュメントはその他の資料で迷子になったときに戻ってくる場所として認識しておいたほうがよいと思う。

### 1. 『プログラミング言語Rust入門』

C、C++の知識のない人間がRustを始めるにはまずここからがよいと思う。簡潔な語り口と丁寧な説明で、入門書の名前にふさわしい。基本文法や所有権のおおまかな概念理解をすませておくと、先々の言語仕様にも必要以上にひるまずに進めるはず。

### 2. とりあえず書いてみる

なんとなくいけそうな感じになってきたら、何でもいいから書いてみる。Rustはコンパイラに手取り足取り教えてもらって初めて分かるようになる言語だ。だから言語に最短で慣れるには、エラーを取り除くということをたくさんやる、つまりエラーがいっぱいのコードを書くのがいい。  
作りたいものがなかったり、作りたくてもハードルが高すぎる場合は、競技プログラミングの問題を解いてみよう。  
AtCoderでもいいが、I/Oのことを考えないでとりあえず書いてみたい場合はLeetCodeやProject Eulerがおすすめ。前者は数学以外の問題もたくさんあり、後者はすべて数学の問題になっているという違いはあるけれど、いずれも基本的な配列の操作や制御フローの学習に向いている。特にLeetCodeは以下の点でおすすめ。

- ヒントが充実しているし、ユーザー数が多く、ディスカッションもたくさん行われているので、つまずきにくい
- わかりやすい難度表示があるのでトライのハードルが低い

### 3. 『実践Rustプログラミング入門』

雰囲気で書けるようになってきたらこれを読んで写経してみる。ふわっとした知識だったところが整理され、理解が深まる感じがする。用語の説明不足も、ここまできたら許容範囲に収まっているはず。  
逆に言うと、雰囲気ででも書けないと、序盤からわからない用語が出てきてつらい気持ちになるはずなので、これで入門するのはおすすめできない。タイトルの入門は「実践的なプログラミングへの入門」であって「文法や基礎知識への入門」ではない。

### rustlings

公式で提供されているRustコードのデバッグ問題集。正直駆け出しにはかなり難度が高いが、『実践Rustプログラミング入門』まで読めたら数問を除いてパスできるようになっているはず。また、雰囲気が分かってきたトピックの穴を洗い出すためにも使える。

### 他言語との比較記事

HaskellとRustの比較記事をいくつか読んだが、Haskellの知識があれば万事うまくいくわけでは全然ないので、足場にしすぎないことが大事。

#### ざっくりした対応関係

Haskell | Rust
--- | ---
Maybeモナド | Option型
Eitherモナド | Result型
data | struct enum
case | match