+++
title = "Zig ファースト・インプレッション"
date = 2022-09-17
math = false
[taxonomies]
categories = ["code"]
tags = ["Zig"]
+++
最近見かけるようになった言語・Zigを少しだけ触ってみたので、ファーストインプレッションを書き留めておく。

[kyoheiu/ulid-zig: Simple ULID implementation for Zig](https://github.com/kyoheiu/ulid-zig)

Better Cというのは言語仕様の面ではその通りかなと思う。だけど個人的には、あえてBetter Goと呼んだほうが、ユーザー層の重なりを表現できるんじゃないかと感じる。

Zigは今のところRustと比較されよく話題になっているが、これはここ最近で最も成功しているオープンソース言語であるRustをターゲットに色々なhypeが行われているからで、実際にはRustとZigは全然違う言語で、解決しようとしている問題も違えば哲学も違うので、比較する意味はあまりない。

そもそもその言語がどんな問題を解決すべく出てきた言語なのか、というのがけっこう気になる性質で、Rustはそこのところが非常に明瞭だったのに対して、Zigは何なんだろう、というのはまだしっかりとはいない。けれども、触ってみて、おそらく想定している「問題」はおおむねCのそれなんだろうな、という気はしている。そうするとそれこそBetter C、もしくはintegrated with CとしてZigを使っていく、というのが正しい使い道なんだろう。そしてそこにはRustはいないと思うのですよね…。それよりは、やはりC - Go - Zigのラインで本当は捉えるべき言語なんじゃないかと思っている。

そして個人的な手触りとしては明らかにGoよりもZigのほうが良い。良いというのは、stdのシンプルさだったりstraightforwardな感じが良い。Goを使うくらいだったら未成熟でもZigのほうを選びたい（どんなシチュエーションでそんな選択肢が出てくるかはまだ分からないが）。ZigがGoを置き換える未来はよい未来だと思う。

ちなみにここが好き！という点は、`u80`などの数値プリミティブタイプを勝手に作って使えるところ。これのおかげでULIDの実装がだいぶスッキリしました。

真剣に使っていくには、公式のパッケージマネージャーがなかったり、language serverが弱かったりするのでまだ厳しい。このへんの環境整備は、最近の企業発の言語（Go, Swift, Rust, Kotlin）と比較するとちょっと微妙というか、ぎこちないなぁという印象を受ける。

あと、別にZigに限らず、新言語が本格的に受容されて使われていくには、上記の「問題解決」や「環境整備」と同時に「キラーライブラリ／キラーアプリ」が必要、というのは感じる。Rustの場合はserdeその他のライブラリ、Haskellで言うとParsecとかPandoc、そういったものが今後出てくるのか。