依存関係の管理
=========================

dependencies に記述した依存するサードパーティのアーティファクトは
${GRADLE_USER_HOME} > ${USER_HOME}/.gradle/cache 以下にキャッシュされる。
Mavenキャッシュと管理方法が異なるので、そのまま Maven リポジトリとして公開はできない、

.. warning::

  Jenkins Gradle Plugin 1.22 では GRADLE_USER_HOME は Jenkins の
  ワークスペース(例えば :file:`/var/lib/jenkins/workspace/job1`)がセットされる。

  Workspace Cleanup Plugin などを使ってビルド前にワークスペースをクリーンしていると、
  毎回ローカルキャッシュも削除されてしまい、ビルドの度に
  ライブラリを毎回ダウンロードすることになってしまうので注意（最新の1.23では解消されており、
  :file:`/var/lib/jenkins/workspace/.gradle` にキャッシュされる）
