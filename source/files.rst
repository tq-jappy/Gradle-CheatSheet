ファイルコレクション
=========================

.. sourcecode:: groovy

   // ファイル
   File configFile = file('src/config.xml')

   // ファイルコレクション
   FileCollection collection = files('src/file1.txt', new File('src/file2.txt'), ['src/file3.txt'])

   // ファイルツリー
   FileTree tree = fileTree(dir: 'src', include: '**/*.java')

ファイルコレクションは、コピー元ファイル、ファイル依存関係などの指定で使われる。
