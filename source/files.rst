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

FileCollection型のプロパティ

- sourceSets.main.compileClasspath
- sourceSets.main.runtimeClasspath

Gradleではファイルの集まりを指定するのに、パス文字列、File, FileCollection, Closureなど
どれでも利用できるケースが多い（コピー元ファイル、ファイル依存関係など）