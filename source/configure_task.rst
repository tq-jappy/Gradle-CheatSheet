タスクプロパティによるタスクのカスタマイズ
=========================

.. sourcecode:: groovy

  // 個別に
  fooTask {
    fooTaskProperty = "xxx"
    fooMethod "yyy"
  }

  // まとめて
  [barTask, bazTask]*.barbazProperty = "zzz"

タスクにどのようなプロパティがあるかを調べるには、そのタスクのTask Typeを辿ればよい。

例1: javaプラグインで追加されるcleanタスクのTask TypeはDelete。

例2: warプラグインで追加されるwarタスクのTask TypeはWar。
