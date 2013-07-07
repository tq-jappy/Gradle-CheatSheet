よく使うプロパティ
=========================

.. csv-table::
   :header: "プラグイン", "プロパティ名", "型", "説明"
   :class: "table4"

   "標準", "rootProject", "Project", "ルートプロジェクト"
   "標準", "rootDir", "File", "プロジェクトのルートディレクトリ"
   "標準", "buildDir", "File", "ビルドディレクトリ"
   "java", "sourceSets", "SourceSetContainer", "ソースセット（デフォルトでmainとjava）"
   "java", "sourceCompatibility", "JavaVersion", "コンパイル時に使用するJavaのバージョン(1.7など)"
   "java", "manifest", "Manifest", "マニフェスト"

拡張プロパティ
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   // 全体
   ext {
     springVersion = "3.1.0.RELEASE"
     emailNotification = "build@master.org"
   }

   // 他のオブジェクト
   sourceSets.all { ext.purpose = null } // 1. プロパティを追加
   sourceSets.main.purpose = "production" // 2. プロパティに値をセット

プロパティを追加せず、直接値をセットしても（1.6時点では）エラーにならないが、
非推奨である（以下の警告が出力される）。拡張プロパティを追加する時は、extを使うことを推奨。

::

  Deprecated dynamic property: "purpose" on "source set 'main'", value: "production".
