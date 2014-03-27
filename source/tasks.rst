よく使うタスク
=========================

まったくプラグインを適用していない場合でも使えるヘルプタスク

.. csv-table::
   :header: "タスク名", "説明"
   :class: "table2"

   "tasks", "タスク一覧を出力"
   "dependencies", "依存関係一覧を出力"
   "projects", "サブプロジェクト一覧を出力（マルチプロジェクトを使っている場合に使う）"
   "properties", "プロパティ一覧を出力"
   "wrapper", "Gradleラッパーファイルを生成(> 1.7)"

プラグインを適用して使えるようになるタスク

.. csv-table::
   :header: "プラグイン", "タスク名", "説明"
   :class: "table3"

   "java", "jar", "JARファイルを作成"
   "java", "assemble", "JAR（やWARやEAR）を作成"
   "java", "test", "ソースコードをテスト"
   "java", "check", "テストし、検証タスクを実行する。testタスクに依存"
   "java", "javadoc", "JavaDocを生成"
   "java", "build", "すべてのアーカイブ作成、テスト実行、検証タスクを実行"
   "java", "clean", "プロジェクトのビルドディレクトリを削除"
   "war", "war", "WARファイルを作成"
   "ear", "ear", "EARファイルを作成"
   "java & maven", "install", "アーティファクトをリポジトリに登録する"
