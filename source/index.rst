=========================
Gradle Cheat Sheet
=========================

build.gradle
=========================

.. sourcecode:: groovy

  // plugins
  apply plugin: "a_name"
  
  // global 
  foo = "value"
  
  // repositories
  repositories {
    mavenCentral()
    mavenLocal()
    maven {
      url "http://repository1/"
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
    runtime 'g:bbb:1.0.0'
    testCompile 'junit:junit:4.11'
    testRuntime 'aaa:bbb:1.0.0'
    doc 'aaa:bbb:1.0.0@zip'
  }
  
  // tasks

Task
=========================

.. sourcecode:: groovy

   task hello << {
     println "hello!"
   }

   task archive (type: Zip) {
     from "src"
     // "build/distributions/xxx.zip"
   }

よく使うプロパティ
=========================

.. csv-table::
   :header: "プラグイン", "プロパティ名", "説明"

   "java", "sourceCompatibility", "コンパイル時に使用するJavaのバージョン(1.7など)"

Artifacts
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

War
=========================

TBD

Ear
=========================

TBD

マルチプロジェクト
=========================

- 階層

:file:`settings.gradle`

.. sourcecode:: groovy

   include "sub1", "sub2"

ルートプロジェクトの build.gradle はそのままサブプロジェクトでも生きる

- フラット

よく使う処理
=========================

.. sourcecode:: groovy

   task hello << {
     copy {
       from 'src/*.txt'
       into 'dest'
     }
   }

- copy
- rename
- filter
- zip


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
