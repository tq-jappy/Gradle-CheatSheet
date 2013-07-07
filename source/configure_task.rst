タスクのカスタマイズ
=========================

.. sourcecode:: groovy

  // プロパティ: 個別に
  fooTask {
    fooTaskProperty = "xxx"
    fooMethod "yyy"
  }

  // プロパティ: まとめて
  [barTask, bazTask]*.barbazProperty = "zzz"

  // Gradle 起動時
  fooTask { }

  // タスクの最初に実行
  aTask.doFirst { }

  // タスクの最後に実行
  aTask.doLast { }
  aTask << { }

タスクにどのようなプロパティがあるかを調べるには、そのタスクのTask Typeを辿ればよい。

例1: javaプラグインで追加されるcleanタスクのTask TypeはDelete。

例2: warプラグインで追加されるwarタスクのTask TypeはWar。
