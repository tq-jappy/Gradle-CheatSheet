よく使う処理
=========================

copy
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   // 方法1: Copyタスクを使う場合
   task myCopy2(type: Copy) << {
     from 'src/*.txt'
     into 'dest'
   }

   // 方法2: Project.copy() メソッドを使う場合
   task myCopy << {
     copy {
       from 'src/*.txt'
       into 'dest'
     }
   }

単なるコピーだけならCopyタスクの方がよい。
Project.copy() メソッドは他のタスクの中に組み込んで使うことが多い。

unzip
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   task myUnzip << {
     copy {
       from files('archive.zip').collect { file -> zipTree(file) }
       into 'dest'
     }
   }

rename
~~~~~~~~~~~~~~~~~~~~~~~~~

filter
~~~~~~~~~~~~~~~~~~~~~~~~~

tar
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   task myTar(type: Tar) {
     compression = Compression.GZIP // NONE/GZIP/BZIP2
     from 'content'
   }

外部コマンド実行
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   // 方法1: Copyタスクを使う場合
   task myExec(type: Exec) << {
     commandLine 'echo', 'hello'
   }

   // 方法2: groovy の execute() メソッドを使う場合
   task myCopy << {
     ['echo', 'hello'].execute()
   }
