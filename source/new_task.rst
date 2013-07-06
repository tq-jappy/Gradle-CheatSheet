タスクの定義
=========================

基本的な作り方
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   task hello << {
     println "hello!"
   }

   // 拡張タスクプロパティ
   task myTask {
     ext.myProperty = "myValue"
   }

タスク型Task typeを使う場合
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   task archive (type: Zip) {
     from "src"
     // "build/distributions/xxx.zip"
   }

Task typeはCopy, Zip, Tar, JavaDocあたりが頻出。

その他
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   // 依存関係をつける
   task taskX(dependsOn: 'taskY') << {
     println 'taskX'
   }

   // 置き換え
   task taskZ(overwrite: true) << {
     println 'taskZ'
   }