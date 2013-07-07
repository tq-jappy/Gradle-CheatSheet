build.gradle のテンプレート
=========================

.. sourcecode:: groovy

  // plugins
  apply plugin: "java"
  apply plugin: "maven"
  apply plugin: "groovy"
  apply plugin: "application"

  // default tasks
  defaultTasks 'clean', 'build'

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
    maven { url "http://maven.seasar.org/maven2" }
    maven { url "http://repository.jboss.org/nexus/content/groups/public-jboss/" }
    maven { url "http://repository.apache.org/content/groups/public" }
    maven { url "http://download.java.net/maven/glassfish" }
  }

  // configurations
  configurations {
    doc // extra configuration
  }

  // dependencies
  dependencies {
    compile 'org.codehaus.groovy:groovy-all:2.0.5'
    // runtime
    testCompile 'junit:junit:4.11'
    // testRuntime

    // extra configuration
    doc 'g:m:v@zip' // @ext

    // providedCompile(War plugin)
    // providedRuntime(War plugin)
  }

  // tasks

大元であるProjectのプロパティやメソッドが呼ばれる。
例えばプラグインを適用するapplyはProject.apply()の呼び出し。
sourceCompatibilityのようにプラグイン(javaプラグイン)を適用することで
追加されるプロパティもある。

build.gradle の分割
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

  apply from: "gradle/foo.gradle"