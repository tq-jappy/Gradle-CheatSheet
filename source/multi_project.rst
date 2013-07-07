マルチプロジェクト
=========================

ルートプロジェクトの :file:`parent/build.gradle`

.. sourcecode:: groovy

   allprojects { task hello << {task -> println "root and all sub projects" } }

   subprojects { hello << {println "all sub projects" } }

   project(':sub1').hello << { println "one sub project" }

階層
~~~~~~~~~~~~~~~~~~~~~~~~~

ルートプロジェクトの :file:`parent/settings.gradle`

.. sourcecode:: groovy

   include "sub1", "sub2", "sub3"

サブプロジェクト間の依存関係

.. sourcecode:: groovy

   dependencies {
     compile project(':sub1')
     compile project(path: ':sub2', configuration: 'abc')
   }

サブプロジェクトのタスクを実行

::

  :sub1:build

フラット
~~~~~~~~~~~~~~~~~~~~~~~~~

ルートプロジェクトの :file:`parent/settings.gradle`

.. sourcecode:: groovy

   includeFlat 'sub1', 'sub2', 'sub3'
