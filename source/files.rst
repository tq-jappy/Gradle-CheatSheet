ファイルコレクション
=========================

.. sourcecode:: groovy

   # Using a relative path
   File configFile = file('src/config.xml')

   # Using a File object
   configFile = file(new File('src/config.xml'))

   # FileCollection
   FileCollection collection = files('src/file1.txt', new File('src/file2.txt'), ['src/file3.txt'])
   collection.each { File file -> println file.name }
   String path = collection.asPath

   # Create a file tree using path
   FileTree tree = fileTree(dir: 'src/main').include('**/*.java')

   # Create a file tree using closure
   tree = fileTree('src') {
     include '**/*.java'
   }

   # Create a file tree using a map
   tree = fileTree(dir: 'src', include: '**/*.java')

ファイルコレクションは、コピー元ファイル、ファイル依存関係などの指定で使われる。
