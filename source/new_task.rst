タスクの定義
=========================

.. sourcecode:: groovy

   task hello << {
     println "hello!"
   }

タスク型Task typeを使う場合

.. sourcecode:: groovy

   task archive (type: Zip) {
     from "src"
     // "build/distributions/xxx.zip"
   }

代表的なタスク型Type

- Copy
- JavaDoc
- Zip
- Tar
