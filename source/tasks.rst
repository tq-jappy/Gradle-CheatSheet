よく使うタスク
=========================

プラグインを使うことでプラグインに応じてタスクが追加される。
Gradleを使うようなケースでは、最低でもjavaプラグインは使うはず。

.. csv-table::
   :header: "プラグイン", "タスク名", "説明"
   :class: "table3"

   "java", "compileJava", "sourceSets.main.java.srcDirs(デフォルトは[src/main/java])にあるJavaソースコードをコンパイル"
   "java", "jar", "JARファイルを作成"
   "java", "test", "sourceSets.test.java.srcDirs(デフォルトは[src/test/java])にあるJavaソースコードをテスト"
   "java", "check", "検証タスクを実行する。testタスクに依存。"
   "java", "javadoc", "JavaDocを生成"
   "java", "build", "すべてのアーカイブ作成、テスト実行、検証タスクを実行"
   "java", "clean", "プロジェクトのビルドディレクトリを削除"
   "war", "war", "WARファイルを作成"
   "ear", "ear", "EARファイルを作成"
   "java & maven", "install", "アーティファクトをリポジトリに登録する"

まったくプラグインを使っていない場合でも、以下のようなヘルプタスクが使える（他にもある）。

.. csv-table::
   :header: "タスク名", "説明"
   :class: "table2"

   "tasks", "タスク一覧を出力"
   "dependencies", "依存関係一覧を出力"
   "projects", "サブプロジェクト一覧を出力（マルチプロジェクトを使っている場合に使う）"
   "properties", "プロパティ一覧を出力"
