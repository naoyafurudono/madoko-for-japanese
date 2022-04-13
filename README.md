# madoko-for-japanese

[Madoko](https://github.com/houshuang/madoko/blob/master/doc/reference.mdk) (Markdown processor written in Koka)
を使うとマークダウン拡張なソースファイルからLaTeXやHTMLを生成できます。
デフォルトではXeLaTeXをPDF向けのレンダリングに使っているのですが、このレポジトリではLuaLaTeX に置き換えています。
それにより日本語でもMadokoでPDFを出力できるようになりました！
Madokoの良いところや使い方は[公式リファレンス](http://madoko.org/reference.pdf)を参照してください。
ちなみに、HTMLを出力したいだけならデフォルトで十分なはずです。

## このテンプレートの使い方

`my-doc.mdk`をMadokoで`out/my-doc.pdf`に変換する方法を紹介します。

1. Madokoをインストールする。
   1. `npm`が必要です。詳しくは[公式リファレンス](http://madoko.org/reference.pdf)からインストール方法を探してください。
2. このリポジトリをクローンする
3. ディレクトリ構成を変えずに、リポジトリのルートディレクトリ（`README.md`があるディレクトリ）で次のコマンドを走らせる。

```sh
madoko --pdf -vv --odir=out my-doc.mdk   
```

これで`out/my-doc.pdf`が出力されたはずです。

## 日本語対応に必要だったこと

僕が日本語対応のためにしたのは、Madokoを実行する際のオプション設定だけです。
その設定ファイルが`style/ltjsarticle.mdk`で、`my-doc.mdk`ではそれを読み込むことで日本語を有効にしています。
なので、`[INCLUDE=style/ltjsarticle]`の記述を削除すると、Madokoはデフォルト設定でソースを処理するようになり、
（おそらく）ASCII以外を無視します。

`style/ltjsarticle.mdk`で日本語対応に効いているのは以下の部分です。

```
Latex         : lualatex
Pdf Latex     : lualatex
Doc Class     : []ltjsarticle.cls
Package       : luatexja 
```

上から順に数式のレンダリング、PDFのレンダリングに使うLaTeXエンジンの指定、ドキュメントクラスの指定、LaTeXパッケージの読み込みを行います。
僕はあまり詳しくないのですが、XeLaTeXは日本語が苦手そうだったのでLuaLaTeXにしました。
