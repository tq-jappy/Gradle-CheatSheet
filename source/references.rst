よく使う処理
=========================

copy
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   // 方法1: Copyタスクを使う場合
   task myCopy(type: Copy) << {
     from 'src/*.txt'
     into 'dest'
     // include '**/*.html'
     // exclude '**/*.jsp'
     // rename { String fileName -> fileName.replace('-staging-', '') }
   }

   // 方法2: Project.copy() メソッドを使う場合
   task myCopy2 << {
     copy {
       from 'src/*.txt'
       into buildDir
     }
   }

単なるコピーだけならCopyタスクの方がよい。
Project.copy() メソッドは他のタスクの中に組み込んで使うことが多い。

mkdir
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   task myMkdir << {
     file('tmp').mkdir()
   }

unzip
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   task myUnzip << {
     copy {
       from zipTree('aaa.zip')
       into buildDir
     }
   }

tar
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   task myTar(type: Tar) {
     compression = Compression.GZIP // NONE/GZIP/BZIP2
     from 'content'

     destinationDir = file('dest') // default: project.distsDir = "build/distributions"
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
