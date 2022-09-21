+++
title = "バックアップについて考える"
date = 2021-03-22
math = false
[taxonomies]
categories = ["code"]
tags = ["Linux", "Arch Linux", "dotfiles", "Static Site Generator"]
+++
[Arch Linuxを再インストールした話](@/posts/reinstall-arch.md)に関連して。

### dotfilesの扱い方

今回感じたのは、最低限i3と、ターミナルエミュレーター / vifm / nvimを入れて、dotfilesをリモートリポジトリから引っ張ってくれば作業環境は整うわけなので、追加のバックアップ作業はもしかしたら要らないのかも、ということ。これまではtimeshiftで定期的にバックアップをとっていたのだが、結局一度も使わないままだったし…。  
逆に上記のパッケージのdotfilesがリモートに存在しない場合、動くことは動くが、細かい設定を整えようとするとかなり面倒くさいことになってしまうので、思っていた以上にdotfilesのバックアップは大事だったとも言える（r/unixpornに貼りつけるだけのアレじゃなかった）。

シェルスクリプトでdotfilesの設定ファイルのシンボリックリンクを各所に貼るプログラムを書いている人が多いと思うが、同じようなものをNimでさくっと書いてみたので貼っておきます。

<script src="https://gist.github.com/kyoheiu/9b5c634d38f26d1b67ad1d34bb29ef76.js"></script>

`os`ライブラリの`createSymlink`は同名のファイルが存在した場合failになるので、ファイルを削除してからシンボリックリンクを作成している。利用する場合は自己責任でお願いします。
nvimのcolorsディレクトリを除いているのはこれ以上コードが入れ子になるのが嫌だったから、程度の理由。

### 書きっぱなしコードの扱い方

これまで練習用に書いてきたHaskellやらRustやらのコードはクリーンインストールによりすべて消えてしまった。まあ見返すことはほとんどなかったし、作り途中のプロジェクトはGitLabのプライベートリポジトリに上げながらやっているから無事だ。それ以外にも、ちょっと面倒な感じの、たとえばHaskellでスクレイピングするプログラムの骨子などはサイトに上げているので、残りのちまちましたやつ（Project Eulerの解答とか）は別にいいかな…と思いつつ、でもやっぱりちょっとさびしい。  
こういう断片的なコードをいちいちGitHub GistsやGitLab Snippetsに上げるか、それとも書き捨てのつもりで気にしないかはけっこう微妙な問題だと思う。見返さなかったとはいえ、振り返ると意外と発見があったり、最近書いていない言語を思い出すのに使ったり、ということもあるだろうし、悩ましい。  
[Gistsに自動アップロードするCLIを書いている](https://note.com/konojunya/n/n461544d2f881)方を見つけて、なるほど、と思ったが、書いた端から上げたい感じもある。VS Codeのエクステンションとか、もうありそうだな…と思ったら[あった](https://github.com/kenhowardpdx/vscode-gist)。自分なりに使いそうなフローで何かCLIを作ってみてもいいかもしれない。  
GitLabも[Snippets APIの紹介がとてもよくまとまっている](https://docs.gitlab.com/ee/api/snippets.html#get-a-single-snippet)のでけっこう使いやすそう。

### 静的サイトジェネレーターの落とし穴(?)

それと、Hugo / Zolaなどの静的サイトジェネレーターを使っている場合は、サイト上にフロントマター付きの.mdファイルが存在するわけではないので、もしデータが消えてしまった場合はサイト上のテキストをコピーしてきて、あらためて.mdとしてタグ付けをしないといけない（もしくはサイトをスクレイピングして.mdファイルを生成するプログラムを書くか。できなくはないが面倒ではある）。  
幸い、数か月前までプライベートリポジトリにサイトごと上げていたので、手作業での.md復旧は数記事で済んだのだが、これがまったくバックアップがない状況だったらけっこう辛かったかもしれない。プライベートリポジトリでもいいので更新時にpushしておくのが大事だとしみじみ思った（もちろん、github.ioなどでサイトをホスティングしている場合は当然バックアップがとれているのでこんなことは考えなくていい）。

### おわりに

以上に書いたものはすべてgitのリモートリポジトリの存在が前提になっている。ここに何か落とし穴がまだあるかもしれない。