=========================
Gradle Cheat Sheet
=========================

build.gradle
=========================

.. sourcecode:: groovy

  // plugins
  apply plugin: "java"
  apply plugin: "maven"
  apply plugin: "application"

  // properties
  sourceCompatibility = '1.7'
  def defaultEncoding = 'UTF-8'
  [
    compileJava,
    compileTestJava,
    javadoc
  ]*.options*.encoding = defaultEncoding

  // repositories
  repositories {
    mavenCentral()
    mavenLocal()
    maven {
      url "http://maven.seasar.org/maven2"
      url "http://repository.jboss.org/nexus/content/groups/public-jboss/"
    }
  }

  // configurations
  configurations {
    doc // extra configuration
  }

  // dependencies
  dependencies {
    // 'groupId:module:version'
    compile 'g:m:v'
    // runtime
    // providedCompile
    testCompile 'junit:junit:4.11'
    // testRuntime
    doc 'aaa:bbb:1.0.0@zip'
  }

  // tasks

よく使うタスク
=========================

.. csv-table::
   :header: "プラグイン", "タスク名", "説明"

   "?", "clean", "ビルド時に作ったファイルを削除"
   "java", "compileJava", "sourceSets.main.java.srcDirs(デフォルトは[src/main/java])にあるJavaソースコードをコンパイル"
   "java", "jar", "JARファイルを作成"
   "java", "test", "sourceSets.test.java.srcDirs(デフォルトは[src/test/java])にあるJavaソースコードをテスト"
   "java", "check", "検証タスクを実行する(testタスクに依存)"
   "java", "build", "すべてのアーカイブ作成、テスト実行、検証タスクを実行"
   "war", "war", "WARファイルを作成"
   "ear", "ear", "EARファイルを作成"
   "?", "install", "アーティファクトをリポジトリに登録する"


よく使うプロパティ
=========================

.. csv-table::
   :header: "プラグイン", "プロパティ名", "説明"

   "java", "sourceCompatibility", "コンパイル時に使用するJavaのバージョン(1.7など)"
   "war", "from",

よく使う処理
=========================

copy
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   // 方法1: Copyタスクを使う場合
   task myCopy2(type: Copy) << {
     from 'src/*.txt'
     into 'dest'
   }

   // 方法2: Project.copy() メソッドを使う場合
   task myCopy << {
     copy {
       from 'src/*.txt'
       into 'dest'
     }
   }

単なるコピーだけならCopyタスクの方がよい。
Project.copy() メソッドは他のタスクの中に組み込んで使うことが多い。

unzip
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   task myUnzip << {
     copy {
       from files('archive.zip').collect { file -> zipTree(file) }
       into 'dest'
     }
   }

rename
~~~~~~~~~~~~~~~~~~~~~~~~~

filter
~~~~~~~~~~~~~~~~~~~~~~~~~

tar
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   task myTar(type: Tar) {
     compression = Compression.GZIP // NONE/GZIP/BZIP2
     from 'content'
   }

外部コマンド実行
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   // 方法1: Copyタスクを使う場合
   task myExec(type: Exec) << {
     commandLine 'echo', 'hello'
   }

   // 方法2: groovy の execute() メソッドを使う場合
   task myCopy << {
     ['echo', 'hello'].execute()
   }

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

アーティファクト
=========================

.. sourcecode:: groovy

   artifacts {
     archives jar
   }

   install
     repositories {
       mavenInstaller {
         pom.groupId = 'com.github.tq-jappy'
         pom.version = '1.0.0-SNAPSHOT'
         pom.artifactId = 'example'
       }
     }
   }

実行可能Jar
=========================

.. sourcecode:: groovy

   jar {
       copy {
           from configurations.compile
           into "build/distribution/lib"
       }
       def manifestClasspath = configurations.compile.collect{ 'lib/' + it.getName() }.join(' ')
       manifest {
           attributes "Main-Class" : "foo.bar.Main"
           attributes 'Class-Path': manifestClasspath
       }
       from (configurations.compile.resolve().collect { it.isDirectory() ? it : fileTree(it) }) {
           exclude 'META-INF/MANIFEST.MF'
           exclude 'META-INF/*.SF'
           exclude 'META-INF/*.DSA'
           exclude 'META-INF/*.RSA'
           exclude '**/*.jar'
       }
       destinationDir = file("build/distribution")
   }

実行可能FatJar
=========================

.. sourcecode:: groovy

   jar {
     from configurations.compile.collect { it.isDirectory() ? it : zipTree(it) }
     manifest.mainAttributes("Main-Class" : "foo.bar.Main")
   }

War
=========================

.. sourcecode:: groovy

   configurations {
     moreLibs
   }

   war {
     from 'src/main/webapp'
     classPath configurations.moreLibs
   }

Ear
=========================

.. sourcecode:: groovy

   dependencies {
     deploy project(':war')

     earlib 'log4j:log4j:1.2.15@jar'
   }

   war {
     appDirName 'src/main/app'
   }

マルチプロジェクト
=========================

階層
~~~~~~~~~~~~~~~~~~~~~~~~~

:file:`settings.gradle`

.. sourcecode:: groovy

   include "sub1", "sub2"

ルートプロジェクトの build.gradle はそのままサブプロジェクトでも生きる

フラット
~~~~~~~~~~~~~~~~~~~~~~~~~

静的解析
=========================

.. sourcecode:: groovy

  apply plugin: "checkstyle"
  apply plugin: "findbugs"
  buildscript {
    apply from: 'https://github.com/valkolovos/gradle_cobertura/raw/master/repo/gradle_cobertura/gradle_cobertura/1.2.1/coberturainit.gradle'
  }

  test.jvmArgs '-XX:-UseSplitVerifier'
  [checkstyleMain, checkstyleTest, findbugsMain, findBugsTest]*.ignoreFailures = true
  [checkstyleTest, findBugsTest]*.excludes = ['**/*']

レポート

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

コマンドラインオプション
=========================

.. csv-table::
   :header: "オプション", "説明"
   :class: "exampletable2"

   "-i", "ログレベルをinfoにする"
   "--daemon", "デーモンモードでビルドを実行する"

Wrapper
=========================

before 1.6

.. sourcecode:: groovy

   task wrapper(type: Wrapper) {
     gradleVersion = '1.6'
   }

1.7 or later

.. sourcecode:: groovy

   wrapper {
     gradleVersion '1.6'
   }

run :command:`gradle wrapper`

Proxy
=========================

:file:`gradle.properties`

.. sourcecode:: properties

   systemProp.http.proxyHost=http://proxy:8080/
   systemProp.http.proxyPort=http://proxy:8080/
   systemProp.https.proxyHost=http://proxy:8080/
   systemProp.https.proxyPort=http://proxy:8080/
