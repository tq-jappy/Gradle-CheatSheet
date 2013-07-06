依存関係の管理
=========================

.. sourcecode:: groovy

   dependencies {
     compile 'org.springframework:spring-core:2.5'
     // アーティファクトオンリー記法
     compile 'org.gradle.test.classifiers:service:1.0:jdk15@jar'
     // 推移的な依存関係の除外
     compile 'org.hibernate:hibernate:3.0.5') {
        transitive = true
     }

     // ローカルのファイル依存関係
     compile fileTree(dir: 'libs', include: '*.jar')
   }

依存関係のキャッシュ
~~~~~~~~~~~~~~~~~~~~~~~~~

dependencies に記述した依存するサードパーティのアーティファクト（依存モジュール）は
${GRADLE_USER_HOME} > ${USER_HOME}/.gradle/cache 以下にキャッシュされる。
Mavenキャッシュと管理方法が異なるので、そのまま Maven リポジトリとして公開はできない、


.. warning::

  Jenkins Gradle Plugin 1.22 では GRADLE_USER_HOME は Jenkins の
  ワークスペース(例えば :file:`/var/lib/jenkins/workspace/job1`)がセットされる。

  Workspace Cleanup Plugin などを使ってビルド前にワークスペースをクリーンしていると、
  毎回ローカルキャッシュも削除されてしまい、ビルドの度に
  ライブラリを毎回ダウンロードすることになってしまうので注意（最新の1.23では解消されており、
  :file:`/var/lib/jenkins/workspace/.gradle` にキャッシュされる）
