+++
title = "OSSのREADME.md更新について"
date = 2021-05-01
math = false
[taxonomies]
categories = ["code"]
tags = ["Nim", "Git", "GitHub"]
+++
先日publicリポジトリに移したmarkdownパーサ`nmark`をちまちま更新しているのだが、更新するたびに以下のような作業が発生していてだんだん面倒になってきた。

<script>window.addEventListener("message", function(e) {var i = e.data.split(":")[1];var h = e.data.split(":")[2];if (e.data.split(":")[0] == "swimlanes-io" && i && h) {document.getElementById("__sw-io-" + i).setAttribute("style","height:" + h + "px");}}, false);</script><div id="__sw-io-fZAw"><iframe style="border:none; width:100%; height:100%" scrolling="no" src="https://cdn.swimlanes.io/dist/embeded.html#fZA7D8IwDIT3/ApvQKTC3gEJiYqJhYq9aWJoROpEeUj039MHUKlDN8v3new7zqkV/gXJKRERvE1RE3LO2LTPjjAO+Y8ItsXYaHrOgBRBbMvyssuBEBVECx6lcDF5hBpJNgPJ/tjCU5Fua4OgKURhzHSvWsVBQqZyjwZFwFFc4ZvOoX/0qWCzPwwC1EkbtVlYvjGldR3g21kf+yjz98s67lMdt+J0vhbsAw==#fZAw"></iframe></div>

（さっき見つけた[swimlane.io](https://swimlanes.io/)を使ってみたかったのであえて作ってみた）

今思いつく解決策としては、

- ベンチマーク出力を２つの外部プログラム（静的サイトジェネレータ、hyperfine）に頼っているので、`nmark`内に実装し、SCFなりでREADME.mdを生成する関数も書いて更新する。
- ベンチマークを画像として出力し、リポジトリに含めて`git push`し、README.md内には画像リンクとして取り込む。
- `git push`をトリガーとしてベンチマークをとってくれるCIを設定し、出力を取り込んでREADME.mdを更新する（もしくは更新するところまでGitHub Actionsなどで実装する）。

という感じだが、

- `nmark`内に全部取り込むのは（可能だが）間違っている気がする
- 数字を画像で出すのは嫌だ

で、CIを勉強してみようかなぁと思っている。最終的にはジェネレータを使わないという選択になりそうな気がする。

こんなふうに、機能を追加したりバグを修正したりするたびにREADME.md内の細かい数字をアップデートしないといけない状況というのはあると思うのだけれど、何か効率的なやり方があるんだろうか。
