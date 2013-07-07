マルチプロジェクト
=========================

階層
~~~~~~~~~~~~~~~~~~~~~~~~~

::

  + parent
    + sub1
    + sub2
    + sub3

ルートプロジェクトの :file:`parent/build.gradle`

.. sourcecode:: groovy

   allprojects {
     task hello << {task -> println "I'm $task.project.name" }
   }
   subprojects {
     hello << {println "- I depend on water"}
   }
   project(':sub1').hello << {
     println "- I'm the largest animal that has ever lived on this planet."
   }

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

::

  + parent
  + sub1
  + sub2
  + sub3

ルートプロジェクトの :file:`parent/settings.gradle`

.. sourcecode:: groovy

   includeFlat 'sub1', 'sub2', 'sub3'