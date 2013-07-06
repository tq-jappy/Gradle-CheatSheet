Gradle-CheatSheet
=================

Gradleのチートシートです。個人的に欲しいと思っていたのですが、見当たらなかったので試しに作ってみました。

フィードバック大歓迎です。

チートシートは Sphinx で作られており、HTMLやPDFに生成することができます。

そのままブラウザで見ることもできます:

https://github.com/tq-jappy/Gradle-CheatSheet/blob/master/source/index.rst

## 免責事項

内容の確認はGradle1.6で行なっています。
それ以外のバージョンではエラーになるかもしれません。

## ビルド

このチートシート自体も Gradle でビルドできるようになっています。

ただし、Windows 以外ではビルドに失敗します（外部コマンドの実行の際に.batを指定しているため）

以下のタスクが利用できます。

- makeHtml
- archiveHhtml
- makePdf
- install

### HTMLを生成する

```
gradle makeHtml
```

中では以下のSphinxのビルドバッチを実行しているだけなので、そのまま以下のコマンドでも可。

```
make html
```

### PDFを生成する

PDFの生成にrst2pdfを使っているので、そのためのセットアップが必要です。
また、Windows以外だと設定ファイルの書き換えが必要です。

1. Windows版 PIL をインストール
  http://www.pythonware.com/products/pil/
2. rst2pdf をインストール
```
easy_install rst2pdf
```
3. VLゴシックフォント(http://dicey.org/vlgothic/) を :file:`C:\Windows\Fonts` にインストール

セットアップ後は下記コマンドで PDF が生成できます。

```
gradle makePdf
```

または普通に

```
make pdf
```

### Mavenローカルリポジトリにインストール

ZipでアーカイブしたHTMLファイルとPDFをMavenのローカルリポジトリにインストールします。

```
gradle install
```